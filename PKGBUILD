# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: lilydjwg <lilydjwg@gmail.com>

pkgname=python-cffi
pkgver=1.16.0
pkgrel=2
pkgdesc="Foreign Function Interface for Python calling C code"
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'mips'
  'i686'
  'powerpc'
  'pentium4'
)
url="https://cffi.readthedocs.org/"
license=(
  'MIT'
)
depends=(
  'python-pycparser'
)
optdepends=(
  'python-setuptools: "limited api" version checking in cffi.setuptools_ext'
)
makedepends=(
  'python-build'
  'python-installer'
  'python-setuptools'
  'python-wheel')
checkdepends=(
  'python-pytest'
)
source=(
  "https://github.com/python-cffi/cffi/archive/v$pkgver/$pkgname-$pkgver.tar.gz"
)
sha512sums=(
  '2115f4d2431f36b18494182d2abb378a750c970dfdf083cfc287b004e52830efe703f07f71a17c89060b47eaa3b52e7b2390017d1980eb39695bdaf31bac3bb5'
)

build() {
  cd \
    cffi-$pkgver
  python \
    -m \
      build \
    -nw
}

check() {
  cd \
    cffi-$pkgver
  python \
    -m \
      installer \
    --destdir=tmpinstall \
    dist/*.whl
  local \
    python_version=$( \
      python \
        -c \
	  'import sys; print(".".join(map(str, sys.version_info[:2])))')
  PYTHONPATH="$PWD/tmpinstall/usr/lib/python${python_version}/site-packages" \
  pytest
}

package() {
  cd \
    cffi-$pkgver
  # remove files created during check()
  # for reproducible SOURCES.txt
  rm \
    -rf \
    testing/cffi{0,1}/__pycache__/
  python \
    -m installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm644 \
    LICENSE \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}

