Asterisk OAUTH2.0 connection with Google Voice
===================


Upgrade Asterisk to an OAUTH2.0 connection with Google Voice

The project is a modification of res_xmpp written by  Matt O'Gorman and Joshua Colp.

More information about using Google Voice with Asterisk can be found here 
https://wiki.asterisk.org/wiki/display/AST/Calling+using+Google

If you would like to get involved or need support visit http://www.gvsip.org 

----------

Here is how it works
-------------

The modified version of res_xmpp allows Asterisk to connect via OAUTH2.0 instead of using a plain password.  It also allows Asterisk to obtain updated login credentials directly from Google when the server is disconnected or at start.  Asterisk obtains updated credentials (which Google expires every hour) by using an offline refresh token it obtains for free from http://www.GVsip.com .   This refresh token never changes and only needs to be obtained once.  

 **Primitive Installation Tutorial for Asterisk:**
> 
To install the modification you need to be installing asterisk from source.  (So far this has been verified to work with Asterisk 12.)

> - Go to http://www.GVsip.com and create an account
> - Then navigate to (Portal Menu) -> Google Voice-> Advanced Google OAUTH2.0 Manager (top right part of screen)
> - Then click “Add Google Voice Account” (Green Button)
> - Select an account with Google Voice and on the next screen click “accept”.
> - The username and refresh_token will now be displayed on the next screen.  
> - Repeat as necessary for all of your Google Voice Accounts 
> - Then modify your asterisk configuration /etc/asterisk/xmpp.conf 

So it should look something like this for each of your Google Accounts
>[google]

>type=client

>serverhost=talk.google.com

>username=(username obtained from)

>secret=(refresh_token obtained from GVsip.com)

>priority=25

>port=5222

>usetls=yes

>usesasl=yes

>status=available

>statusmessage="I am using OAUTH2.0 now! Woot!"

>timeout=5


 **To complete the installation:**
> - Download the modified version of res_xmpp.c from Github.  https://github.com/gvsip/Asterisk
> - Copy the modified version of res_xmpp.c to
 /(asterisk source directory)/res/res_xmpp.c
> - Then run “Make install”
> - Then restart asterisk