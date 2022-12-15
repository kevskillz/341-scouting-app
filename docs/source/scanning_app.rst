.. _scanning_app:


Scanning App
==========


The scanning app is given to one scout who scans QR codes.
..
   add image of app

After the scouts generate QR codes with the :ref:`tablet_app` and :ref:`master_app.` for both pit and match scouting,
the scanner can push the data to the database when they are connected to the internet.

Installation for Development
----------------------------

To use the tablet app, first install it using pip:

.. code-block:: console

   (.venv) $ pip install lumache


Usage
-----

Test
~~~~


Deployment
----------

To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

