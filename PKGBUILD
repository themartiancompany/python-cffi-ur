# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: lilydjwg <lilydjwg@gmail.com>

pkgbase=python-cffi
pkgname=(python-cffi python2-cffi)
pkgver=1.7.0
_revision=338244197c0dd4afcf76a7dbf962e70fb95b8044
pkgrel=1
pkgdesc="Foreign Function Interface for Python calling C code"
arch=('i686' 'x86_64')
url="http://cffi.readthedocs.org/"
license=('MIT')
makedepends=('python-setuptools' 'python2-setuptools' 'python-pycparser' 'python2-pycparser' 'mercurial')
checkdepends=('python-pytest-runner' 'python2-pytest-runner')
source=("hg+https://bitbucket.org/cffi/cffi#revision=$_revision")
sha512sums=('SKIP')

prepare() {
  cp -a cffi{,-py2}
}

build() {
  cd "$srcdir"/cffi
  python3 setup.py build

  cd "$srcdir"/cffi-py2
  python2 setup.py build
}

check() {
  cd "$srcdir"/cffi
  python3 setup.py ptr

  cd "$srcdir"/cffi-py2
  python2 setup.py ptr
}

package_python-cffi() {
  depends=('python-pycparser')

  cd cffi
  python3 setup.py install --root="$pkgdir" --optimize=1
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-cffi() {
  depends=('python2-pycparser')

  cd cffi-py2
  python2 setup.py install --root="$pkgdir" --optimize=1
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
