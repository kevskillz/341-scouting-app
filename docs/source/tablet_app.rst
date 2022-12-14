.. _tablet_app:


Tablet App
==========


The tablet app is given to six scouts during matches and while pit scouting.
..
   add image of app

After the scouts fill out the data, QR codes are generated which are scanned by the :ref:`scanning_app`.

Installation for Development
----------------------------

To use the tablet app, first install it using pip:

.. code-block:: console

   (.venv) $ pip install lumache



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

