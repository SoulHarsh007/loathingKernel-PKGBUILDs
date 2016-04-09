pkgname=aurutils
pkgver=0.5.1
pkgrel=1
pkgdesc='helper tools for the arch user repository'
arch=('any')
url=https://github.com/AladW/aurutils
license=('ISC')
source=("https://github.com/AladW/aurutils/archive/$pkgver.tar.gz")
md5sums=('0cb58606e1b60502cda6f7eb7ef0139d')
depends=('pacman>=5.0' 'git' 'repose' 'jshon' 'pacutils' 'expac' 'aria2' 'datamash')
checkdepends=('shellcheck')
makedepends=('git')
optdepends=('devtools: aurbuild -c'
	    'vifm: improved build file interaction')

check() {
  cd "$pkgname-$pkgver"
  shellcheck -e 2016,2174 -x bin/*
}

package() {
  cd "$pkgname-$pkgver"
  install -d "$pkgdir"/usr/{bin,share{/licenses,/doc}/aurutils}

  install -m755 bin/* "$pkgdir"/usr/bin/
  install -m644 LICENSE "$pkgdir"/usr/share/licenses/aurutils/
  install -m644 README.org CREDITS doc/* "$pkgdir"/usr/share/doc/aurutils/
}

