Python buildpack: Numpy, and Scipy (Python 2.7 only)
====================================================

This is a custom for Python apps that use NumPy and/or SciPy, powered by [pip](http://www.pip-installer.org/).

This is a derivative of [the original](https://github.com/thenovices/heroku-buildpack-scipy), supported versions may diverge over time.

Details
-------

This buildpack currently supports:

NumPy:
  * 1.6.2
  * 1.7.2
  * 1.8.1
  * 1.8.2
  * 1.9.0
  * 1.9.1
  * 1.9.2

SciPy:
  * 0.13.3 (compiled against NumPy 1.9.0)
  * 0.14.0 (compiled against NumPy 1.8.1)
  * 0.15.1 (compiled against NumPy 1.9.2)

Note: SciPy should be compiled against the right minor version of NumPy, but
the patch version doesn't matter, e.g., SciPy 0.15.1 can be compiled against
1.9.0 or 1.9.1, but probably not 1.8. I checked every single case though --
you should run tests (`numpy.test()` or `scipy.test()`) if you aren't sure
that things will work.

This package will also install compiled runtime libraries for BLAS, LAPACK,
ATLAS, and Fortran, which are needed by NumPy and SciPy at runtime.

### Known Issues and Todos

  1. Scikit-learn can be installed, but may not pass all tests. For example, scikit-learn 0.14.1 installed with NumPy 1.9.0 and SciPy 0.13.3 did not pass all tests.
  1. This buildpack may not work well with Multipack apps.
  1. Some minor test failures for NumPy 1.9.2 remain unresolved.
  1. This buildpack currently only works for Python 2.7. .


Usage
-----
##### Pull from Github

Add the following line to your `manifest.yml`

```
buildpack: https://github.com/IBM-Bluemix/python-buildpack-scipy.git
```

##### Create a build pack

See `cf create-buildpack --help` for details.


##### requirements.txt

You must specify your exact desired version in `requirements.txt` (e.g.,
`numpy==1.9.0`). 

If no version is specified, the latest version available will be used. 

At this time, this buildpack does not support requirements of the
form `numpy>=1.8`.


Acknowledgments
---------------

This fork is taken from [@thenovices](https://github.com/thenovices/).
