LightGBM Python-package
=======================

|License| |Python Versions| |PyPI Version|

Installation
------------

Preparation
'''''''''''

32-bit Python is not supported. Please install 64-bit version.

`setuptools <https://pypi.org/project/setuptools>`_ is needed.

Install from `PyPI <https://pypi.org/project/lightgbm>`_ Using ``pip``
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

For **Windows** users, `VC runtime <https://go.microsoft.com/fwlink/?LinkId=746572>`_ is needed if **Visual Studio** (2015 or 2017) is not installed.

For **Linux** users, **glibc** >= 2.14 is required.

For **macOS** users:

- Starting from version 2.2.1, the library file in distribution wheels is built by the **Apple Clang** (Xcode_8.3.1) compiler. This means that you don't need to install the **gcc** compiler anymore. Instead of that you need to install the **OpenMP** library, which is required for running LightGBM on the system with the **Apple Clang** compiler. You can install the **OpenMP** library by the following command: ``brew install libomp``.

- For version smaller than 2.2.1 and not smaller than 2.1.2, **gcc-8** with **OpenMP** support must be installed first. Refer to `Installation Guide <https://github.com/Microsoft/LightGBM/blob/master/docs/Installation-Guide.rst#gcc>`__ for installation of **gcc-8** with **OpenMP** support.

- For version smaller than 2.1.2, **gcc-7** with **OpenMP** is required.

Install `wheel <http://pythonwheels.com>`_ via ``pip install wheel`` first. After that download the wheel file and install from it:

.. code:: sh

    pip install lightgbm

Build from Sources
******************

.. code:: sh

    pip install --no-binary :all: lightgbm

For **Linux** and **macOS** users, installation from sources requires installed `CMake`_.

For **macOS** users, you can perform installation either with **Apple Clang** or **gcc**. In case you prefer **Apple Clang**, you should install **OpenMP** (details for installation can be found in `Installation Guide <https://github.com/Microsoft/LightGBM/blob/master/docs/Installation-Guide.rst#apple-clang>`__) first and **CMake** version 3.12 or higher is required. In case you prefer **gcc**, you need to install it (details for installation can be found in `Installation Guide <https://github.com/Microsoft/LightGBM/blob/master/docs/Installation-Guide.rst#gcc>`__) and specify compilers by running ``export CXX=g++-7 CC=gcc-7`` (replace "7" with version of **gcc** installed on your machine) first.

For **Windows** users, **Visual Studio** (or `VS Build Tools <https://visualstudio.microsoft.com/downloads/>`_) is needed. If you get any errors during installation, you may need to install `CMake`_ (version 3.8 or higher).

Build MPI Version
~~~~~~~~~~~~~~~~~

.. code:: sh

    pip install lightgbm --install-option=--mpi

All remarks from `Build from Sources section <#build-from-sources>`__ are actual in this case.

For **Windows** users, compilation with **MinGW-w64** is not supported and `CMake`_ (version 3.8 or higher) is strongly required.

**MPI** libraries are needed: details for installation can be found in `Installation Guide <https://github.com/Microsoft/LightGBM/blob/master/docs/Installation-Guide.rst#build-mpi-version>`__.

Build GPU Version
~~~~~~~~~~~~~~~~~

.. code:: sh

    pip install lightgbm --install-option=--gpu

All remarks from `Build from Sources section <#build-from-sources>`__ are actual in this case.

For **Windows** users, `CMake`_ (version 3.8 or higher) is strongly required.

**Boost** and **OpenCL** are needed: details for installation can be found in `Installation Guide <https://github.com/Microsoft/LightGBM/blob/master/docs/Installation-Guide.rst#build-gpu-version>`__. You need to add ``OpenCL_INCLUDE_DIR`` to the environmental variable **'PATH'** and export ``BOOST_ROOT`` before installation. Alternatively, you may pass options to **CMake** via ``pip`` options, like

.. code:: sh

    pip install lightgbm --install-option=--gpu --install-option="--opencl-include-dir=/usr/local/cuda/include/" --install-option="--opencl-library=/usr/local/cuda/lib64/libOpenCL.so"

All available options:

- boost-root

- boost-dir

- boost-include-dir

- boost-librarydir

- opencl-include-dir

- opencl-library

For more details see `FindBoost <https://cmake.org/cmake/help/v3.8/module/FindBoost.html>`__ and `FindOpenCL <https://cmake.org/cmake/help/v3.8/module/FindOpenCL.html>`__.

Build HDFS Version
~~~~~~~~~~~~~~~~~~

.. code:: sh

    pip install lightgbm --install-option=--hdfs

Note that the installation process of HDFS version is **untested**.

Build with MinGW-w64 on Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: sh

    pip install lightgbm --install-option=--mingw

`CMake`_ and `MinGW-w64 <https://mingw-w64.org/>`_ should be installed first.

It is recommended to use **Visual Studio** for its better multithreading efficiency in **Windows** for many-core systems (see `FAQ <https://github.com/Microsoft/LightGBM/blob/master/docs/FAQ.rst#lightgbm>`__ Question 4 and Question 8).

Install from GitHub
'''''''''''''''''''

All remarks from `Build from Sources section <#build-from-sources>`__ are actual in this case.

For **Windows** users, if you get any errors during installation and there is the warning ``WARNING:LightGBM:Compilation with MSBuild from existing solution file failed.`` in the log, you should install `CMake`_ (version 3.8 or higher).

.. code:: sh

    git clone --recursive https://github.com/Microsoft/LightGBM.git
    cd LightGBM/python-package
    # export CXX=g++-7 CC=gcc-7  # macOS users, if you decided to compile with gcc, don't forget to specify compilers (replace "7" with version of gcc installed on your machine)
    python setup.py install

Note: ``sudo`` (or administrator rights in **Windows**) may be needed to perform the command.

Run ``python setup.py install --mpi`` to enable **MPI** support. All remarks from `Build MPI Version section <#build-mpi-version>`__ are actual in this case.

Run ``python setup.py install --mingw``, if you want to use **MinGW-w64** on **Windows** instead of **Visual Studio**. All remarks from `Build with MinGW-w64 on Windows section <#build-with-mingw-w64-on-windows>`__ are actual in this case.

Run ``python setup.py install --gpu`` to enable GPU support. All remarks from `Build GPU Version section <#build-gpu-version>`__ are actual in this case. To pass additional options to **CMake** use the following syntax: ``python setup.py install --gpu --opencl-include-dir=/usr/local/cuda/include/``, see `Build GPU Version section <#build-gpu-version>`__ for the complete list of them.

Run ``python setup.py install --hdfs`` to enable HDFS support. All remarks from `Build HDFS Version section <#build-hdfs-version>`__ are actual in this case.

If you get any errors during installation or due to any other reasons, you may want to build dynamic library from sources by any method you prefer (see `Installation Guide <https://github.com/Microsoft/LightGBM/blob/master/docs/Installation-Guide.rst>`__) and then just run ``python setup.py install --precompile``.

Troubleshooting
---------------

In case you are facing any errors during the installation process, you can examine ``$HOME/LightGBM_compilation.log`` file, in which all operations are logged, to get more details about occurred problem. Also, please attach this file to the issue on GitHub to help faster indicate the cause of the error.

Refer to `FAQ <https://github.com/Microsoft/LightGBM/tree/master/docs/FAQ.rst>`_.

Examples
--------

Refer to the walk through examples in `Python guide folder <https://github.com/Microsoft/LightGBM/tree/master/examples/python-guide>`_.

Developments
------------

The code style of Python-package follows `PEP 8 <https://www.python.org/dev/peps/pep-0008/>`_. If you would like to make a contribution and not familiar with PEP 8, please check the PEP 8 style guide first. Otherwise, the check won't pass. You should be careful about:

- E1 Indentation (check PEP 8 link above)
- E202 whitespace before and after brackets
- E225 missing whitespace around operator
- E226 missing whitespace around arithmetic operator
- E261 at least two spaces before inline comment
- E301 expected 1 blank line in front of and at the end of a method
- E302 expected 2 blank lines in front of and at the end of a function or a class

E501 (line too long) and W503 (line break occurred before a binary operator) can be ignored.

.. |License| image:: https://img.shields.io/badge/license-MIT-blue.svg
   :target: https://github.com/Microsoft/LightGBM/blob/master/LICENSE
.. |Python Versions| image:: https://img.shields.io/pypi/pyversions/lightgbm.svg
   :target: https://pypi.org/project/lightgbm
.. |PyPI Version| image:: https://img.shields.io/pypi/v/lightgbm.svg
   :target: https://pypi.org/project/lightgbm

.. _CMake: https://cmake.org/
