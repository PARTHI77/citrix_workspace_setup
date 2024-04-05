# citrix_workspace_setup
How to install the Citrix client on Ubuntu 22.04

The Citrix client provided by Citrix doesn’t currently work with Ubuntu 22.04. There is another way.

Why the normal deb install won’t work  *** not preferered ***

If you’ve tried to install the Citrix Workspace deb package you’ll notice you get the error about libidn11 missing. It looks like Citrix haven’t updated their installer yet.

% sudo dpkg -i icaclient_22.3.0.24_amd64.deb 
[sudo] password for reepy: 
Selecting previously unselected package icaclient.
(Reading database ... 215549 files and directories currently installed.)
Preparing to unpack icaclient_22.3.0.24_amd64.deb ...
Unpacking icaclient (22.3.0.24) ...
dpkg: dependency problems prevent configuration of icaclient:
 icaclient depends on libidn11; however:
  Package libidn11 is not installed.
dpkg: error processing package icaclient (--install):
 dependency problems - leaving unconfigured
Errors were encountered while processing:
 icaclient
 
Normally you’d install that missing package but libidn11 is not available on Ubuntu 22.04. It’s been replaced with libidn12 which isn’t compatible. You can install older versions, but there is an easier way.

***   Install the tar.gz instead

You’ll need to be familiar with the terminal and basic commands. You will not need root access to install this.

From the Citrix Workspace download page in the ‘tarball package’ section download the latest x86_64 tar.gz.
Open a terminal

Get ready to install it:

Go to the directory you downloaded it to: cd Downloads (or whatever directory you downloaded it to).

Make a temporary directory: mkdir icaclient

Go to that directory: cd icaclient

Extract the tar.gz: tar -zxvf ../icaclient*.tar.gz

Start the setup:

Run the setup: ./setupwfc

In the setup answer 1 to install, accept the default install location then no to GStreamer.

Once it takes you back to the menu you can select 3 to quit.

You now need to add some additional SSL certificates:

cd ~/ICAClient/linuxx64/keystore/cacerts

ln -s /usr/share/ca-certificates/mozilla/* .

c_rehash .

To solve ‘Error 61’ there are a few additional steps, thanks to Luk in the comments:

cd ~/ICAClient/linuxx64/keystore/cacerts

ln -s /etc/ssl/certs/* .

~/ICAClient/linuxx64/util/ctx_rehash

You should now be able to use the Citrix client from your web based Citrix portal.


