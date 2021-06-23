
Slimekoi & Friends mirror
=============================================
This is a mirror of Slimekoi & Friend's stuff, minus the parts I've covered in here, note that these are written from Slimakoi's perspective and not mine.

FAQ
---

Can we get banned using Amino.py?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**Depends**, 
Amino doesn't have any specific rules against it, but I've used it for many months and never got punished, if you don't go againts the amino guidelines and the community guidelines, nothing will happen to you. 

But keep in mind that if your account does get disabled and you get device banned, we won't be responsible for it.



My code doesn't work and doesn't show anything
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Print the code,

| When this happens it means that something is blocking you from executing that command or you messed your code somewhere, to check, print the faulty code. 
| 
| Simple example below

.. code-block:: python

    code = client.sub_clients  
    print(code)



My code is returning the error json.decoder.JSONDecodeError
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Issue from Amino,

Amino sometimes due to the servers being trash, it doesn't return anything instead of json, that happens because the library expects json but gets nothing. 

For this you can just ignore it with an try except. Simple example below

.. code-block:: python

   import json

   try:
      client.sub_clients
   except json.decoder.JSONDecodeError:
      pass

How do I use objects?
^^^^^^^^^^^^^^^^^^^^^
For example, if you do subclient.get_chat_members() you'll get UserProfileList(), and for example if you want to get their nickname, you should add .nickname and there you have it.
   


I'm getting error 270, VerificationRequired
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Verify yourself, its super easy, all you need to do is look on the error, there should be an URL thats something like https://service.narvii.com/... then you open it on your browser and do the captcha on your screen. After completed you can close the browser, and you're verified!

Amino.py reference
------------------

.. code-block::
  [messageTypes][com.narvii.model.ChatMessage]

   1 - STRIKE
   50 - UNSUPPORTED_MESSAGE
   58 - MISSED_VOICE_CHAT
   57 - REJECTED_VOICE_CHAT
   59 - CANCELED_VOICE_CHAT
   100 - DELETED_MESSAGE
   101 - JOINED_CHAT
   102 - LEFT_CHAT
   103 - STARTED_CHAT
   104 - CHANGED_BACKGROUND
   105 - EDITED_CHAT
   106 - EDITED_CHAT_ICON
   107 - STARTED_VOICE_CHAT
   109 - UNSUPPORTED_MESSAGE
   110 - ENDED_VOICE_CHAT
   113 - EDITED_CHAT_DESCRIPTION
   114 - ENABLED_LIVE_MODE
   115 - DISABLED_LIVE_MODE
   116 - NEW_CHAT_HOST
   124 - INVITE_ONLY_CHANGED
   125 - ENABLED_VIEW_ONLY
   126 - DISABLED_VIEW_ONLY

   NOT COMPLETED



.. code-block::

   [objectTypes]

   0 - User Profile
   1 - Blog, Image, Poll, Quiz, Story
   2 - Wiki
   3 - Comment
   4 - Blog Category
   7 - Chat Message
   9 - Ads (Wallet History)
   12 - Public Chat, Earnings (Wallet History)
   13 - Wiki Album
   15 - Wiki Submission
   16 - Community
   17 - Community Collection
   18 - Earnings (Wallet History)
   20 - Bookmark
   106 - Shared Folder Album
   109 - Shared Folder Picture
   114 - Sticker Collection
   116 - Chat Bubble
   122 - Avatar Frame
   128 - Topic
   131 - Announcement

   [objectTypes for Chats]
   0 - Direct Message
   1 - Private Group Chat
   2 - Public Chat



.. code-block::
   [punishmentTypes flagTypes]

   0 - Bullying
   1 - Inappropriate Content
   2 - Spam
   3 - Art Theft
   4 - Off-Topic
   5 - Trolling
   100 - Sexually Explicit
   101 - Extreme Violence
   102 - Inappropriate Requests
   106 - Violence Graphic Content or Dangerous Activity
   107 - Hate Speech & Bigotry
   108 - Self-Injury & Suicide
   109 - Harassment & Trolling
   110 - Nudity & Pornography
   104, 105, 200 - Other


**List of Events**

