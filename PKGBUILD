# Maintainer: Morten Linderud <morten@linderud.pw>

pkgname=auracle-git
_pkgname=auracle
pkgver=r8.89398f2
pkgrel=1
pkgdesc='Next generation cower'
arch=('any')
url="https://github.com/falconindy/auracle.git"
license=('MIT')
makedepends=('meson' 'ragel')
provides=("$_pkgname")
conflicts=("$_pkgname")
source=("git+https://github.com/falconindy/auracle.git")
sha256sums=('SKIP')

pkgver() {
  cd "$_pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build () {
  cd "$_pkgname"
  meson build -D buildtype=release
  ninja -C build
}

package () {
  cd "$_pkgname"
  DESTDIR="$pkgdir" ninja -C build install
  install -Dm644 "${srcdir}/${_pkgname}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim: et ts=2 sw=2
