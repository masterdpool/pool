Lbry Mining Pool based on Yiimp

To install the pool you will need:
1. Ubuntu 16.04 VPS
2. Install Script

The install Script will install the pool and all dependencies needed.

TO INSTALL:
1. Log in to VPS
2. Create new user - sudo adduser (username)
3. Add user to sudo group - sudo adduser (username) sudo
4. Log in to new user - sudo su (username)
5. wget https://raw.githubusercontent.com/lbryio/pool/next/install.sh && chmod +x install.sh && ./install.sh
6. Follow the instructions on the screen.

This will setup the pool ready for coin daemons to be added.

You need at least three backend shells (in screen) running these scripts:

	web/main.sh
	web/loop2.sh
	web/block.sh
	
The install script will create a file in the ~/ directory called screen-start.sh which you will need to run. This file has the above scripts in it.


On the website, go to http://server.com/site/adminRights to login as admin. You have to change it to something different in the code (web/yaamp/modules/site/SiteController.php) or the during the install. A real admin login may be added later, but you can setup a password authentification with your web server, sample for lighttpd:

	htpasswd -c /etc/yiimp/admin.htpasswd <adminuser>

and in the lighttpd config file:

	# Admin access
	$HTTP["url"] =~ "^/site/adminRights" {
	        auth.backend = "htpasswd"
	        auth.backend.htpasswd.userfile = "/etc/yiimp/admin.htpasswd"
	        auth.require = (
	                "/" => (
	                        "method" => "basic",
	                        "realm" => "Yiimp Administration",
	                        "require" => "valid-user"
	                )
	        )
	}

And finally remove the IP filter check in SiteController.php



There are logs generated in the /var/stratum folder and /var/log/stratum/debug.log for the php log.

More instructions coming as needed.




Credits:

Thanks to globalzon to have released the initial Yaamp source code.

Thanks to tpruvot for the yiimp source code.

Thanks to oakey22 for the install script.

--

You can support this project donating to tpruvot :

BTC : 1Auhps1mHZQpoX4mCcVL8odU81VakZQ6dR

