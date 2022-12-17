.. _data_api:


Data API
========


The data API allows for data to be retrieved/put into the database.
It contains various routes, some of which need to be modified to be game specific.


Installation for Development
----------------------------

Download Node.js `here <https://nodejs.org/en/download/>`_.

Open up the GitHub project `341-data-api <TODO>`_ in `GitHub Desktop <https://desktop.github.com/>`_ for easy version control.

In the app directory, run

.. code-block:: console

   npm install

to install all the packages.


To run the app, run

.. code-block:: console

   node server.js


Components
----------
``server.js``


``POINTS``
^^^^^^^^^^
A dictionary that maps scouted data to point values. This will need to be updated each game

``per_team_helper``
^^^^^^^^^^^^^^^^^^^^
A function that calculates the total points and points per game (stored as the last value in the ``data`` array) of different game metrics.

``getProcessedData``
^^^^^^^^^^^^^^^^^^^^
Function to process data before being sent to the database.


Routes
------

.. note:: 

   A ``:`` means that this is a variable input which is used to process the request.

:file:`/from_comp/:comp` gets all raw data from a certain competition

:file:`/from_comp/:comp/team/:team` gets match data for a certain team at a competition

:file:`/from_comp/:comp/all_teams` gets match data for all teams at a competition as a list of dictionaries ``{team: match_data}``

:file:`/from_comp/:comp/all_teams_arr` gets match data for all teams at a competition as a list of match data, but contains a key ``TEAM`` in each entry

:file:`/from_comp/:comp/pit/:team` gets pit data for a certain team at a competition

:file:`/from_comp/:comp/pit/:team` gets pit data for a certain team at a competition

:file:`/from_comp/:comp/match_predict/:match` gets a match prediction for teams at specific match

:file:`/from_comp/:comp/match_predict_custom/:teams` gets a match prediction for any any number of teams. ``:teams`` should be the in this format: ``1,2,3|4,5,6``, with blue team first and red team after (can be any number on each team).

:file:`/match_fields` gets column info on match database 

:file:`/pit_fields` gets column info on pit database 

:file:`/team_fields` gets column names used in points per game calculations

:file:`/add_pit/:sepBig/:sepSmall/:data` adds a new pit entry to the database. ``sepBig`` seperates multiple entries and ``sepSmall`` splits each entry into columns. ``data`` should use these seperators provided in the route call and follow same order of data as columns in database.

:file:`/add_match/:sepBig/:sepSmall/:data` adds a new match entry to the database. ``sepBig`` seperates multiple entries and ``sepSmall`` splits each entry into columns. ``data`` should use these seperators provided in the route call and follow same order of data as columns in database.


Deployment
----------

Deploy the Node.js API to team server.

.. note::

   Where this is deployed online will need to be updated.