Simple example of how to use this in #aminopy-examples 
.. code-block::
   on_text_message
   on_image_message
   on_youtube_message
   on_strike_message
   on_voice_message
   on_sticker_message
   on_voice_chat_not_answered
   on_voice_chat_not_cancelled
   on_voice_chat_not_declined
   on_video_chat_not_answered
   on_video_chat_not_cancelled
   on_video_chat_not_declined
   on_avatar_chat_not_answered
   on_avatar_chat_not_cancelled
   on_avatar_chat_not_declined
   on_delete_message
   on_group_member_join
   on_group_member_leave
   on_chat_invite
   on_chat_background_changed
   on_chat_title_changed
   on_chat_icon_changed
   on_voice_chat_start
   on_video_chat_start
   on_avatar_chat_start
   on_voice_chat_end
   on_video_chat_end
   on_avatar_chat_end
   on_chat_content_changed
   on_screen_room_start
   on_screen_room_end
   on_chat_host_transfered
   on_text_message_force_removed
   on_chat_removed_message
   on_text_message_removed_by_admin
   on_chat_tip
   on_chat_pin_announcement
   on_voice_chat_permission_open_to_everyone
   on_voice_chat_permission_invited_and_requested
   on_voice_chat_permission_invite_only
   on_chat_view_only_enabled
   on_chat_view_only_disabled
   on_chat_unpin_announcement
   on_chat_tipping_enabled
   on_chat_tipping_disabled
   on_timestamp_message
   on_welcome_message
   on_invite_message
   on_user_typing_start
   on_user_typing_end

   default (For Other events, will be adding more on the next updates!)

Amino.py examples
-----------------

Basic login
^^^^^^^^^^^

.. code-block:: python

   import amino

   client = amino.Client()
   client.login(email='YOUR_EMAIL', password='YOUR_PASSWORD')

List the communities you're in
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

   import amino

   client = amino.Client()
   client.login(email='YOUR_EMAIL', password='YOUR_PASSWORD')

   subclients = client.sub_clients()
   for name, id in zip(subclients.name, subclients.comId):
      print(name, id)

List the chats you're in (from a community)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

   import amino

   client = amino.Client()
   client.login(email='YOUR_EMAIL', password='YOUR_PASSWORD')
   subclient = amino.SubClient(comId='YOUR_COMMUNITY_ID', profile=client.profile)

   chats = subclient.get_chat_threads()
   for name, id in zip(chats.title, chats.chatId):
      print(name, id)

Basic send message function
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

   import amino

   client = amino.Client()
   client.login(email='YOUR_EMAIL', password='YOUR_PASSWORD')
   subclient = amino.SubClient(comId='YOUR_COMMUNITY_ID', profile=client.profile)

   subclient.send_message(message='YOUR_MESSAGE', chatId='YOUR_CHAT_ID')

Discover UserId, BlogId, ChatId by link
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


.. code-block:: python

   import amino
   client = amino.Client()
   email = 'YOUR_EMAIL_HERE'
   password = 'YOUR_PASSWORD_HERE'
   client.login(email=email, password=password)
   # https://aminoapps.com/p/EXAMPLE (example link)
   id = client.get_from_code("EXAMPLE").objectId
   print(id)


Follow/Unfollow
^^^^^^^^^^^^^^^^

.. code-block:: python

   import amino
   client = amino.Client()
   email = 'YOUR_EMAIL_HERE'
   password = 'YOUR_PASSWORD_HERE'
   client.login(email=email, password=password)
   subclient = amino.SubClient(comId='YOUR_COMMUNITY_ID_HERE', profile=client.profile)
   subclient.follow('USER_ID_HERE') #Follow
   subclient.unfollow('USER_ID_HERE') #Unfollow

Like/Unlike
^^^^^^^^^^^

.. code-block:: python

   import amino
   client = amino.Client()
   email = 'YOUR_EMAIL_HERE'
   password = 'YOUR_PASSWORD_HERE'
   client.login(email=email, password=password)
   subclient = amino.SubClient(comId='YOUR_COMMUNITY_ID_HERE', profile=client.profile)
   subclient.like_blog('BLOG_ID_HERE','WIKI_ID_HERE') #Like
   subclient.unlike_blog('BLOG_ID_HERE','WIKI_ID_HERE') #Unlike

