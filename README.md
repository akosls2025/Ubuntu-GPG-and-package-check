## Ubuntu GPG and package check:

#### Check installed packages:
-	apt list --installed  -  sorter list
-	dpkg --listlist   -    detailed list
-	apt-cache pkgnames  -   installed package names

#### Checking a package to see if it comes from the official Ubuntu archive:
**500 - archive.ubuntu.com or security.ubuntu.com** - original
-	apt-cache policy <package name> 

#### Check source.list and source.list.d if we have vanilla install we compare it.
-	cat /etc/apt/sources.list
-	ls /etc/apt/sources.list.d/

#### Check external repositories:
-	grep -r ^deb /etc/apt/sources.list /etc/apt/sources.list.d/

#### Check GPG:
-	apt-key list
-	cat /etc/apt/trusted.gpg
-	ls /etc/apt/trusted.gpg.d/
-	ls /usr/share/keyrings

#### Check the GPG for one key:
-	gpg --no-default-keyring --keyring /usr/share/keyrings/<filename>.gpg --list-keys

#### Check the GPG all keys:
-	for f in /usr/share/keyrings/*.gpg; do echo -e "\n--- $f ---"; gpg --no-default-keyring --keyring "$f" --list-keys; done

  ##### **Check the UID and fingerprint – on official webpages**

#### Check the validation of GPG:
-	gpg --keyserver keyserver.ubuntu.com --recv-keys <fingerprint last several character> - try to download it, if faled and no data the key is old, manipulated or bad ID.
-	gpg --list-keys --with-fingerprint – check the keys if the date is too fresh it is suspicious

#### Check packagefiles integrity:
-	sudo apt install debsums
-	sudo debsums -s   -   check the modificate or missing packagefiles, comparing their current checksums with the checksums stored in the package's metadata. The -s (or --silent): Only shows errors
-	sudo debsums -a    -  verify the integrity of all files installed by Debian packages. Checks every file installed by .deb packages against their original checksums.
-	sudo debsums -c  -  Only check config files (conffiles).
-	sudo debsums -l    -  List all files that would be checked.

### Best practice:
-	sudo debsums -as – check all packagefiles and show only FAILED
-	sudo debsums -a | grep -i failed – check all packagefiles and show only FAILED case insesitive
-	sudo debsums -a | grep „FAILED” - check all packagefiles and show only FAILED case sesitive
