.. _Installation Guide:

Install on Ubuntu
=================

1. Download and install VMWare Player (or Workstation or Fusion) if needed:

   http://www.vmware.com/products/player/

2. Download Ubuntu Desktop 12.10 (64 bit):

   http://www.ubuntu.com/download/desktop

3. Create new virtual machine and install Ubuntu (ubuntu-12.10-desktop-amd64.iso).
   Default settings work fine.
   Do not forget to install VMWare Tools for Linux.

4. Add the following lines to your /etc/apt/sources.list configuration file.::

        deb http://tinyprod.net/repos/debian squeeze   main
        deb http://tinyprod.net/repos/debian msp430-46 main

5. Refresh the package database.::

        gpg --keyserver http://tinyprod.net/repos/debian/ --recv-keys 34EC655A
        gpg -a --export 34EC655A | sudo apt-key add -
        sudo apt-get update

6. Install the TinyOS (msp430) packages.::

        sudo apt-get install msp430-46 nesc tinyos-tools mspdebug git

7. Create folder for tinyos source tree (this can be in your home too, modify the paths accordingly).::

        sudo mkdir /opt/tinyos
        sudo chown `id -u`.`id -g` /opt/tinyos/

8. Get the tinyos repository.::

        git clone http://github.com/pillforge/tinyos.git /opt/tinyos/

9. Create a new file: /etc/profile.d/tinyos.sh with the following contents.::

        TOSROOT="/opt/tinyos"
        TOSDIR="${TOSROOT}/tos"
        CLASSPATH="{$TOSROOT}/support/sdk/java/tinyos.jar;."
        MAKERULES="${TOSROOT}/support/make/Makerules"
        export TOSROOT TOSDIR CLASSPATH MAKERULES

        LOCATE_JRE=/usr/bin/tos-locate-jre
        type java >/dev/null 2>/dev/null || PATH=`$LOCATE_JRE --java`:$PATH
        type javac >/dev/null 2>/dev/null || PATH=`$LOCATE_JRE --javac`:$PATH
        export PATH

10. Log out and log in (for the profile configuration to take effect) and verify if the toolchain is properly set up.::

        cd /opt/tinyos/apps/Blink
        make vumcr