Block/Unblock
^^^^^^^^^^^^^

.. code-block:: python

   import amino
   client = amino.Client()
   email = 'YOUR_EMAIL_HERE'
   password = 'YOUR_PASSWORD_HERE'
   client.login(email=email, password=password)
   subclient = amino.SubClient(comId='YOUR_COMMUNITY_ID_HERE', profile=client.profile)
   subclient.block('USER_ID_HERE') #Block
   subclient.unblock('USER_ID_HERE') #Unblock

Post blog
^^^^^^^^

.. code-block:: python

   import amino
   client = amino.Client()
   email = 'YOUR_EMAIL_HERE'
   password = 'YOUR_PASSWORD_HERE'
   client.login(email=email, password=password)
   subclient = amino.SubClient(comId='YOUR_COMMUNITY_ID_HERE', profile=client.profile)
   subclient.post_blog('TITLE','CONTENT','CATEGORIESLIST','BACKGROUBDCOLOR','IMAGES','FANSONLY')

Edit blog
^^^^^^^^^
.. code-block:: python

   import amino
   client = amino.Client()
   email = 'YOUR_EMAIL_HERE'
   password = 'YOUR_PASSWORD_HERE'
   client.login(email=email, password=password)
   subclient = amino.SubClient(comId='YOUR_COMMUNITY_ID_HERE', profile=client.profile)
   subclient.edit_blog('BLOG_ID','TITLE','BODY','CATEGORIESLIST','BACKGROUBDCOLOR','IMAGES','FANSONLY')

Delete blog
^^^^^^^^^^^

.. code-block:: python

   import amino
   client = amino.Client()
   email = 'YOUR_EMAIL_HERE'
   password = 'YOUR_PASSWORD_HERE'
   client.login(email=email, password=password)
   subclient = amino.SubClient(comId='YOUR_COMMUNITY_ID_HERE', profile=client.profile)
   subclient.delete_blog('BLOG_ID')


Comment blog, wiki, user
^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

   import amino
   client = amino.Client()
   email = 'YOUR_EMAIL_HERE'
   password = 'YOUR_PASSWORD_HERE'
   client.login(email=email, password=password)
   subclient = amino.SubClient(comId='YOUR_COMMUNITY_ID_HERE', profile=client.profile)
   subclient.comment('CONTENT','USER_ID','BLOG_ID','WIKI_ID','REPLYTO','ISGUEST')

Set activity status
^^^^^^^^^^^^^^^^^^^

.. code-block:: python

   import amino
   client = amino.Client()
   email = 'YOUR_EMAIL_HERE'
   password = 'YOUR_PASSWORD_HERE'
   client.login(email=email, password=password)
   subclient = amino.SubClient(comId='YOUR_COMMUNITY_ID_HERE', profile=client.profile)
   subclient.activity_status('number')

| 1 - online
| 2 - offline


Repost blog
^^^^^^^^^^^

.. code-block:: python

   import amino
   client = amino.Client()
   email = 'YOUR_EMAIL_HERE'
   password = 'YOUR_PASSWORD_HERE'
   client.login(email=email, password=password)
   subclient = amino.SubClient(comId='YOUR_COMMUNITY_ID_HERE', profile=client.profile)
   subclient.repost_blog('BLOG_ID','CONTENT')

Discover message id
^^^^^^^^^^^^^^^^^^^
.. code-block:: python

   import amino
   client = amino.Client()
   email = 'YOUR_EMAIL_HERE'
   password = 'YOUR_PASSWORD_HERE'
   client.login(email=email, password=password)
   subclient = amino.SubClient(comId='COMMUNITY_ID', profile=client.profile)
   mesId = subclient.get_chat_messages(chatId='CHAT_ID_HERE',size=1).messageId
   print(mesId)

Delete message
^^^^^^^^^^
.. code-block:: python

   import amino
   client = amino.Client()
   email = 'YOUR_EMAIL_HERE'
   password = 'YOUR_PASSWORD_HERE'
   client.login(email=email, password=password)
   subclient = amino.SubClient(comId='COMMUNITY_ID_HERE', profile=client.profile)
   subclient.delete_message(chatId='CHAT_ID_HERE',messageId='MESSAGE_ID_HERE')

