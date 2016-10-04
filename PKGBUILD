pkgname=aurutils
pkgver=1.3.5
pkgrel=1
pkgdesc='helper tools for the arch user repository'
arch=('any')
url=https://github.com/AladW/aurutils
license=('ISC')
depends=('pacman>=5' 'expac>=7' 'git' 'jq'
	 'repose' 'pacutils>=0.4')
checkdepends=('shellcheck')
makedepends=('git')
optdepends=('devtools: build in an nspawn container'
	    'vifm: improved build file interaction'
	    'datamash: check tsort input'
	    'aria2>=1.23: alternative downloader'
	    'parallel: alternative downloader')
source=("$pkgname-$pkgver::git+$url#tag=$pkgver")
sha256sums=('SKIP')

check() {
  cd "$pkgname-$pkgver"
  make check
}

package() {
  cd "$pkgname-$pkgver"
  make DESTDIR="$pkgdir" PREFIX="/usr" install
}
