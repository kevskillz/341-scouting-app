.. _scanning_app:


Scanning App
============


The scanning app is given to one scout who scans QR codes.

After the scouts generate QR codes with the :ref:`tablet_app` and :ref:`master_app.` for both pit and match scouting,
the scanner can push the data to the database when they are connected to the internet. The scanning app runs on the
browser but does **not** require constant internet access.

Installation for Development
----------------------------


The scanning app uses Flutter. Follow instructions to install it `here <https://docs.flutter.dev/get-started/install/windows>`_.

Set up your VS Code editor to handle Flutter with the instructions provided `here <https://docs.flutter.dev/get-started/editor?tab=vscode>`_.

Open up the GitHub project `341-scouting https://github.com/kevskillz/341-Scouting`_ in `GitHub Desktop <https://desktop.github.com/>`_ for easy version control and open the ``scanning_app`` folder in VS Code.


Deployment
----------

First run

.. code-block:: console

   flutter build web

Then navigate to the ``build/web`` folder generated with the assets folder and deploy it on the team server.

.. note::
   
   Where this is deployed online will need to be updated.

