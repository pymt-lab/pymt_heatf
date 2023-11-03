==========
pymt_heatf
==========

This is an example of building a model,
written in Fortran and wrapped in Python with the `babelizer <https://github.com/csdms/babelizer>`_,
with the `meson-python <https://meson-python.readthedocs.io/en/latest/>`_ build system
using a *pyproject.toml* file to describe the build.

Build/Install
-------------

This is a sketch of how to build and install this project.

With conda
..........

1. Create a conda environment from the *environment.yml* file and activate it
2. Build/install the `Fortran BMI example <https://github.com/csdms/bmi-example-fortran/#buildinstall>`_
3. Build/install this project with:

   .. code-block:: bash

    $ make install

With pip
........

Make, CMake, and a Fortran compiler are required.

1. Create a virtual environment
2. Build/install the `Fortran BMI specification <https://github.com/csdms/bmi-fortran/#buildinstall>`_ (it's not installable through ``pip``)
3. Build/install the `Fortran BMI example <https://github.com/csdms/bmi-example-fortran/#buildinstall>`_
4. Install the build system requirements through ``pip``:

   .. code-block:: bash

    $ pip install meson-python meson ninja cython numpy bmipy

5. Build/install this project with:

   .. code-block:: bash

    $ make install

Use
---

Import the standalone project into a Python session:

.. code-block:: python

    >>> import pymt_heatf

Import the *pymt* component:

.. code-block:: python

    >>> from pymt.MODELS import HeatModelF

Try the examples in the `examples` directory.
