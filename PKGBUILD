# Contributor: Mettacrawer <metta.crawler@gmail.com>
# Maintainer:  max.bra <max dot bra dot gtalk at gmail dot com>
# Maintainer:  graysky <graysky AT archlinux DOT us>

pkgname=pi-hole-ftl
_pkgname=FTL
_servicename=pihole-FTL
pkgver=5.0
pkgrel=1
_now=`date +%N`
arch=('i686' 'x86_64' 'arm' 'armv6h' 'armv7h' 'aarch64')
pkgdesc="The Pi-hole FTL engine"
url="https://github.com/pi-hole/FTL"
license=('EUPL-1.1')
depends=('nettle' 'gmp')
makedepends=('sqlite')
conflicts=('dnsmasq')
provides=('dnsmasq')
install=$pkgname.install
backup=('etc/pihole/pihole-FTL.conf' 'etc/pihole/pihole-FTL.db')
source=($pkgname-v$pkgver.tar.gz::"https://github.com/pi-hole/FTL/archive/v$pkgver.tar.gz"
        arch-ftl-$pkgver-$_now.patch::"https://raw.githubusercontent.com/max72bra/pi-hole-ftl-archlinux-customization/master/arch-ftl-$pkgver.patch"
        "$pkgname.tmpfile"
        "$pkgname.sysuser"
        "$pkgname.service"
        "$pkgname.db"
        "$pkgname.conf")
md5sums=('a405fee9a924324eefe6bfb832180c3d'
         'b5a92d614ca46486bd2ede3c8bb13af8'
         'ca844c23699ba64777571253bc7ccb21'
         '455c38b73491bf641e422be3652698b7'
         '6dfe9e75d89554e7a290ba815d85c068'
         '0495c002b7d5dce303d451e4cd2fede5'
         'a9c8de83f02d36bfe96db57975984bbb')

prepare() {
#  cd "$srcdir"/"$_pkgname"-"$pkgver"/src/dnsmasq
#  patch -Np2 -i "$srcdir"/glib.patch
  cd "$srcdir"/"$_pkgname"-"$pkgver"
#  patch -Np1 -i "$srcdir"/nettle35.patch
  patch -Np1 -i "$srcdir"/arch-ftl-$pkgver-$_now.patch
}

build() {
  cd $_pkgname-$pkgver
  make
}

package() {
  cd "$srcdir"
  install -Dm755 "$_pkgname"-$pkgver/pihole-FTL "${pkgdir}"/usr/bin/pihole-FTL
  
  install -Dm644 "$pkgname.tmpfile" "$pkgdir"/usr/lib/tmpfiles.d/$pkgname.conf
  install -Dm644 "$pkgname.sysuser" "$pkgdir"/usr/lib/sysusers.d/$pkgname.conf

  install -dm755 "$pkgdir"/etc/pihole
  install -Dm644 "$pkgname.conf" "$pkgdir"/etc/pihole/pihole-FTL.conf
  install -Dm644 "$pkgname.db" "$pkgdir"/etc/pihole/pihole-FTL.db

  install -Dm644 "$pkgname.service" "$pkgdir"/usr/lib/systemd/system/$_servicename.service
  install -dm755 "$pkgdir/usr/lib/systemd/system/multi-user.target.wants"
  ln -s ../$_servicename.service "$pkgdir/usr/lib/systemd/system/multi-user.target.wants/$_servicename.service"
  
  # ver. 5.0 dnamasq dropin support
  ln -s ./pihole-FTL "$pkgdir/usr/bin/dnsmasq"
}
