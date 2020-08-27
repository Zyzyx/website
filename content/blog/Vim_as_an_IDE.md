
---
title: "Vim as an IDE"
date: "2016-08-02T22:25:31-04:00"
draft: false
---

Crap, it's been over a year since posting an update.

Lately at the office I've had a rare few days where I did not have any high priority work or firedrills to attend to. This is nice because I got a chance to focus on some productivity improvements, and that has been a long time coming for my editor of choice, [Vim](http://www.vim.org). I do a lot of Python development at work, and on reddit somewhere I stumbled onto a link that described how to [turn Vim into an IDE](https://realpython.com/blog/python/vim-and-python-a-match-made-in-heaven/). This provided a lot of features I have not seen since messing with [Eclipse](https://eclipse.org) and .Net. 

You can read that site for yourself, the walkthrough is pretty clear, however there were a couple of additional steps I had to take to make everything work just right. I'll cover that first.

1. I had to install ncurses-compat-libs on Fedora 24 to make auto-completion work. Apparently the YCM server (which is started and stopped with Vim) [needs libtinfo.so.5](https://github.com/Valloric/YouCompleteMe/issues/778#issuecomment-228704671), but libtinfo.so.6 is provided in the normal system install.
2. Remember to ```mkdir ~/.vim/tmp``` to make the session stuff work
3. Install python2-flake8 and pylint (if you want) for the syntax checker and style checker to work (Syntastic)
4. I had to mess with patched fonts a lot to get the special characters to form in Powerline.

I had the bad habit of using tabs to display separate buffers, which is generally discouraged by the Vim community, and I've been trying to stop that lately. Thus this next section is for my own use, a cheat sheet of the various commands I'll have to memorize. I'm sure I'll set bindings if I make a habit of their use. All of these are documented with ```:help``` and on the github project page.

* Buffers (I really need to bind these and look into [BufExplorer](https://github.com/jlanzarotta/bufexplorer))

  **:bn** - go to the next buffer<br>
  **:bp** - go to the previous buffer<br>
  **:bwipeout** - delete a buffer<br>
  **:badd <name>** - add a buffer

* Folding

  **space** - in normal mode, fold or unfold code with the space bar<br>
  **zM** - fold up everything<br>
  **zR** - unfold everything<br>
  **zD** - (recursively delete a fold at the cursor)<br>
  **[z** - Move to the start of the current open fold. If already at the start, move to the start of the fold that contains it.<br>
  **]z** - Move to the end of the current open fold. If already at the end, move to the end of the fold that contains it.<br>
  **zj** - Move downwards to the start of the next fold<br>
  **zk** - Move upwards to the end of the previous fold

* NERDTree

  **Ctrl-N:** toggle the visibility of the tree, open files in new buffers

* Fugitive

  **:Git** -  for running any arbitrary command<br>
  **:GRead** - a variant of git checkout -- filename that operates on the buffer rather than the filename<br>
  **:GWrite** - writes to both the work tree and index versions of a file, making it like git add when called from a work tree file and like git checkout when called from the index or a blob in history<br>
  **:Gdiff** - :Gdiff to bring up the staged version of the file side by side with the working tree version and use Vim's diff handling capabilities to stage a subset of the file's changes<br>
  **:GCommit**<br>
  **:Gblame** - brings up an interactive vertical split with git blame output<br>
  **:Gmove** - does a git mv on a file and simultaneously renames the buffer<br>
  **:Gremove** - does a git rm on a file and simultaneously deletes the buffer

Even with all of these nifty features it is still not a true IDE in my opinion. The I stands for Integrated and the features themselves are not really integrated with each other. I cannot set breakpoints for code in Vim when I run the code in a given buffer, nor can I print out frame information while it is running. I cannot dynamically mess with compile options when I save a script. Do I need these things? Not really, I've been living without the basics for a while, and I confess my code probably shows it. I went back to some earlier stuff and saw code in conditionals that had undefined symbols still there, it was just never found because the conditional never evaluates to True or something. Shameful.

For reference, here's a copy of my working vimrc. This comes from years of hacking, but saw a significant rewrite after following this guide.

```
" GENERAL
set nocompatible                " use vim settings; this must be first
set backspace=indent,eol,start  " allow backspace over everything in insert mode
set directory=~/.vim/tmp        " directory to place swap files in
set iskeyword+=_,$,%,#        " none of these are word dividers
set showtabline=2               " always show the tab bar
set list                        " enable showing tabs and trailing ws
set listchars=tab:>-,trail:-    " small tweak to list option above
set showmatch       " show matching brackets
set filetype=off    " required for Vundle (plugin manager)
set novisualbell    " don't blink the screen on bell
set smartindent     " use language syntax to auto-indent
set laststatus=2    " always show status bar & format it
set statusline=[%F%m%r]\ [%{&ff}]\ [%lx%c]\ [%L]
set paste               " avoid copying staircases
set encoding=utf-8
set fileformat=unix
set number          " turn on line numbers
set numberwidth=6   " We are good up to 999,999 lines
set hidden          " a buffer does not need to be displayed

" Python specific indentation and formating
"au BufNewFile,BufRead *.py "FIXME
set tabstop=4
set softtabstop=4
set shiftwidth=4
set textwidth=79
set expandtab
set autoindent

" JavaScript and web stuff 
au BufNewFile,BufRead *.js, *.html, *.css
    \ set tabstop=2
    \ set softtabstop=2
    \ set shiftwidth=2

" Folding details
set foldenable          " Turn on folding
set foldmethod=indent   " Fold on indents
set foldlevel=100       " Don't autofold anythinhg (but still used manually)
autocmd BufWinEnter *.py setlocal foldexpr=SimpylFold(v:lnum) foldmethod=expr
autocmd BufWinLeave *.py setlocal foldexpr< foldmethod<

" Manage plugins
" follow https://realpython.com/blog/python/vim-and-python-a-match-made-in-heaven/
"
" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
Plugin 'gmarik/Vundle.vim'
Plugin 'tmhedberg/SimpylFold'       " folding improvements
Plugin 'Valloric/YouCompleteMe'     " autocomplete helper
Plugin 'scrooloose/syntastic'       " check syntax on save
Plugin 'nvie/vim-flake8'            " PEP8 checking on save
Plugin 'jnurmine/Zenburn'           " better color theme
Plugin 'scrooloose/nerdtree'        " file browser
Plugin 'jistr/vim-nerdtree-tabs'    " tabs for it
Plugin 'ctrlpvim/ctrlp.vim'         " better searchin
Plugin 'tpope/vim-fugitive'         " git command integration
Plugin 'Lokaltog/powerline', {'rtp': 'powerline/bindings/vim/'} " super status
Plugin 'powerline/fonts'
call vundle#end()
filetype plugin indent on

" Plugin-specific configuration has to come after this line.

" config for SimplyFold
let g:SimpylFold_docstring_preview=1

" config for YouCompleteMe
let g:ycm_autoclose_preview_window_after_completion=1
map <leader>g  :YcmCompleter GoToDefinitionElseDeclaration<CR>

" syntastic config
let python_highlight_all=1
syntax on
let g:syntastic_check_on_open = 1
let g:syntastic_check_on_wq = 0
let g:syntastic_auto_jump = 3
let g:syntastic_always_populate_loc_list = 1
let g:syntastic_auto_loc_list = 1

" NERDTree config
let NERDTreeIgnore=['\.pyc$', '\~$'] " ignore .pyc files

" zenburn config
if has('gui_running')
  set background=dark
  colorscheme solarized
else
  colorscheme zenburn
endif

" virtualenv support
py << EOF
import os
import sys
if 'VIRTUAL_ENV' in os.environ:
  project_base_dir = os.environ['VIRTUAL_ENV']
  activate_this = os.path.join(project_base_dir, 'bin/activate_this.py')
  execfile(activate_this, dict(__file__=activate_this))
EOF

" KEY MAPPINGS
" Don't use Ex mode, use Q for formatting
map Q gq

" easier folding
nnoremap <space> za

" key mappings for adding/moving between tabs
map <C-t> :tabnew<CR>
map <C-LEFT> :tabp<CR>
map <C-RIGHT> :tabn<CR>

" key mappings for moving by visual lines
nmap <A-UP> gk
nmap <A-DOWN> gj
imap <A-UP> <ESC>gki
imap <A-DOWN> <ESC>gji

" undo and redo
map <C-z> <ESC>:undo<CR>
map <C-y> <ESC>:redo<CR>

" Open/Close NERDTree
map <C-n> :NERDTreeToggle<CR>

" open a file named the same as a word the cursor is on
nmap gf :e <cfile><CR>

" fill buffers with templates based on file extension
autocmd BufNewFile * silent! 0r /home/jgreguske/.vim/templates/%:e.tpl

" use file extensions to figure out syntax
au BufNewFile,BufRead *.ks set filetype=kickstart
au BufNewFile,BufRead *.json set filetype=json

" UI TWEAKS
if &t_Co > 2 || has("gui_running")  " do we support colors?
    set hlsearch                    " enable highlights
    nnoremap <cr> :noh <cr>
endif

" automatically save and load sessions
autocmd VimEnter * call LoadSession()
autocmd VimLeave * call SaveSession()
function! SaveSession()
    execute 'mksession! $HOME/.vim/session.vim'
endfunction
function! LoadSession()
    if argc() == 0
        execute 'source $HOME/.vim/session.vim'
    endif
endfunction
```
