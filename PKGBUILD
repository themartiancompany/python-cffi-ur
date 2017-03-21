# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: lilydjwg <lilydjwg@gmail.com>

pkgbase=python-cffi
pkgname=(python-cffi python2-cffi)
pkgver=1.10.0
_revision=486d919c0b87288ec93c7696f75e2105ed4a91fd
pkgrel=1
pkgdesc="Foreign Function Interface for Python calling C code"
arch=('i686' 'x86_64')
url="http://cffi.readthedocs.org/"
license=('MIT')
makedepends=('python-setuptools' 'python2-setuptools' 'python-pycparser' 'python2-pycparser')
checkdepends=('python-pytest-runner' 'python2-pytest-runner')
source=("$pkgbase-$pkgver.tar.gz::https://bitbucket.org/cffi/cffi/get/$_revision.tar.gz")
sha512sums=('5c48f27bdca1568e60ba425f90603ca413b1ea095a83ecc3da073e937c044efd204620fba25d204a9db65d6dfde8cb37a990a347a1816a09e7248733e6f142b3')

prepare() {
  cp -a cffi-cffi-${_revision::12}{,-py2}
}

build() {
  cd "$srcdir"/cffi-cffi-${_revision::12}
  python setup.py build

  cd "$srcdir"/cffi-cffi-${_revision::12}-py2
  python2 setup.py build
}

check() {
  cd "$srcdir"/cffi-cffi-${_revision::12}
  python setup.py pytest

  cd "$srcdir"/cffi-cffi-${_revision::12}-py2
  python2 setup.py pytest
}

package_python-cffi() {
  depends=('python-pycparser')

  cd cffi-cffi-${_revision::12}
  python setup.py install --root="$pkgdir" --optimize=1
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-cffi() {
  depends=('python2-pycparser')

  cd cffi-cffi-${_revision::12}-py2
  python2 setup.py install --root="$pkgdir" --optimize=1
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
