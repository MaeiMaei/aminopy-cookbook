Migrating your code after the July update (InvalidDevice)
=========================================================
.. 
   Fuck everything about this page, it's such a stub that I could return back to the drawing board and have the same content. 
   The sniffing section is unintutive and doesn't touch on anything because I can't test it and EVERYTHING IS TOO SMALL.
   You can basically smell my pessimism bleeding through the pages.
   I'll fix it as soon I actually get some sleep, I did the page ma.

Background
----------
| On 22 July 2021, Team Amino rolled out an update to address their API being leaked and misused. 
| `Teased in May on a Leader Amino FAQ <http://aminoapps.com/p/mpkqbd>`_ by Sam Chen, the update has broken Amino.py (at least for running out of the box). 
| The new Device IDs now start with 22, this is how you identify old from new.


Workaround
----------
You now need a 22 Device ID, old Device IDs will not work. For all we are aware, not much should be broken so you *should* be up and running quickly again with a new Device ID.
Even then, please test your code for the sake of your own sanity. FLUFFY DOES NOT GENERATE VALID DEVICE IDS AS OF 09/08/2021.

Here is a video on how to get it from the app outside sniffing.

.. youtube:: z_lRRosScxQ

For a text guide instead: 

#. Go to Amino profile page
#. Cut off your internet access
#. Reset your password
#. Copy entire page and paste it into text document
#. Copy everything after deviceid= and before &sid=
#. Paste into device.json

I'm sure this will get fixed at some point but it works right now, it saves you the effort of sniffing the values out (probably needing a rooted device due Android 7 security changes).

Sniffing as more sustainable alternative
----------------------------------------

.. important:: 
    This section is completely invalidated because if you have elevated permissions, you could also **cat /data/data/com.narvii.amino.master/files/did** for your device id **and save yourself this insanity.** 

.. This is literally just filler content, whatever poor soul wants to rework this shitty guide, go ahead and submit a PR.

In case the method does get fixed, here is a quick off the cuff guide for setting up Charles on an Android device.
This requires Magisk for a module, **if you have root, then I trust you to know what you're doing.** 

You could alternatively also just manually install the certificate to the system store, but enjoy tripping Safetynet.

#. Install https://github.com/NVISOsecurity/MagiskTrustUserCerts, it automatically adds all user certificates to the system store, ONLY INSTALL CERTIFICATES YOU TRUST. SERIOUSLY. 
#. Start Charles Proxy and save the root certificate, transfer it to your device and add it to your user certificates.
#. Go to the SSL Proxy Settings (Proxy -> SSL Proxy Settings or Ctrl + Shift L), add an inclusion and use * for both fields.
#. Reboot your device
#. Go to your WIFI AP and change the proxy settings to your PCs IP and your port (default 8888). You can find out that internal IP per ipconfig or your OS equivalent, save yourself the headache I had from a incorrect IP from the remote Browser dialog.  
#. Allow the connection, if you don't get a dialog to confirm it, you probably messed something up.
#. Enable the proxy and SSL Proxying (padlock)
#. Pray to whatever god you belive in
#. Open Amino and sniff out the Narvii connections

If you're lucky, you should now be able to see in real time what connections your phone makes. It broke on my end and I had about two mental breakdowns trying to fix certificate related issues, so not that I recommend this either.

And even then, I'm already calling that they just do certificate pinning and turn their app into a ticking timebomb.

