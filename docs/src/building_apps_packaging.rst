.. _building_apps_packaging:

Running ``tcpackage`` will build a zip package of your App that can be installed directly in the ThreatConnect Platform.  For Apps packages that contain multiple Apps using separate **install.json** files add the ``--bundle`` argument to build a bundle.  When using multiple **install.json** files the prefix of the filename is the App name (e.g. MyApp.install.json will have an App name of **MyApp**).  During the build process validation of the **install.json** file will be handled automatically if the **tcex_json_schema.json** schema file is included in the base directory of your App.

.. Note:: Typically the ``tcpackage`` command would be run with no arguments or using the ``--bundle`` flag for packages with multiple install.json files. Optionally a **package** configuration parameter can be added to the configuration file to provide additional functionality.

Usage
-----

.. code:: bash

    usage: tcpackage [-h] [--bundle] [--exclude EXCLUDE] [--config CONFIG]
                     [--install_json INSTALL_JSON] [--outdir OUTDIR]

    optional arguments:
      -h, --help            show this help message and exit
      --bundle              Build a bundle file.
      --exclude EXCLUDE     File and directories to exclude from build.
      --config CONFIG       Build configuration file (Default: tcex.json).
      --install_json INSTALL_JSON
                            The install.json file name for the App that should be
                            built.
      --outdir OUTDIR       Directory to write the outfile (Default: target)

Configuration Options
---------------------
By default the ``tcex.json`` file will be loaded by ``tcpackage``.  The following is an example of additiona configuration that can be provided for the ``tcpackage`` command.

.. code:: javascript

  <..snipped>
  "package": {
    "bundle": true,
    "bundle_name": "TCPB_-_My_Bundle",
    "excludes": [
      "log",
      "requirements.txt",
      "tcex.d"
    ],
    "outdir": "target"
  },
  <snipped..>

**Multiple Bundles**

.. code:: javascript

  <..snipped>
  "package": {
    "bundle": true,
    "bundle_name": "TCPB_-_Palo_Alto",
    "bundle_packages": [{
      "name": "TCPB_-_My_Bundle_Create",
      "patterns": [
        ".*Create.*"
      ]
    },
    {
      "name": "TCPB_-_My_Bundle_Delete",
      "patterns": [
        ".*Delete.*"
      ]
    }],
    "excludes": [
      "log",
      "requirements.txt",
      "tcex.d"
    ],
    "outdir": "target"
  },
  <snipped..>