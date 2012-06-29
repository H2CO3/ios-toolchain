How to build the toolchain
--------------------------

0.	You'll need Ubuntu 10.04.4 32-bit. Then:

	sudo apt-get remove gcc-4.4 g++-4.4
	sudo apt-get install gcc-4.3 g++-4.3 gobjc-4.3 gcc-4.3-multilib g++-4.3-multilib gobjc-4.3-multilib

	Use update-alternatives to make gcc point to gcc-4.3 and g++ to g++-4.3:

	sudo update-alternatives --remove-all gcc
	sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.3 44 --slave /usr/bin/g++ g++ /usr/bin/g++-4.3 --slave /usr/bin/gcov gcov /usr/bin/gcov-4.3
	Symlink /usr/bin/gcc to /usr/bin/cc as well:

	sudo ln -s /usr/bin/gcc /usr/bin/cc

1.	sudo apt-get install build-essential make automake bison flex git-core subversion
	sudo apt-get install cpio p7zip-full gzip libbz2-dev tar unzip zlib1g-dev
	sudo apt-get install wget xar uuid uuid-dev libssl-dev libcurl4-openssl-dev

2.	cd ~
	mkdir ios-toolchain
	cd ios-toolchain
	svn co http://iphonedevonlinux.googlecode.com/svn/trunk ./
	mkdir -p files/firmware
	mkdir sdks

3.	Download the iPhoneOS3.1.2.sdk.tar.gz and the MacOSX10.5.sdk.tar.gz files.
	Also download the iPhoneOS_3.1.2.tar.gz file.

	MacOSX10.5.sdk.tar.gz:		http://depositfiles.com/files/8xeo4we2y
	iPhoneOS3.1.2.sdk.tar.gz:	http://depositfiles.com/files/t0wj7stsm
	iPhoneOS_3.1.2.tar.gz:		http://depositfiles.com/files/82k4toawd

	Extract the two former to ios-toolchain/sdks, and the latter to files/firmware.
	(You should now have the ios-toolchain/sdks/iPhoneOS3.1.2.sdk,
	ios-toolchain/sdks/MacOSX10.5.sdk and ios-toolchain/files/firmware/current directories.)

4.	If you're not in ~/ios-toolchain, cd back into it
	sudo ./toolchain.sh headers (answer N if it says it's already extracted)
	sudo ./toolchain.sh darwin_sources
	sudo ./toolchain.sh firmware (answer N again if it asks you)
	
5.	sudo ./toolchain.sh build (answer N again if it asks you)
	This will take a *long time* (at least 30 min), especially GCC itself (binutils aren't that large)
	After this you should see: "It seems like the toolchain was built."

6.	Alternatively:
	sudo ./toolchain.sh clean

Enjoy! :-)

(Alternatively, you can download a prebuilt version of the toolchain, without
headers and libraries: http://depositfiles.com/files/75l4yyz6z)

