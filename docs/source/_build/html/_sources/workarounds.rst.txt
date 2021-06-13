
Workarounds
=============================================

Wait, aren't you selling to me the FAQ section of Slimakoi in a cheap ReadTheDocs page?

:doc:`No, this is. <s&f>`

AttributeError: 'Thread' object has no attribute 'isAlive'
----------------------------------------------------------
websocket-client 0.57.0 uses isAlive(), which got `removed as of Python 3.9. <https://docs.python.org/3/whatsnew/3.9.html#removed>`_ 
It got replaced with is_alive(). As of June 2021, Amino.py installs 0.57.0 by default instead of latest version where it has been fixed.

This breaks out of the box compatibility with Amino.py for Python 3.9 and above.

If you run a version above Python 3.9, install latest websocket-client per 
 | ``pip uninstall websocket-client`` 
 | ``pip install websocket-client`` 

Alternatively, you could revert back to 3.8 which supports both though deprecated.




amino.lib.util.exceptions.ActionNotAllowed: 'Action not allowed.' 
-----------------------------------------------------------------
Due how unspecific this error is, it's hard to track down what specifically causes the issue for you without full support.
Some generic fixes are :ref:`changing your DeviceID <did>` or :ref:`using a proxy <proxies>` to bypass any blocks (if you have any).

.. note:: Feel free to ask for help in `Slimakoi & Friends <https://discord.gg/eMJ6WSkUyA>`_ if your issue isn't fixed after these fixes. Bring up that you tried these, please.


.. _did:

Changing Device ID
^^^^^^^^^^^^^^^^^^
When you start an Amino.py script, it *should* create a device.json file with a DeviceID for you.

.. figure:: devicejson.png
   :alt: Example of device.json with redacted DeviceID 

While that should normally do fine, you can swap the "device_id" value out with a new one. For example, in case your ID got smited or you want to bypass some restriction.

Alternatively you can also add the deviceId parameter to your login function like this:

.. code-block:: python

    client.login(email='YOUR_EMAIL', password='YOUR_PASSWORD', deviceId='variable or string here')

The advantage of this is that it opens the login function up to be used more dynamically, like in loops.



*Getting that ID is your job however*, the easiest way is to `join Slimakoi & Friends <https://discord.gg/eMJ6WSkUyA>`_, go into #bot-commands and type "f!deviceid".
Fluffy is the in-house Device ID generator, you can request 1 ID every 6 hours (4/day).

.. figure:: fluffy_demo.png
    :alt: Example of Fluffy, sending a deviceID

Alternatively, you can sniff out the ID from the network traffic of the mobile app. This is a lot more foolproof, because unless Amino fundimentally changes how the ID's work, you should always be able to get a valid one.
Charles Proxy is a valid option for this, `see this workaround (requires root) <https://blog.ropnop.com/configuring-burp-suite-with-android-nougat/>`_ to get it working above Android 7.

.. figure:: sniffedtree.png
    :alt: Image showing network structure in Charles Proxy

.. figure:: sniffingresult.png
    :alt: Result of device request traffic

.. _proxies:

Using proxies
^^^^^^^^^^^^^
.. This remark is paranoid because connections are HTTPS, I'm leaving it here so I can add it back in case that's a wrong assumption.
.. .. warning:: Proxies are hosted by a third-party and can be malicious, especially when free. The owner has unrestricted access to what you're sending them, use at your risk or switch to a paid service. 

.. important:: Your Proxy needs to be **HTTPS**, else it will not connect.

A proxy is a middleman between you and what you want to access (Amino's servers in this case), doing the request for you with the IP of that proxy.

Amino may impose IP restrictions on some actions, to bypass this you can use proxies. Here is the example implementation of this:

.. code-block:: python

    proxies = {"https": "https://0.0.0.0:0000","https": "https://etcetc:0000"}
    client = amino.Client(proxies=proxies)

If you'd like a recommendation for a proxy checking tool, `Unfx Proxy Checker <https://github.com/assnctr/unfx-proxy-checker>`_ is neat and looks pretty.