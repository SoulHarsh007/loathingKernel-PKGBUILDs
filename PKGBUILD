# Maintainer: Alad Wenter <alad@mailbox.org>
pkgname=aurutils
pkgver=1.5.3
pkgrel=4
pkgdesc='helper tools for the arch user repository'
arch=('any')
url='https://github.com/AladW/aurutils'
license=('custom:ISC')
depends=('pacman>=5' 'git' 'jq' 'pacutils>=0.4')
makedepends=('git')
optdepends=('devtools: systemd-nspawn support'
            'vifm: build file interaction'
            'aria2: threaded downloads'
            'parallel: threaded downloads'
            'expac: aursift script'
            'repose: repo-add alternative')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz"
        "$pkgname-$pkgver.tar.gz.asc::$url/releases/download/$pkgver/$pkgver.tar.gz.asc"
        "0001-aurbuild-backport-fix-for-236.patch"
        "0002-aurbuild-disable-verbose-signing.patch")
sha256sums=('a09088a460e352179dbf799d915e866af47aa280474a9c943f8e6885490734c5'
            'SKIP'
            '5001ece7fc2a4ec7e1860a0162e042f19adab13bad5c1070436306f2fe2f2b86'
            'f0a2d95b4fb51e4a392e0515ef6e10e0478a609caf7257aa8a896fadf027bfbb')
# Alad Wenter <alad@mailbox.org>
validpgpkeys=('DBE7D3DD8C81D58D0A13D0E76BC26A17B9B7018A')

prepare() {
    cd "$pkgname-$pkgver"
    patch -p1 < "$srcdir"/0001-aurbuild-backport-fix-for-236.patch
    patch -p1 < "$srcdir"/0002-aurbuild-disable-verbose-signing.patch
}

package() {
    cd "$pkgname-$pkgver"
    make DESTDIR="$pkgdir" PREFIX="/usr" install
}
