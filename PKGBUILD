# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Johannes Löthberg <johannes@kyriasis.com>
# Contributor: Sébastien "Seblu" Luttringer

_py=python
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pkg=msgpack
_pkgname="${_pkg}-${_py}"
pkgname="${_py}-${_pkg}"
pkgver=1.0.5
pkgrel=2
pkgdesc='MessagePack serializer implementation for Python'
_http="https://github.com"
_ns="${_pkg}"
url="${_http}/${_ns}/${_pkgname}"
arch=(
  'x86_64'
  'i686'
  'pentium4'
  'arm'
  'armv7l'
  'aarch64'
  'mips'
  'powerpc'
)
license=(
  'Apache-2.0'
)
depends=(
  "${_py}>=${_pymajver}"
)
makedepends=(
  'cython'
  "${_py}-setuptools"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-pytest"
)

source=(
  "${_pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz"
)
sha512sums=(
  '0d0b479044cda16519cf85d45acb8900b6e6585bf95816396fc96d6d1eb260036fb9c75bf8f88d99e212937a40d314a200d2b847d1da8a9ebc5694ab52e22896'
)

prepare() {
  sed \
    -i \
    's/~=/>=/' \
    "${_pkgname}-${pkgver}/pyproject.toml"
}

build() {
  cd \
    "${_pkgname}-${pkgver}"
  python \
    -m build \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${_pkgname}-${pkgver}"
  PYTHONDONTWRITEBYTECODE=1 \
  PYTHONPATH="$( \
    printf \
      '%s\n' \
      "${PWD}/build/"* | \
      paste \
        -sd:)" \
  py.test \
    test
}

package() {
  cd \
    "${_pkgname}-${pkgver}"
  python \
    -m installer \
    --destdir="${pkgdir}" \
    dist/*.whl
}

# vim:set ts=2 sw=2 et:
