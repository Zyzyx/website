
---
title: "12 Tops"
date: "2012-08-26T13:03:00-04:00"
draft: false
---

The [12 Tops Encyclopedia](http://12tops.brolem.net) is back up, now running on <a href="https://openshift.redhat.com/app/">OpenShift</a>. For now, OpenShift is free, and there will always be a free tier, but eventually heavy users of the service will be charged. I don't expect that to be us. I plan to move <a href="http://prithiva.brolem.net">Prithiva</a> and the main Brolem site there too.

Here's how I completed the migration. If you want your own hosted MediaWiki (or whatever else), give OpenShift a try. So far it was pretty painless.

<ol>
  <li>Create an account at http://openshift.redhat.com/</li>
  <li>Install the <strong>rubygem-rhc</strong> package on Fedora. Clients exist for other platforms too.
    <pre># yum install rubygem-rhc</pre></li>
  <li>Create a php-5.3 application and attach mysql to it
    <pre>$ rhc app create -a 12tops -t php-5.3
    $ rhc app cartridge add -a 12tops -c mysql-5.1</pre></li>
  <li>Add the example openshift mediawiki git repository to your app's repo
    <pre>$ cd 12tops
    $ git remote add upstream -m master git://github.com/openshift/mediawiki-example.git
    $ git pull -s recursive -X theirs upstream master</pre></li>
  <li>Push everything up
    <pre>$ git push</pre></li>
</ol>

At this point I had a working fresh installation. However, I had a database dump from an older version of MediaWiki that I needed to import, so there were a few additional steps.

<ol>
  <li>Figure out the system hosting my application and ssh to it. You can figure this out from the OpenShift Web-Management Console.</li>
  <li>Copy up the database dump, and import it to the new database. This is just a mysql command executed in the OpenShift shell. (Delete the dump after importing since it contains password hashes)
    <pre>mysql -u "$OPENSHIFT_DB_USERNAME" --password="$OPENSHIFT_DB_PASSWORD" -h "$OPENSHIFT_DB_HOST" -P "$OPENSHIFT_DB_PORT" [DB-Name] < dump.sql</pre></li>
  <li>Re-run MediaWiki's update script from the website.</li>
</ol>

<strong>Update 1:</strong> Images can be uploaded by copying them from the existing site to a specific directory on the hosting system. The source will be <strong>$wiki_root/images/*</strong>, and you'll want to put them in a similar location on the OpenShift site. However, if you look in your git clone, the <strong>images</strong> directory is actually a broken symlink to <strong>../../data</strong>. I suspect this is to keep images out of the repo itself so it does not count against your quota, but it means you'll need to copy them to the system itself via scp rather than 'git push'. The symlink resolves fine host-side.

<strong>Update 2:</strong> Skins can easily be added, just commit custom ones in the <strong>$root/php/skins</strong> directory in your repository. Include the capitalized header file too (like Dusk.php in my case), and don't forget to update LocalSettings.php if you want it to be the default.

A few maps I neglected to save, but over all the site looks intact. There are still some user-account kinks to work out. For example, only users with confirmed email addresses are allowed to create and edit pages, but the emailer does not seem to be working. It also lacks the dark-skinned theme, but I didn't save that either, and I don't have it in me to bash the CSS into submission again. Does anyone know a good way to edit and review CSS on the fly?

