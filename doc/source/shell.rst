The :program:`gnocchi` shell utility
=========================================

.. program:: gnocchi
.. highlight:: bash

The :program:`gnocchi` shell utility interacts with Gnocchi API
from the command line. It supports the entirety of the Gnocchi API.

You'll need to provide :program:`gnocchi` with your OpenStack credentials.
You can do this with the :option:`--os-username`, :option:`--os-password`,
:option:`--os-tenant-id` and :option:`--os-auth-url` options, but it's easier to
just set them as environment variables:

.. envvar:: OS_USERNAME

    Your OpenStack username.

.. envvar:: OS_PASSWORD

    Your password.

.. envvar:: OS_TENANT_NAME

    Project to work on.

.. envvar:: OS_AUTH_URL

    The OpenStack auth server URL (keystone).

For example, in Bash you would use::

    export OS_USERNAME=user
    export OS_PASSWORD=pass
    export OS_TENANT_NAME=myproject
    export OS_AUTH_URL=http://auth.example.com:5000/v2.0

The command line tool will attempt to reauthenticate using your provided credentials
for every request. You can override this behavior by manually supplying an auth
token using :option:`--os-gnocchi-url` and :option:`--os-auth-token`. You can alternatively
set these environment variables::

    export GNOCCHI_ENDPOINT=http://gnocchi.example.org:8041
    export OS_AUTH_TOKEN=3bcc3d3a03f44e3d8377f9247b0ad155

From there, all shell commands take the form::

    gnocchi <command> [arguments...]

Run :program:`gnocchi help` to get a full list of all possible commands,
and run :program:`gnocchi help <command>` to get detailed help for that
command.

Examples
--------

Create a resource::

    gnocch resource create instance --attribute id:5a301761-f78b-46e2-8900-8b4f6fe6675a --attribute project_id:eba5c38f-c3dd-4d9c-9235-32d430471f94 --metric temperature:high

List resources::

    gnocchi resource list instance

Search of resources::

    gnocchi resource search -q "project_id=5a301761-f78b-46e2-8900-8b4f6fe6675a and not (name like '%foobar%' or name='my_resource')"