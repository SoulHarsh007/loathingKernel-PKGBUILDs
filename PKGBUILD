# Maintainer: willemw <willemw12@gmail.com>
# Contributor: Oliver Rümpelein <arch@pheerai.de>

pkgname=mergerfs
pkgver=2.25.0
pkgrel=1
pkgdesc="FUSE based union filesystem"
arch=('x86_64')
url="https://github.com/trapexit/mergerfs"
license=('custom:ISC')
depends=('fuse2')
makedepends=('git')    # 'pandoc'
#source=("https://github.com/trapexit/mergerfs/archive/$pkgver.tar.gz")
source=("https://github.com/trapexit/mergerfs/releases/download/$pkgver/mergerfs-$pkgver.tar.gz")
md5sums=('f62e0ce205687b2edd9284e3c82e6984')

build() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" PREFIX="/usr" SBINDIR="/usr/bin"
}

package() {
  cd $pkgname-$pkgver
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  make DESTDIR="$pkgdir" PREFIX="/usr" SBINDIR="/usr/bin" install
}

