---
category: post
tags: ['KDE']
---
### Set up the arcanist for Koko
* It was pretty much easy to install. For my **Archlinux** just below command did the work for me.
> yaourt -S arcanist-git 
* Then I had to add ```.arcconfig ``` to the Koko repository so that arc could point to the link where it should publish the changes
> { 
"phabricator.uri":"https://phabricator.kde.org/"
}
* The only problem is with the SSL certificates, as the university campus wireless network uses its own self-signed certificate. This will create problem to access the ssl encrypted web content, pretty much everything related to development :P
* Also university campus network does not allow SSH over it's network. This will prohibit me from committing the changes to the git repository. 
* Hence to use the arcanist, everytime I will have to check for the **curl.cainfo** in the ```/etc/php/php.ini``` and set/unset the environment variable **GIT_SSL_CAINFO** depending on the network I am using.
