# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: lilydjwg <lilydjwg@gmail.com>

_name=cffi
pkgbase=python-$_name
pkgname=(python-$_name python2-$_name)
pkgver=1.0.0
pkgrel=1
pkgdesc="Foreign Function Interface for Python calling C code"
arch=('i686' 'x86_64')
url="http://cffi.readthedocs.org/"
license=('MIT')
makedepends=('python-setuptools' 'python2-setuptools' 'python-pycparser' 'python2-pycparser')
checkdepends=('python-pytest' 'python2-pytest')
source=("https://pypi.python.org/packages/source/c/${_name}/${_name}-${pkgver}.tar.gz")
sha512sums=('07508579d304307531eccb82001011c0a810bb4dc88573420097a4ed22583ba33b43ba203999fe25ab62a28d6e80bd4917e61354ea164794c0f3dfb20d991591')

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