Basic bot v2.1 (easier
^^^^^^^^^^^^^^

.. code-block:: python

   import amino

   client = amino.Client()

   client.login(email="EMAIL_HERE", password="PASSWORD_HERE")

   subclient = amino.SubClient(comId="COMID_HERE", profile=client.profile)

   oldMessages = []

   with open("oldMessages.txt", "r") as oldFile:
      for messageId in oldFile.read().split("\n")[:-1]:
         oldMessages.append(messageId)

   while True:
      readChats = subclient.get_chat_threads().chatId
      
      for chatId in readChats:
         msg = subclient.get_chat_messages(chatId=chatId, size=25)
         for message, messageId, author in zip(msg.content, msg.messageId, msg.author.nickname):
               if not messageId in oldMessages:
                  print(chatId, author, message)
                  
                  # "!ping" comnand
                  if str(message).startswith("!ping"):
                     subclient.send_message(chatId, "Pong!")
               
                  oldMessages.append(messageId)
                  with open("oldMessages.txt", "a") as oldFile:
                     oldFile.write(messageId + "\n")
                     oldFile.close()

Send Images and Audios to a chat
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

   [SEND IMAGES]
   with open("file.png", "rb") as file:
      subclient.send_message(..., file=file)

   [SEND AUDIOS]
   with open("file.mp3", "rb") as file:
      subclient.send_message(..., file=file, fileType="audio")


Discover message's author nickname
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
special thx for code - @Nautic (Nautic#1978)

.. code-block:: python

   subclient = amino.SubClient(comId=communityID, profile=client.profile)
   chatId = 'CHAT_ID_HERE'

   while True:
      readChats = subclient.get_chat_threads().chatId
      
      for chatId in readChats:
         msg = subclient.get_chat_messages(chatId=chatId, size=25)
         for message, messageId, author, authorId in zip(msg.content, msg.messageId, msg.author.nickname, msg.author.userId):
                  Dec=' | '
                  chatTitle=subclient.get_chat_thread(chatId).title
                  print(chatTitle,Dec,author,':',message)

Simple Tutorials
^^^^^^^^^^^^^^^^

🇺🇸 Soon... Maybe
 
| 🇵🇹: Portuguese made by @Lesaninho
| https://www.youtube.com/watch?v=eCvl5Ub7Alg
| https://www.youtube.com/watch?v=BZ8TLqyy5Pk

.. Are these still up to date? I don't speak Portuguese, I'm German.

Simple event example
^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

   @client.event("on_text_message")
   def on_text_message(data):
      print(f"{data.message.author.nickname}: {data.message.content}")

Check for comment bot
^^^^^^^^^^^^^^^^^^^^^
This code will search the list of **recently joined users** and check their **top wall comments**, if it doesn't find the comment **"custom comment"** in the list, it will comment **"custom comment"**

Made by @Standby (Standby#7907)

.. code-block:: python

   import amino
   import time

   client = amino.Client()
   client.login(email="EMAIL_HERE", password="PASSWORD_HERE")
   subclient = amino.SubClient(comId="COMID_HERE", profile=client.profile)
   oldComments = []
   users = subclient.get_all_users()
   for nickname, id in zip(users.profile.nickname, users.profile.userId):
      wallComments = subclient.get_wall_comments(str(id), sorting='top').content

      if "custom comment" not in wallComments:
         oldComments.append(str(id))
         subclient.comment("custom comment", userId=str(id))
         print("Commented on", nickname, str(id))

      time.sleep(10.0)

Clickable message (mentions look-alike)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
This to make those clickable texts like when you mention someone on chat using the app. I'll be inputting screenshots below of its usage, but things to note.

1. This is only for send_message in Client and SubClient
2. Only works if it has at least one user id on the list of mentionUserIds
3. The formatting and index of mentionUserIds will be in order, look at the point 3 in the code if you didn't understood.

Only available for versions 1.2.5 or above

.. code-block:: diff

   ! --2--
   + Works
   message="My Account: <$Click-Me$>!", mentionUserIds=[client.userId]

   - Won't Work
   message="My Account: <$Click-Me$>!"
   message="My Account: <$Click-Me$>!", mentionUserIds=[]

   + --3--
   message="<$User1$>, <$User2$>", mentionUserIds=["id of user 1", "id of user 2"]
   + <$User1$> will be "id of user 1"
   + <$User2$> will be "id of user 2"

.. figure:: _static/images/mentionlookalike.png

Store users when they send a message (Global)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

| This will store all the users into a database, what will be stored?
| 1 - uid : amino id
| 2 - nickname : amino nickname (community)

|
| Make sure to have pymongo installed *and* have a mongodb set up at: https://mongodb.com/ 
| the link should look a bit like this: mongodb://myDBReader:D1fficultP%40ssw0rd@mongodb0.example.com:27017/ 
| make sure to put nothing behind the final / The links can be different for every user.

.. code-block:: python

   import amino
   from pymongo import MongoClient

   #  Make sure to have 'pymongo' installed!

   email = "EMAIL"  # Set your own password here!
   password = "PASSWORD"  # Set your own password here!
   cid = "126936831"  # Community ID
   mongo = MongoClient('MONGOURL')  # Mongo url, example: go to > mongodb.com > create collection > then ONLY get mongodb+srv://DETAILS/
   db = mongo['amino_mongo_test']
   client = amino.Client()
   client.login(email=email, password=password)
   print("Bot logged in")
   sub = amino.SubClient(comId=cid, profile=client.profile)
   print("Bot logged onto the community, id:", cid, "\nBot Name:", sub.profile.nickname)


   @client.callbacks.event("on_text_message")
   def on_text_message(data):
      user = {
         "uid": str(data.message.author.userId),
         "nickname": str(data.message.author.nickname)
      }
      print(data.message.author.userId)
      founduser = db.users.find_one({'uid': data.message.author.userId})
      if founduser is not None:
         updateuser = db.users.update_one({'uid': data.message.author.userId},
                                          {'$set': {'nickname': data.message.author.nickname}})
         resultfind = db.users.find_one({'uid': data.message.author.userId})
         print("User updated!:", resultfind["nickname"])
      else:
         result = db.users.insert_one(user)
         resultfind = db.users.find_one({'uid': data.message.author.userId})
         print("New user stored!:", resultfind["nickname"])

DMs Only Command
^^^^^^^^^^^^^^^^
This command will only work for private messages

.. code-block:: python

   @client.callbacks.event("on_text_message")
   def on_text_message(data: amino.objects.Event):
      content = data.message.content
      chatId = data.message.chatId
      
      chatType = subclient.get_chat_thread(chatId=chatId).type

      if content.lower().startswith("!ping"):
         if chatType == 0:
               subclient.send_message(chatId=chatId, message="Pong!")
         else:
               subclient.send_message(chatId=chatId, message="Command for DMs Only!")

Welcomes new users when they join or leave
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Made by @KIRITO (KIRITO#0001)

.. code-block:: python

   import amino
   import time
   client=amino.Client()
   client.login(email="Your_Email",password="Your_Password")
   community='Your_community_id'
   subclient = amino.SubClient(comId=community , profile=client.profile)

   @client.event("on_group_member_join")
   def on_group_member_join(data):
      if data.comId==community:
         if subclient.get_chat_thread(data.message.chatId).title!=None:
               try:
                  subclient.send_message(chatId=data.message.chatId,message=f"Welcome, <$@{data.message.author.nickname}$> to the group chat.", mentionUserIds=[data.message.author.userId])
                  print(f"\nWelcomed {data.message.author.nickname} in a chatroom ")
               except:
                  print(f"\nWelcomed {data.message.author.nickname} in a chatroom ")

   @client.event("on_group_member_leave")
   def on_group_member_leave(data):
      if data.comId==community:
         if subclient.get_chat_thread(data.message.chatId).title!=None:
               try:
                  subclient.send_message(chatId=data.message.chatId,message="Someone has left the group chat.")
                  print(f"\n{data.message.author.nickname}someone left the chatroom ")
               except:
                  print(f"\n{data.message.author.nickname}someone left the chatroom ")