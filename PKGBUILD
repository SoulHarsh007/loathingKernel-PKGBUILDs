pkgname=auracle-git
_pkgname=auracle
pkgver=r55.67cb813
pkgrel=1
pkgdesc='A flexible client for the AUR'
arch=('x86_64' 'i686')
url="https://github.com/falconindy/auracle.git"
license=('MIT')
depends=('pacman' 'libarchive.so' 'libcurl.so')
makedepends=('meson' 'git' 'nlohmann-json')
checkdepends=('gtest' 'gmock')
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

  arch-meson build
  ninja -C build
}

check() {
  meson test -C "$_pkgname/build"
}

package () {
  cd "$_pkgname"

  DESTDIR=$pkgdir ninja -C build install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: et ts=2 sw=2
