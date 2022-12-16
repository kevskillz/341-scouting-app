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

Create a :file:`.env` file with the following text: ``TBA_API_KEY=api_key``, with ``api_key`` being replaced with an actual key, which can be obtained `here <https://www.thebluealliance.com/account>`_.

Now try running the app with an Android device selected and it should spring to life!


Components
----------


Global Variables
~~~~~~~~~~~~~~~~
``.env``, ``Globals.dart``

Add variables to :file:`.env` for private constant variables like api keys which requires security.

Add other variables to :file:`Globals.dart` if they need to be accessible throughout the project. These do not have to be constants.

``MATCH_FIELDS`` and ``PIT_FIELDS`` will need to be changed to match the current season's scouting data.


Custom Icons
~~~~~~~~~~~~
``CustomIcons.dart``

Go to `fluttericon <https://www.fluttericon.com/>`_ for custom icons. Select the icons and click download. Make sure to download the icons already in the FlLutter project as 
you can only have one ttf font file. Unzip and find the ``.ttf`` file. Put that under the :file:`fonts` folder in the Flutter project and rename it to :file:`CustomIcons.ttf`. Then go to
the ``.dart`` file downloaded and copy ONLY the IconData objects into :file:`CustomIcons.dart`. 

Example Usage: ``Icon(CustomIcons.robot_arm)`` generates an Icon object with the custom robot arm icon.


Field Info
~~~~~~~~~~
``FieldInfo.dart``

Class to hold formatting and type information for form fields.


Local Data Handler
~~~~~~~~~~~~~~~~~~
``LocalDataHandler.dart``

Contains functions to save data to the tablet locally. Called whenever the data is updated/submitted.

.. warning:: 

   Pit images are **only** saved locally and we will need to develop a way to transfer these images to the database quickly.


Navigation Drawer
~~~~~~~~~~~~~~~~~
``NavigationDrawer.dart``

Creates navigation drawer to switch between pages. To add a new item, add to the ``Wrap`` children in ``buildMenuItems`` like so:

.. code-block:: dart

   ListTile(
          leading: const Icon(Icons.qr_code_2_outlined),
          title: const Text("QR Codes"),
          onTap: () {
            onPageTap?.call();

            Navigator.of(context)
                .pushReplacement(MaterialPageRoute(builder: (ctx) => QRPage()));
          },
   ),

Change the icon, title, and the destination in the ``MaterialPageRoute`` builder. Keep everything else the same.

QR Process
~~~~~~~~~~
``QRProcess.dart``

Contains the ``addEntry`` function which is called whenever a match or pit entry is submitted. Any special processing of certain data types when converting to Strings
should be done inside this for loop:

.. code-block:: dart

   for (String key in arr.keys) {
    if (arr[key] is bool) {
      arr[key] = arr[key] ? '1' : '0';
    } else if (arr[key] is List<dynamic>) {
      arr[key] = arr[key].join(',');
    }
   }


TBA Query
~~~~~~~~~
``TBAQuery.dart``

Contains functions to fetch and handle TBA data. Used to determine which team to scout during matches.


Title Text
~~~~~~~~~~
``TitleTxt.dart``

Wrapper for a generic text object used in form objects.


UI Functions
~~~~~~~~~~~~
``UIFunctions.dart``

Contains the ``showSnackBar`` function to show the bottom black bar with a custom message.
Contains the ``hideKeyboard`` function to force the keyboard to be hidden.


Pages Subfolder
~~~~~~~~~~~~~~~


Config Page
^^^^^^^^^^^
``ConfigPage.dart``


This page manages the configuration of the app. It is the first page the app loads into. The ``initState`` function is first called, so it loads cached data on
the app's first load and notifies the user through the snackbar.

.. note:: 

   Whenever overriding ``initState``, remember to call ``super.initState()``

Add new Widgets to be displayed in the ``build`` function in the children of ``Column``.


Match Page
^^^^^^^^^^^
``MatchPage.dart``

This page manages the match scouting portion of this app. Autonomous and Teleop forms will need to be modified to match the current season's match scouting data.
To modify the forms, go to the ``build`` function and find a ``FormBuilder`` (first one is info, second one is auton, third one is teleop). Modify the Widgets in 
the children under ``Column`` at the respective ``FormBuilder``.

.. important:: 

   Ensure that the id passed in to FormObjects in the form matches the keys defined in ``MATCH_FIELDS``


Pit Page
^^^^^^^^
``PitPage.dart``

This page manages the pit scouting portion of this app. The form will need to be modified to match the current season's pit scouting data.
To modify the forms, go to the ``build`` function and modify the Widgets in the children under ``Column``.

.. important:: 

   Ensure that the id passed in to FormObjects in the form matches the keys defined in ``PIT_FIELDS``


QR Code Page
^^^^^^^^^^^^
``QRPage.dart``

This page displays the QR codes and allows for the modification of data in case of user error, which instantly updates the codes.

Contains ``QRWrapper``, which generates the QR codes and the editing grid.
Contains ``QRCarousel``, which manages multiple ``QRWrapper`` objects and displays them in a carousel.

