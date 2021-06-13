Code samples
=============================================
These are code snippets I use myself.

Subclient login skeleton
------------------------
.. code-block:: python

    import amino

    client = amino.Client()
    client.login(email='YOUR_EMAIL', password='YOUR_PASSWORD')
    subclient = amino.SubClient(comId='YOUR_COMMUNITY_ID', profile=client.profile) 

Loop through subclient chats
----------------------------
.. code-block:: python

    chats = subclient.get_chat_threads()
    for name, id in zip(chats.title, chats.chatId):
        print(name, id) 

You could alternatively swap out the print for your logic.

Get ID from URL (UserID, BlogID, ChatID)
----------------------------------------
.. code-block:: python

    getcode = client.get_from_code("http://aminoapps.com/p/EXAMPLE")
    functionhere(getcode.objectId)

While I would normally add print(dir()) to an obscure object like this, the most interesting thing is objectId to convert Amino URLs to IDs. You use these in functions.

Get Community Object from AminoID
----------------------------

.. code-block:: python

    com_obj = client.search_community(aminoId=VariableOrStringHere)
    print(dir(com_obj))

search_community gives you the object of the community if it finds one, I added dir() to it so you can see what the object actually contains.
