---
layout: post
---
### Set up the arcanist for Koko
* It was pretty much easy to install. For my archlinux just below command did the work for me.
> yaourt -S arcanist-git 
* The only problem is with the SSL certificates, as the university campus wireless network uses its own self-signed certificate. This will create problem to access the ssl encrypted web content, pretty much everything related to development :P
* Also university campus network does not allow SSH over it's network. This will prohibit me from committing the changes to the git repository. 
* Hence to use the arcanist, everytime I will have to check for the curl.cainfo and set/unset the environment variable GIT_SSL_CAINFO depending on the network I am using.
