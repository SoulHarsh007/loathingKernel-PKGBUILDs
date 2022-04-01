_pkgname='pathvalidate'
pkgname=python-$_pkgname
pkgver=2.5.0
pkgrel=1
pkgdesc='Sanitize/validate strings in filenames/file-paths/etc'
arch=('any')
url='https://github.com/thombashi/pathvalidate'
license=('MIT')
depends=('python')
makedepends=('python-setuptools')
source=("$pkgname-$pkgver.tar.gz::https://github.com/thombashi/pathvalidate/archive/v$pkgver.tar.gz")
sha256sums=('3bb7901211e14fb774e8fe960a0eb0c3fbbd30794f9dfba12d575abdc6c4a772')

build() {
  cd "${_pkgname}-${pkgver}"
  python setup.py build
}

package() {
  cd "${_pkgname}-${pkgver}"
  python setup.py install --root="${pkgdir}" --optimize=1 --skip-build
  install -Dvm644 'README.rst' -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dvm644 'LICENSE' -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