.. note:: 

   ``QRPage`` is the class which is ultimately displayed.


Picture Page
^^^^^^^^^^^^
``TakePicPage.dart``

This page displays a live camera feed and takes a photo before popping back to the last page. This is only used in the Pit Page.


FormObjects Subfolder
~~~~~~~~~~~~~~~~~~~~


All FormObjects require a label and id. The label is the text which will be displayed to explain the FormObject. The id is what
differentiates FormObjects and should be unique and match what is stored in ``MATCH_FIELDS`` or ``PIT_FIELDS``.

.. note:: 

   In dart, all arguments that are surrounded by {} are **optional** if they are not marked required.

Checkbox
^^^^^^^^
``CheckboxObj.dart``

A simple true or false checkbox.

.. code-block:: dart

   CheckboxObj(
      String label,
      String id,
      {
      final Color checkColor = Colors.white, // color of check
      final Color activeColor = Colors.black // color of checkbox background
      }
   )

Data saved as ``bool``.


Checkbox Group
^^^^^^^^^^^^^^
``CheckboxGroupObj.dart``

A group of chips which allows for **multiple items** to be selected at once.

.. code-block:: dart

   CheckboxGroupObj(
      String label,
      String id,
      List<FormBuilderChipOption> options, // list of selectable checkbox options
      {
      final Color activeColor = Colors.black // color when option is selected
      }
   )

Data saved as ``List<dynamic>``.


Counter
^^^^^^^
``CounterObj.dart``

A counter which has a ``-`` and ``+`` control. It's value can also be edited through the keyboard.

.. code-block:: dart

   CounterObj(
      String label,
      String id,
      {
      final color = Colors.black, // background color of counter
      final arrangement = ButtonArrangement.incRightDecLeft // arrangement of - and + control
      }
   )

Data saved as ``int``.


Radio Group
^^^^^^^^^^^
``RadioGroupObj.dart``

A group of chips which allows for **only one** item to be selected at once.

.. code-block:: dart

   RadioGroupObj(
      String label,
      String id,
      List<FormBuilderChipOption> options, // list of selectable options
      {
      final Color activeColor = Colors.black, // color when option is selected
      Function(dynamic)? onChanged, // callback function which is called when an option is selected
      dynamic initialValue // value to be selected by default
      }
   )

Data saved as ``String``.


SliderObj
^^^^^^^^^
``SliderObj.dart``

A slider with reset and start/stop buttons.

.. code-block:: dart

   SliderObj(
      String label,
      String id,
      final double min, // min value of slider
      final double max, // max value of slider
      {
      final int? discreteDivisions, // number of divisions between min and max, including one for max (set to max - min for steps of 1)
      double? initialVal, // initial value to be set for slider (by default it is min)
      Function(dynamic)? onChanged, // callback function which is called when slider is changed
      }
   )

Data saved as ``double``.


Stopwatch
^^^^^^^^^
``StopwatchObj.dart``

A stopwatch with reset and start/stop buttons.

.. code-block:: dart

   StopwatchObj(
      String label,
      String id,
      GlobalKey<FormBuilderState> curKey, // the key used in page which manages the form state
      {
      bool enabled = true, // whether the stopwatch can be used 
      Stream<bool>? enabledController // a stream which can change the enabled state of the stopwatch (true = enabled, false = disabled)
      }
   )

Data saved as ``String`` (# of seconds formatted to 2 decimal places).


Switch
^^^^^^
``SwitchObj.dart``

A simple switch which can be toggled on and off.

.. code-block:: dart

   SwitchObj(
      String label,
      String id,
      {
      final Color activeColor = Colors.black, // color of the switch track when set to on
      final Color inactiveColor = Colors.white, // color of the switch track when set to off
      final Color activeColorCircle = const Color.fromARGB(255, 189, 189, 189), // color of the switch circle when set to on
      final Color inactiveColorCircle = Colors.black87, // color of the switch circle when set to off
      final bool enabled = true, // whether the switch can be updated
      final Function(bool?)? onChanged // callback function which is called when switch is toggled
      }
   )

Data saved as ``bool``.


Text Field
^^^^^^^^^^
``TextFieldObj.dart``

.. code-block:: dart

   TextFieldObj(
      String label,
      String id,
      FieldInfo typeRestrictions, // used to determine type of keyboard to display and what inputs are allowed
      {
      Function(dynamic)? onChanged, // callback function which is called when field is updated
      String? initalValue, // initial text in field 
      double? fontSize = TitleTxt.FONT_SIZE, // font size of text
      TextEditingController? controller // can update the text of the field programatically without calling setState with a controller
      }
   )

Data saved as ``String``.


Deployment
----------

To deploy the app, connect to the Kindle and select it as the primary device in your VS Code Flutter project by clicking on the device panel on the bottom right.

Then run the following command in the terminal at the root directory of the project.

.. code-block:: console

   flutter run --release

The --release flag is required as Flutter runs everything in debug mode by default.
