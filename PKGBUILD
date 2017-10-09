# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: lilydjwg <lilydjwg@gmail.com>

pkgbase=python-cffi
pkgname=(python-cffi python2-cffi)
pkgver=1.11.1
pkgrel=1
pkgdesc="Foreign Function Interface for Python calling C code"
arch=('i686' 'x86_64')
url="http://cffi.readthedocs.org/"
license=('MIT')
makedepends=('python-setuptools' 'python2-setuptools' 'python-pycparser' 'python2-pycparser')
checkdepends=('python-pytest-runner' 'python2-pytest-runner')
source=("$pkgbase-$pkgver.tar.gz::https://bitbucket.org/cffi/cffi/get/v$pkgver.tar.gz")
sha512sums=('808c1ecab11e7d31ea1afbd10b0b985f7c7e9b891af8d738087e15331d401d2b305e3cbe8937ee3c8ae3d6c64e996a7dc6b66033c900b3db1094fe8b7804a2b8')

prepare() {
  mv cffi-cffi-* cffi-$pkgver
  cp -a cffi-$pkgver{,-py2}
}

build() {
  cd "$srcdir"/cffi-$pkgver
  python setup.py build

  cd "$srcdir"/cffi-$pkgver-py2
  python2 setup.py build
}

check() {
  cd "$srcdir"/cffi-$pkgver
  python setup.py pytest

  cd "$srcdir"/cffi-$pkgver-py2
  python2 setup.py pytest
}

package_python-cffi() {
  depends=('python-pycparser')

  cd cffi-$pkgver
  python setup.py install --root="$pkgdir" --optimize=1
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-cffi() {
  depends=('python2-pycparser')

  cd cffi-$pkgver-py2
  python2 setup.py install --root="$pkgdir" --optimize=1
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
