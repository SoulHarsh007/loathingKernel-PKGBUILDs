# Maintainer:  max.bra <max dot bra dot gtalk at gmail dot com>
# Maintainer:  graysky <graysky AT archlinux DOT us>

pkgname=pi-hole-server
_pkgname=pi-hole
pkgver=5.2.3
pkgrel=1
_wwwpkgname=AdminLTE
_wwwpkgver=5.3
_now=`date +%N`
pkgdesc='The Pi-hole is an advertising-aware DNS/Web server. Arch adaptation for lan wide DNS server.'
arch=('any')
license=('EUPL-1.1')
url="https://github.com/pi-hole/pi-hole"
depends=('pi-hole-ftl>=5.0' 'bc' 'perl' 'net-tools' 'iproute2' 'logrotate' 'bind-tools' 'sudo' 'lsof')
optdepends=(
'lighttpd: a secure, fast, compliant and very flexible web-server'
'php-cgi: CGI and FCGI SAPI for PHP needed only for lighttpd'
'nginx-mainline: lightweight http server'
'php-fpm: FastCGI process manager for php needed for nginx'
'php-sqlite: sqlite db access for nginx'
)
conflicts=('pi-hole-standalone')
install=$pkgname.install
backup=('etc/dnsmasq.d/01-pihole.conf' 'etc/pihole/adlists.list' 'etc/dnsmasq.conf')

source=($pkgname-core-$pkgver.tar.gz::https://github.com/$_pkgname/$_pkgname/archive/v$pkgver.tar.gz
	    $pkgname-admin-$_wwwpkgver.tar.gz::https://github.com/$_pkgname/$_wwwpkgname/archive/v$_wwwpkgver.tar.gz
        arch-server-core-$pkgver-$_now.patch::"https://raw.githubusercontent.com/max72bra/pi-hole-server-archlinux-customization/master/arch-server-core-$pkgver.patch"
        arch-server-admin-$_wwwpkgver-$_now.patch::"https://raw.githubusercontent.com/max72bra/pi-hole-server-archlinux-customization/master/arch-server-admin-$_wwwpkgver.patch"
	    dnsmasq.include
	    lighttpd.pi-hole.conf
	    nginx.pi-hole.conf
	    $_pkgname.tmpfile
	    $_pkgname-gravity.service
	    $_pkgname-gravity.timer
	    $_pkgname-logtruncate.service
	    $_pkgname-logtruncate.timer
	    mimic_setupVars.conf.sh
	    mimic_basic-install.sh
	    piholeDebug.sh
)

sha256sums=('11c7cefc868e17c46f23ea7b747ce445515eac5154587d74d2dbd8d089b716c3'
            'bac26b2d9129bf68fbc73833fc17da32fba25754d93a59d88ed27a867e21fd42'
            'f8fe19afbbf7561540035b291c585251ed5182d00edc0b99da15ab22b4b3b657'
            '0df28287b76384eb97f0a6f9539b1285adc4ba223eef3982f5be11f0889d801d'
            '96c1fb8b15e1d0e99c18dc768f5dc3d4991184fb2631af84c5e2111028bc5287'
            '6495a9db2e77cc2e6b822f3c93d637842acdb7447811dd6dda9ded94bb205630'
            '032770450ba4a1085bcb0bf3f944c436c5702f3a3faf984fbbba2d3dbc6accea'
            '6da6bba6cfac4e87a1f1e8e1488b71858ac6feb0a2e327470a58d8f1e9ad8cbf'
            '9b72d7769036f8f4bb7121968d2ae4bdba427e4b16787ce340205a5f62b45c7c'
            '5228b4f923eab7784952a0fd6da895e7bff2f80a7f91c4a7c6350491dfdbb2e8'
            '88e3c78bbeaf5dc1100df65202ded8207877954a96bdf1b0ab3d9990d9fa759f'
            'ff507ce58c9492cce57e947696e1b814469fc2d856a1e303c6e68f98c62ebf46'
            'bfa80b3dd82d778dce6141ae50edefeda16c6d3851e11383e61e1a71a3ca3a59'
            'fa8d91d07b75f21076e5334c46d323cbc3dcf9a33fe9b8b4e032dbc5c979a6d2'
            '69a71c29dbe42ef0cbd3655fd7ce5cf04e8a77e27a5b2c3a1fcce0b544223309')

