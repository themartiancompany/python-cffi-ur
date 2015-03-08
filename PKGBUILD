# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: lilydjwg <lilydjwg@gmail.com>

_name=cffi
pkgbase=python-$_name
pkgname=(python-$_name python2-$_name)
pkgver=0.9.1
pkgrel=1
pkgdesc="Foreign Function Interface for Python calling C code"
arch=('i686' 'x86_64')
url="http://cffi.readthedocs.org/"
license=('MIT')
makedepends=('python-setuptools' 'python2-setuptools' 'python-pycparser' 'python2-pycparser')
checkdepends=('python-pytest' 'python2-pytest')
source=("http://pypi.python.org/packages/source/c/${_name}/${_name}-${pkgver}.tar.gz")
sha512sums=('8eb484256057f6cc6f12030967a433395f6c2570766aa9bfa2bcacd4181ea49e320c51b885a11f3ed85ca4c4dc7cfb939197c1ebc19effd806efbefe630e0259')

prepare() {
  cp -a $_name-$pkgver{,-py2}
}

build() {
  cd "$srcdir/$_name-$pkgver"
  python3 setup.py build

  cd "$srcdir/$_name-$pkgver-py2"
  python2 setup.py build
}

check() {
  cd "$srcdir/$_name-$pkgver"
  PYTHONPATH="$PWD/build/lib.linux-$CARCH-3.4:$PYTHONPATH" py.test

  cd "$srcdir/$_name-$pkgver-py2"
  PYTHONPATH="$PWD/build/lib.linux-$CARCH-2.7:$PYTHONPATH" py.test2
}

package_python-cffi() {
  depends=('python' 'python-pycparser')

  cd "$srcdir/$_name-$pkgver"
  python3 setup.py install --root="$pkgdir/" --optimize=1
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

package_python2-cffi() {
  depends=('python2' 'python2-pycparser')

  cd "$srcdir/$_name-$pkgver-py2"
  python2 setup.py install --root="$pkgdir/" --optimize=1
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
