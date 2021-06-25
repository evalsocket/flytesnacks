Athena
======

Executing Athena Queries
------------------------

Flyte backend can be connected with Athena. Once enabled it can allow you to query a athena service (e.g. Qubole) and retrieve typed schema (optionally).
This section will provide how to use the athena Query Plugin using flytekit python

Installation
------------

To use the ``flytekit-athena`` plugin simply run the following:

.. prompt:: bash

    pip install flytekitplugins-athena


.. NOTE::

    This plugin is purely a spec since SQL is completely portable has no need to build a container, therefore the plugin
    examples do not have an associated Dockerfile.

Configuring the backend to get athena working
---------------------------------------------

.. NOTE::

    Coming soon. 🛠
