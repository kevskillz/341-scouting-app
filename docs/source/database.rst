.. _database:


Database
========


The database is run on a mySQL server `here <http://mysql.team341.com/>`_ hosted on the team server.

On new seasons, we will have to update the ``MATCH_DATA`` and ``PIT_DATA`` table columns to fit the game.

MATCH_DATA
----------

Keys in order by index: COMP_NAME, MATCH_NUMBER, TEAM

.. note:: 

    Keys eliminate duplicate entries with the same key values.


PIT_DATA
---------

.. note:: 

    `TODO`: Add keys to the table and an IMAGE column which stores encoded pit images.
