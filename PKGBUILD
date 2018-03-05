# Maintainer: Stelios Tsampas <loathingkernel @at gmail .dot com>

pkgname=arenatracker-git
pkgver=6.3.r48.g3df0c73
pkgrel=1
pkgdesc="Arena Tracker is a deck tracker that gives you a lot of extra info while playing Hearthstone"
arch=('x86_64')
url="https://github.com/supertriodo/Arena-Tracker"
license=('GPL')
depends=('qt5-base' 'python-pyautogui' 'xcb-util-renderutil' 'libpng12' 'opencv2')
makedepends=('imagemagick' 'git')
provides=("${pkgname/%-git/}")
conflicts=("${pkgname/%-git/}")
source=("${pkgname/%-git/}::git+https://github.com/supertriodo/Arena-Tracker.git"
        'ArenaTracker.desktop')
md5sums=('SKIP'
         '016d2e7016df6c2f07228ad49c5fb96c')

pkgver() {
    cd "${pkgname/%-git/}"
    git describe --long --tags 2>/dev/null | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
    cd "${pkgname/%-git/}"
    if [[ -d build ]]; then
        rm -rf build
    fi
    mkdir build
}

build() {
    cd "${pkgname/%-git/}"/build
    qmake \
        PREFIX=/usr \
        QMAKE_CFLAGS_RELEASE="${CFLAGS}" \
        QMAKE_CXXFLAGS_RELEASE="${CXXFLAGS}" \
        ../ArenaTracker.pro
    make
    convert ../ArenaTracker.ico ArenaTracker.png
}

package() {
    cd "${pkgname/%-git/}"
    install -dm755 "$pkgdir"/usr/bin
    install -dm755 "$pkgdir"/usr/share/{applications,pixmaps}
    install -m755 build/ArenaTracker "$pkgdir"/usr/bin/
    install -m644 build/ArenaTracker.png "$pkgdir"/usr/share/pixmaps/
    install -m644 "$srcdir"/ArenaTracker.desktop "$pkgdir"/usr/share/applications/
}