prepare() {
  cd "$srcdir"/"$_pkgname"-"$pkgver"
  patch -Np1 -i "$srcdir"/arch-server-core-$pkgver-$_now.patch
  cd "$srcdir"/"$_wwwpkgname"-"$_wwwpkgver"
  patch -Np1 -i "$srcdir"/arch-server-admin-$_wwwpkgver-$_now.patch
}

package() {
  cd "$srcdir"
  install -Dm755 $_pkgname-$pkgver/pihole "$pkgdir"/usr/bin/pihole

  install -dm755 "$pkgdir"/opt/pihole
  install -Dm755 $_pkgname-$pkgver/gravity.sh "$pkgdir"/opt/pihole/gravity.sh
  install -Dm755 $_pkgname-$pkgver/advanced/Scripts/version.sh "$pkgdir"/opt/pihole/version.sh
  install -Dm755 $_pkgname-$pkgver/advanced/Scripts/piholeLogFlush.sh "$pkgdir"/opt/pihole/piholeLogFlush.sh
  install -Dm755 $_pkgname-$pkgver/advanced/Scripts/chronometer.sh "$pkgdir"/opt/pihole/chronometer.sh
  install -Dm755 $_pkgname-$pkgver/advanced/Scripts/list.sh "$pkgdir"/opt/pihole/list.sh
  install -Dm755 $_pkgname-$pkgver/advanced/Scripts/webpage.sh "$pkgdir"/opt/pihole/webpage.sh
  install -Dm755 $_pkgname-$pkgver/advanced/Scripts/wildcard_regex_converter.sh "$pkgdir"/opt/pihole/wildcard_regex_converter.sh
  install -Dm755 $_pkgname-$pkgver/advanced/Scripts/query.sh "$pkgdir"/opt/pihole/query.sh
  install -Dm755 $_pkgname-$pkgver/advanced/Scripts/pihole-reenable.sh "$pkgdir"/opt/pihole/pihole-reenable.sh
  install -Dm755 $_pkgname-$pkgver/advanced/Scripts/piholeARPTable.sh "$pkgdir"/opt/pihole/piholeARPTable.sh

  install -Dm644 $_pkgname-$pkgver/advanced/Scripts/COL_TABLE "$pkgdir"/opt/pihole/COL_TABLE

  install -Dm644 $_pkgname-$pkgver/advanced/Templates/gravity.db.sql "$pkgdir"/opt/pihole/gravity.db.sql
  install -Dm644 $_pkgname-$pkgver/advanced/Templates/gravity_copy.sql "$pkgdir"/opt/pihole/gravity_copy.sql

  install -Dm755 piholeDebug.sh "$pkgdir"/opt/pihole/piholeDebug.sh
  install -Dm755 mimic_setupVars.conf.sh "$pkgdir"/opt/pihole/mimic_setupVars.conf.sh
  install -Dm755 mimic_basic-install.sh "$pkgdir"/opt/pihole/basic-install.sh

  cp -dpr --no-preserve=ownership $_pkgname-$pkgver/advanced/Scripts/database_migration "$pkgdir"/opt/pihole/

  install -dm750 "$pkgdir"/etc/sudoers.d
  install -Dm440 $_pkgname-$pkgver/advanced/Templates/pihole.sudo "$pkgdir"/etc/sudoers.d/pihole
  install -Dm644 $_pkgname-$pkgver/advanced/dnsmasq.conf.original "$pkgdir"/etc/dnsmasq.conf
  install -Dm644 dnsmasq.include "$pkgdir"/etc/dnsmasq.d/01-pihole.conf

  install -Dm644 pi-hole.tmpfile "$pkgdir"/usr/lib/tmpfiles.d/pi-hole.conf

  install -Dm644 "$_pkgname-gravity.timer" "$pkgdir/usr/lib/systemd/system/$_pkgname-gravity.timer"
  install -Dm644 "$_pkgname-gravity.service" $pkgdir/usr/lib/systemd/system/$_pkgname-gravity.service
  install -Dm644 "$_pkgname-logtruncate.timer" "$pkgdir/usr/lib/systemd/system/$_pkgname-logtruncate.timer"
  install -Dm644 "$_pkgname-logtruncate.service" $pkgdir/usr/lib/systemd/system/$_pkgname-logtruncate.service
  install -dm755 "$pkgdir/usr/lib/systemd/system/multi-user.target.wants"
  ln -s ../$_pkgname-gravity.timer "$pkgdir/usr/lib/systemd/system/multi-user.target.wants/$_pkgname-gravity.timer"
  ln -s ../$_pkgname-logtruncate.timer "$pkgdir/usr/lib/systemd/system/multi-user.target.wants/$_pkgname-logtruncate.timer"

  install -dm775 "$pkgdir"/etc/pihole
  install -dm755 "$pkgdir"/usr/share/pihole/configs
  install -Dm644 $_pkgname-$pkgver/dns-servers.conf "$pkgdir"/etc/pihole/dns-servers.conf
  install -Dm644 $_pkgname-$pkgver/advanced/Templates/logrotate "$pkgdir"/etc/pihole/logrotate
  install -Dm644 $_pkgname-$pkgver/adlists.list "$pkgdir"/etc/pihole/adlists.list
#  install -Dm644 /dev/null "$pkgdir"/etc/pihole/whitelist.txt
#  install -Dm644 /dev/null "$pkgdir"/etc/pihole/blacklist.txt
#  install -Dm664 /dev/null "$pkgdir"/etc/pihole/regex.list

  install -Dm644 lighttpd.pi-hole.conf "$pkgdir"/usr/share/pihole/configs/lighttpd.example.conf
  install -Dm644 nginx.pi-hole.conf "$pkgdir"/usr/share/pihole/configs/nginx.example.conf

  install -dm755 "$pkgdir"/srv/http/pihole/admin
  install -Dm644 $_pkgname-$pkgver/advanced/index.php "$pkgdir"/srv/http/pihole/pihole/index.php
#  install -Dm644 $_pkgname-$pkgver/advanced/index.js "$pkgdir"/srv/http/pihole/pihole/index.js
  install -Dm644 $_pkgname-$pkgver/advanced/blockingpage.css "$pkgdir"/srv/http/pihole/pihole/blockingpage.css

  cp -dpr --no-preserve=ownership $_wwwpkgname-$_wwwpkgver/* "$pkgdir"/srv/http/pihole/admin/

  install -dm755 "$pkgdir"/usr/share/licenses/pihole
  install -Dm644 ${pkgname%-*}-$pkgver/LICENSE "$pkgdir"/usr/share/licenses/pihole/Pi-hole
  install -Dm644 $_wwwpkgname-$_wwwpkgver/LICENSE "$pkgdir"/usr/share/licenses/pihole/AdminLTE
#  install -Dm644 $_wwwpkgname-$_wwwpkgver/style/vendor/SourceSansPro/OFL.txt \
#    "$pkgdir"/usr/share/licenses/pihole/SourceSansPro

  rm "$pkgdir"/srv/http/pihole/admin/*.md
  rm "$pkgdir"/srv/http/pihole/admin/LICENSE
  rm "$pkgdir"/srv/http/pihole/admin/style/vendor/LICENSE
  rm "$pkgdir"/srv/http/pihole/admin/scripts/vendor/LICENSE
#  rm "$pkgdir"/srv/http/pihole/admin/style/vendor/SourceSansPro/OFL.txt
}
