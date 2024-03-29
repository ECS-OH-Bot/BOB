.. |DiscordLogo| image:: https://img.icons8.com/color/48/000000/discord-logo.png
   :target: https://discordapp.com

|DiscordLogo| BOB
======================================

The "Better" Office Hours Bot
------------------------------

.. raw:: html

   <p align=center style="font-size:large">
      <a href=#purpose>Purpose</a> • 
      <a href=#overview>Overview</a> • 
      <a href=#quickstart>Quick Start</a> • 
      <a href=https://ecs-oh-bot.github.io/OH-Bot/docs/build/html/index.html>Docs</a> •
      <a href=#license>License</a>
   </p>
.. raw:: html

   </p>

Purpose
-------

With the need for online learning becoming increasingly higher,
efficient means of reaching educators has become extremely important. We
implemented a discord bot to help instructors automate the process of
their Office Hours through Discord.

We created this bot with the goal of allowing students to effectively
communicate with their instructors, with the option to be able to ask
their peers for help while they wait.

Overview
--------

**BOB** is a server managment automation bot. This means that tasks
like queue management and notifying students are
handled by **BOB**

**BOB** is a *self-hotsted* bot - meaning that you will need to host
and maintain your own instance. See `Quick Start <#quickstart>`__ to
get started.

The standard OH-Session protocol that we follow: 

> Helpers refer to Instructors, TAs, and Tutors

#. Helpers Opens Queues for which they help for
#. Students enter the queue of their choice
#. Helpers issues a dequeue command
#. Helpers close their queues when their OH-Session is over
#. Multiple Helpers can help for the same queue. A Queue will only
   close if there are no helpers for that queue.

Waiting Queue System
--------------------

**BOB** implements a simple *first come first serve* queue where
student are allowed to enter and leave the queue whenever they like
while OH is being held.

Server Template: **TODO**
------------------------------------------------------

**BOB** makes use of Discord’s Server Template feature

There are three roles in the **BOB** server

-  Admin - total control of bot functionality and server interfaces
-  Instructor - control over OH sessions and locked channels
-  Student - ability to interface with OH-Queue

Commands
~~~~~~~~

**BOB** commands have access level based on sender roles

-  ``/start`` - Access Role: [Admin, Helper]

   -  Open queues that the Helper is assigned to help for

-  ``/stop`` - Access Role: [Admin, Helper]

   -  Close the OH-queue, stop students from entering the queue
   -  Students that were in the queue before closing will still be
      regisitered for OH

-  ``/clear (queue_name) (all)`` - Access Role: [Admin, Helper]

   -  Empties a queue of students
   -  Option ``queue_name`` : Clears only the queue ``queue_name``
   -  Option ``all`` : Clears all queues

-  ``/enqueue [queue_name] (user)`` - Access Role: [Admin, Helper, Student]

   -  Adds sender to the back of the queue ``queue_name``
   -  Option ``user`` : Adds ``user`` to the end of the queue ``queue_name``. Access Role: [Admin, Helper]

-  ``/leave`` - Access Role: [Admin, Helper, Student]

   -  Removes sender from the queue in which they are in

-  ``/next (queue_name) (user)`` - Access Role: [Admin, Helper]

   -  Removes next student from the sender's queue(s) and sends them 
      an invite to the voice channel.
   -  Option ``queue_name`` : Removes a student from a particular queue
   -  Option ``user`` : Removes a particular user from the queue(s)

-  ``/announce [message] (queue_name)`` - Access Role: [Admin, Helper]

   - Sends a messeage ``message`` to all of the students in the sender's queues
   - Option ``queue_name``: Sends the message to only those in ``queue_name``

-  ``/list-helpers`` - Access Role: [Admin, Helper, Student]

   -  Shows a list of Helpers that are currently helping, the queues 
      for which they help for and how long it's been since they
      started helping

-  ``/queue add [queue_name]`` - Access Role: [Admin]

   - Creates a new category with the name ``queue_name`` and creates a #queue and #chat text channels within it

-  ``/queue remove [queue_name]`` - Access Role: [Admin]

   - Deletes the category with the name ``queue_name``, if it exists, and the channels within it

Requirements
------------

-  `Git <https://git-scm.com/>`__ (Optional if using packaged release)
-  `Node.js (includes npm) <https://nodejs.org/en/download/>`__ 

-  `Discord <https://discordapp.com/>`__ app & account
- `Google Cloud `__ account & service account

Quick Start
--------------------------

Instantiate an instance of a server in Discord 


Follow discord.py `docs <https://discordpy.readthedocs.io/en/latest/discord.html>`__ on creating and adding a bot to your server.

Clone the source code

.. code:: bash

   git clone https://github.com/ECS-OH-Bot/BOB && cd BOB

Follow the instructions
`here <https://discordpy.readthedocs.io/en/v1.3.3/discord.html#creating-a-bot-account>`__
for obtaining a token for your instance of the Bot

Make a ``.env`` file in the current directory with the following format:

.. code:: 

   BOB_GOOGLE_SHEET_ID=[Insert Google Sheets Token ID here]
   BOB_APP_ID=[Insert Discord Application ID here]
   BOB_BOT_TOKEN=[Insert Discord BOT Token here]

Also create a .json file in the current directory named ``gcs_service_account_key.json`` which you get get from the Google Cloud website

Run the following command to setup the bot locally

.. code:: bash

   npm run build

If the build succeeds, run the next command to run the bot

.. code:: bash

   npm run start

``npm run test`` and ``npm run lint`` are also available. run ``npm run`` at anytime to view the available npm commands

Adjust the role hierarchy.

For security/privacy purposes, bot/scripts are not allowed to adjust themselves upward the role hierarchy. This must be done by hand to allow features of the bot.

.. image:: ./assets/adjustRole.gif

Run the script to start up the bot

.. code:: bash

   ./run{ENV_FILE_NAME}.sh

`Docs <https://ecs-oh-bot.github.io/OH-Bot/docs/build/html/index.html>`__
=========================================================================

License
-------

Released under the `GNU GPL
v3 <https://www.gnu.org/licenses/gpl-3.0.en.html>`__ license.

``Copyright (C) 2020  Grant Gilson, Noah Rose Ledesma, Stephen Ott``
