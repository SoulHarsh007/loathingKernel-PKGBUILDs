# Maintainer: Morgan <morganamilo@archlinux.org>
pkgname=paru-git
_pkgname=paru
pkgver=1.0.0.r0.g387a38f
pkgrel=1
pkgdesc='AUR helper based on yay'
url='https://github.com/morganamilo/paru'
source=("git+https://github.com/morganamilo/paru")
backup=("etc/paru.conf")
arch=('x86_64' 'i686')
license=('GPL3')
makedepends=('cargo')
depends=('git' 'pacman')
optdepends=('asp: downloading repo pkgbuilds' 'bat: colored pkgbuild printing')
conflicts=('paru')
provides=('paru')
sha256sums=(SKIP)

build () {
  cd "$srcdir/$_pkgname"

  if pacman -T pacman-git > /dev/null; then
    _features+="git,generate,"
  fi

  if [[ $(rustc -V) == *"nightly"* ]]; then
    _features+="backtrace,"
  fi

  PARU_VERSION=$pkgver cargo build --locked --features "${_features:-}" --release
}

package() {
  cd "$srcdir/$_pkgname"

  install -Dm755 target/release/paru "${pkgdir}/usr/bin/paru"
  install -Dm644 paru.conf "${pkgdir}/etc/paru.conf"

  install -Dm644 man/paru.8 "$pkgdir/usr/share/man/man8/paru.8"
  install -Dm644 man/paru.conf.5 "$pkgdir/usr/share/man/man5/paru.conf.5"

  install -Dm644 completions/bash "${pkgdir}/usr/share/bash-completion/completions/paru.bash"
  install -Dm644 completions/fish "${pkgdir}/usr/share/fish/completions/paru.fish"
  install -Dm644 completions/zsh "${pkgdir}/usr/share/zsh/functions/Completion/Linux/_paru"
}

pkgver() {
  cd "$srcdir/$_pkgname"
  git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}
