
---
title: "vimrc"
date: "2010-06-10T11:25:00-04:00"
draft: false
---

I recently read Hacking Vim in a fit of nerdiness. Honestly, I don't recommend the book: too much of it involved tricks for gvim, which I don't use and is not practical for use in my work environment. Still, I did glean several useful tricks and configuration tips that will be useful. I shall include my new and improved vimrc file here for others to peruse.

```
" format the status bar
:set laststatus=2
:set statusline=[%F%m%r] [%{&ff}] [%lx%c] [%L]

" always show the tab bar
:set showtabline=2

" key mappings for adding/moving between tabs
:map <C-t> :tabnew<CR>
:map <C-left> :tabp<CR>
:map <C-right> :tabn<CR>

" key mappings for moving by visual lines
:nmap <A-UP> gk
:nmap <A-DOWN> gj
:imap <A-UP> <ESC>gki
:imap <A-DOWN> <ESC>gji

" open a file named the same as a word the cursor is on
:nmap gf :tabf <cfile><CR>

" fill buffers with templates based on file extension
:autocmd BufNewFile * silent! 0r /home/jgreguske/.vim/templates/%:e.tpl

" automatically create ctags when a file is opened, map keys to use them
:autocmd BufWritePost * silent !ctags "%"
:autocmd BufReadPost * silent !ctags "%"
:autocmd VimLeave * call delete("tags")
:nmap s <C-]>
:nmap S :pop<CR>

" automatically save and load sessions
:autocmd VimEnter * call LoadSession()
:autocmd VimLeave * call SaveSession()
function! SaveSession()
    execute 'mksession! $HOME/.vim/session.vim'
endfunction
function! LoadSession()
    if argc() == 0
        execute 'source $HOME/.vim/session.vim'
    endif
endfunction

" undo
:map <C-z> <ESC>:undo<CR>

" add an underline 
:nmap <C-u> yypVr=o

" indentation config
:set tabstop=4
:set expandtab
:set shiftwidth=4
:set smartindent

" When writing Python files check the syntax
:autocmd BufWriteCmd *.py call CheckPythonSyntax()
function CheckPythonSyntax()
    " Write the current buffer to a temporary file, check the syntax and
    " if no syntax errors are found, write the file
    let curfile = bufname("%")
    let tmpfile = tempname()
    silent execute "write! ".tmpfile
    let output = system("python -c "__import__('py_compile').compile(r'".tmpfile."')" 2>&1")
    if output != ''
        " Make sure the output specifies the correct filename
        let output = substitute(output, fnameescape(tmpfile), fnameescape(curfile), "g")
        echo output
    else
        write
    endif
    " Delete the temporary file when done
    call delete(tmpfile)
endfunction
```
