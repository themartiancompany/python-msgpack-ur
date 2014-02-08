# Maintainer: Sébastien "Seblu" Luttringer

pkgbase=python-msgpack
pkgname=('python-msgpack' 'python2-msgpack')
pkgver=0.4.0
pkgrel=1
arch=('i686' 'x86_64')
url='https://github.com/msgpack/msgpack-python'
license=('Apache')
makedepends=('cython' 'cython2' 'python-distribute' 'python2-distribute')
checkdepends=('python-pytest' 'python2-pytest' 'python-six' 'python2-six')
source=("http://pypi.python.org/packages/source/m/msgpack-python/msgpack-python-$pkgver.tar.gz")
md5sums=('8b9ce43619fd1428bf7baddf57e38d1a')

build() {
  cd msgpack-python-$pkgver
  python setup.py build --build-lib=build/python
  python2 setup.py build --build-lib=build/python2
  find build/python2 -type f -exec \
    sed -i '1s,^#! \?/usr/bin/\(env \|\)python$,#!/usr/bin/python2,' {} \;
}

check() {
  cd msgpack-python-$pkgver
  msg2 'python'
  PYTHONPATH=$PWD/build/python py.test test
  msg2 'python2'
  PYTHONPATH=$PWD/build/python2 py.test2 test
}

package_python-msgpack() {
  pkgdesc='MessagePack serializer implementation for Python'
  depends=('python')

  cd msgpack-python-$pkgver
  python setup.py build --build-lib=build/python \
                  install --root="$pkgdir" --optimize=1
}

package_python2-msgpack() {
  pkgdesc='MessagePack serializer implementation for Python2'
  depends=('python2')

  cd msgpack-python-$pkgver
  python2 setup.py build --build-lib=build/python2 \
                   install --root="$pkgdir" --optimize=1
}

# vim:set ts=2 sw=2 et:
