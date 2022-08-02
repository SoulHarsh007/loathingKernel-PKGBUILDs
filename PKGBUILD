# Maintainer: Ondřej Hošek <ondra.hosek@gmail.com>
# Contributor: Jan de Groot <jgc@archlinux.org>
# Contributor: Maxime de Roucy <maxime.deroucy@gmail.com>
# Contributor: Darwin Bautista <djclue917@gmail.com>

pkgname=lib32-gsm
_pkgbase=gsm
pkgver=1.0.21
pkgrel=1
pkgdesc="Shared libraries for GSM 06.10 lossy speech compression"
arch=('x86_64')
url="http://www.quut.com/gsm/"
license=('custom')
depends=('gsm' 'lib32-glibc')
makedepends=('lib32-gcc-libs')
source=("http://www.quut.com/${_pkgbase}/${_pkgbase}-${pkgver}.tar.gz"
        'gsm-shared.patch')
sha256sums=('7d8439fc6ed8bfba1a85011f26800b2afee78b96555c9ed9ce9d3024d4da7754'
            'c551ef1efef5b6a56fb8d955d1c8adf89f11556330dc8df405e3ffb0e3f3f8d7')


prepare() {
  cd "${srcdir}/${_pkgbase}-${pkgver%.*}-pl${pkgver##*.}/"

  patch -p0 -i "${srcdir}/gsm-shared.patch"
}

build() {
  cd "${srcdir}/${_pkgbase}-${pkgver%.*}-pl${pkgver##*.}/"

  # flags for shared lib
  CFLAGS="${CFLAGS} -fPIC"
  make \
    CC="gcc -m32" \
    CCFLAGS="-c ${CFLAGS} -fPIC"
}

package() {
  cd "${srcdir}/${_pkgbase}-${pkgver%.*}-pl${pkgver##*.}/"

  # Prepare directories
  install -m755 -d "${pkgdir}"/usr/{bin,lib,lib32,include/gsm,share/{licenses/${_pkgbase},man/man{1,3}}}

  make -j1 \
    CC="gcc -m32" \
    INSTALL_ROOT="${pkgdir}/usr" \
    GSM_INSTALL_LIB="${pkgdir}/usr/lib32" \
    GSM_INSTALL_INC="${pkgdir}/usr/include/gsm" \
    GSM_INSTALL_MAN="${pkgdir}/usr/share/man/man3" \
    TOAST_INSTALL_MAN="${pkgdir}/usr/share/man/man1" \
    install

  # clean directories provided by 64-bit package
  rm -Rf "${pkgdir}"/usr/{bin,include,lib,share}
}
