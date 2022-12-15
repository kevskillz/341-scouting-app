.. _tablet_app:


Tablet App
==========


The tablet app is given to six scouts during matches and while pit scouting.
..
   add image of app

After the scouts fill out the data, QR codes are generated which are scanned by the :ref:`scanning_app`.

Installation for Development
----------------------------

The tablet app uses Flutter. Follow instructions to install it `here <https://docs.flutter.dev/get-started/install/windows>`_.

Since the app runs on android, follow the instructions to set up Android support `here <https://docs.flutter.dev/get-started/install/windows>`_. During development,
a Kindle will likely be plugged in to test code, but installing an emulator like the instructions suggest doesn't hurt.

Set up your VS Code editor to handle Flutter with the instructions provided `here <https://docs.flutter.dev/get-started/editor?tab=vscode>`_.

Open up the GitHub project `341-tablet-app <TODO>`_ in `GitHub Desktop <https://desktop.github.com/>`_ for easy version control.

Create a `.env` file with the following text: `TBA_API_KEY=api_key`, with `api_key` being replaced with an actual key, which can be obtained `here <https://www.thebluealliance.com/account>`_.

Now try running the app with an Android device selected and it should spring to life!


Components
----------

Global Variables
~~~~~~~~~~~~~~~~

Add variables to `.env` for private constant variables like api keys which requires security.

Add other variables to `Globals.dart` if they need to be accessible throughout the project. These do not have to be constants.


Custom Icons
~~~~~~~~~~~~


Go to `fluttericon <https://www.fluttericon.com/>`_ for custom icons. Select the icons and click download. Make sure to download the icons already in the FLutter project as 
you can only have one ttf font file. Unzip and find the ``.ttf`` file. Put that under the `/fonts` folder in the Flutter project and rename it to :file:`CustomIcons.ttf`. Then go to
the ``.dart`` file downloaded and copy ONLY the IconData objects into :file:`CustomIcons.dart`. 

Example Usage: ``Icon(CustomIcons.robot_arm)`` generates an Icon object with the custom robot arm icon.

Field Info
~~~~~~~~~~

Class to hold formatting and type information for form fields.

Local Data Handler
~~~~~~~~~~~~~~~~~~

:file:`Global.dart` for .
:file:`.env` for private constant variables like api keys which requires security.

Navigation Drawer
~~~~~~~~~~~~~~~~~

`Global.dart` for .
`.env` for private constant variables like api keys which requires security.

QR Process
~~~~~~~~~~


TBA Query
~~~~~~~~~



UI Functions
~~~~~~~~~~~~


Pages Subfolder
~~~~~~~~~~~~~~~

Config Page
^^^^^^^^^^^

Match Page
^^^^^^^^^^^

Pit Page
^^^^^^^^^^^

QR Code Page
^^^^^^^^^^^

Picture Page
^^^^^^^^^^^


FormObjects Subfolder
~~~~~~~~~~~~~~~~~~~~

Checkbox
^^^^^^^^

Checkbox Group
^^^^^^^^^^^^^^

Counter
^^^^^^^

Radio Group
^^^^^^^^^^^

Stopwatch
^^^^^^^^^

Switch
^^^^^^

Text Field
^^^^^^^^^^


Title Text
^^^^^^^^^^
Wrapper for a generic text object used in form objects.




Deployment
----------

To deploy the app, connect to the Kindle and select it as the primary device in your VS Code Flutter project by clicking on the device panel on the bottom right.

Then run the following command in the terminal at the root directory of the project.

.. code-block:: console

   flutter run --release

The --release flag is required as Flutter runs everything in debug mode by default.
