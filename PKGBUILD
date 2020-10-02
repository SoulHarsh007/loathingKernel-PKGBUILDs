# Maintainer: willemw <willemw12@gmail.com>
# Contributor: Oliver Rümpelein <arch@pheerai.de>

pkgname=mergerfs
pkgver=2.31.0
pkgrel=1
pkgdesc="FUSE based union filesystem"
arch=('x86_64')
url="https://github.com/trapexit/mergerfs"
license=('custom:ISC')
makedepends=('git')    # 'pandoc'
optdepends=('fuse2: for mounting via fstab')
source=("https://github.com/trapexit/mergerfs/archive/$pkgver.tar.gz")
#source=("https://github.com/trapexit/mergerfs/releases/download/$pkgver/mergerfs-$pkgver.tar.gz")
md5sums=('219983914c50486aff14dbf268063f94')

prepare() {
  cd $pkgname-$pkgver
  sed -i 's|^VERSION=.*|VERSION="'$pkgver'"|' tools/update-version
}

build() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" PREFIX="/usr" SBINDIR="/usr/bin"
}

package() {
  cd $pkgname-$pkgver
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  make DESTDIR="$pkgdir" PREFIX="/usr" SBINDIR="/usr/bin" install
}

