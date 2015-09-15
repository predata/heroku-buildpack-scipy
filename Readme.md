Heroku buildpack: Python, Numpy, and Scipy
====================================================

This is a custom [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks)
for Python apps that use NumPy and/or SciPy, powered by [pip](http://www.pip-installer.org/).

Please open a GitHub for any problems encountered or feature requests.
If are using this project and found it useful, please let me know! (Preferably
by email: brandon.k.liu@gmail.com). I maintain this project on my spare time,
and I am much more motivated to work on it if I know there are people who are
benefiting.

Details
-------

This buildpack currently supports:

NumPy:
  * 1.9.1

SciPy:
  * 0.14.0 (compiled against NumPy 1.9.1)

Note: SciPy should be compiled against the right minor version of NumPy, but
the patch version doesn't matter, e.g., SciPy 0.15.1 can be compiled against
1.9.1 or 1.9.2, but probably not 1.8. I checked every single case though --
you should run tests (`numpy.test()` or `scipy.test()`) if you aren't sure
that things will work.

This package will also install compiled runtime libraries for BLAS, LAPACK,
ATLAS, and Fortran, which are needed by NumPy and SciPy at runtime.

Usage
-----
For a new app:

    heroku create --buildpack https://github.com/predata/heroku-buildpack-scipy

For an existing app:

    heroku config:set BUILDPACK_URL=https://github.com/predata/heroku-buildpack-scipy

You must specify your exact desired version in `requirements.txt` (e.g.,
`numpy==1.9.0`). If no version is specified, the latest version available will
be used. At this time, this buildpack does not support requirements of the
form `numpy>=1.8`.
