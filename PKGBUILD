# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Ben Reedy <thebenj88@gmail.com>
# Contributor: Clement Guerin <geecko.dev@free.fr>
# Contributor: Thiago Kenji Okada <thiago.mast3r@gmail.com>
# Contributor: uberushaximus <uberushaximus@gmail.com>

pkgbase=ppsspp-git
pkgname=('ppsspp-git' 'ppsspp-qt-git')
pkgver=1.3.r229.47ee86ebc
pkgrel=1
pkgdesc='A PSP emulator written in C++'
arch=('i686' 'x86_64')
url='http://www.ppsspp.org/'
license=('GPL2')
depends=('gcc-libs' 'glew' 'glibc' 'libgl' 'libzip' 'sdl2' 'zlib'
         'libavcodec.so' 'libavformat.so' 'libavutil.so' 'libswresample.so'
         'libswscale.so')
makedepends=('cmake' 'git' 'glu' 'qt5-multimedia' 'qt5-tools')
source=('git+https://github.com/hrydgard/ppsspp.git'
        'git+https://github.com/hrydgard/ppsspp-lang.git'
        'ppsspp-glslang::git+https://github.com/hrydgard/glslang.git'
        'ppsspp-armips::git+https://github.com/Kingcom/armips.git'
        'armips-tinyformat::git+https://github.com/Kingcom/tinyformat.git'
        'ppsspp.desktop')
sha256sums=('SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            '1c332702d0aeced07df7e12ba8530bc3f19a52bc76c355f6c84c141becfd46d8')

pkgver() {
  cd ppsspp

  echo "$(git describe --tags | sed 's/^v//; s/-/.r/; s/-g/./')"
}

prepare() {
  cd ppsspp

  for submodule in assets/lang ext/{armips,glslang}; do
    git submodule init ${submodule}
    git config submodule.${submodule}.url ../ppsspp-${submodule#*/}
    git submodule update ${submodule}
  done

  pushd ext/armips
  git submodule init ext/tinyformat
  git config submodule.ext/tinyformat.url ../../../armips-tinyformat
  git submodule update ext/tinyformat
  popd

  for ui in sdl qt; do
    if [[ -d build-$ui ]]; then
      rm -rf build-$ui
    fi
    mkdir build-$ui
  done
}

build() {
  cd ppsspp/build-sdl

  cmake .. \
    -DCMAKE_BUILD_TYPE='Release' \
    -DCMAKE_SKIP_RPATH='ON' \
    -DUSE_SYSTEM_FFMPEG='ON'
  make

  cd ../build-qt

  cmake .. \
    -DCMAKE_BUILD_TYPE='Release' \
    -DCMAKE_SKIP_RPATH='ON' \
    -DUSE_SYSTEM_FFMPEG='ON' \
    -DUSING_QT_UI='ON'
  make
}

package_ppsspp-git() {
  provides=('ppsspp')
  conflicts=('ppsspp' 'ppsspp-qt' 'ppsspp-qt-git')

  cd ppsspp/build-sdl

  install -dm 755 "${pkgdir}"/usr/{bin,share/{applications,icons,man/man1,pixmaps,ppsspp}}
  install -m 755 PPSSPPSDL "${pkgdir}"/usr/bin/ppsspp
  cp -dr --no-preserve='ownership' assets "${pkgdir}"/usr/share/ppsspp/
  cp -dr --no-preserve='ownership' ../icons/hicolor "${pkgdir}"/usr/share/icons/
  install -m 644 ../icons/icon-512.svg "${pkgdir}"/usr/share/pixmaps/ppsspp.svg
  install -m 644 ../../ppsspp.desktop "${pkgdir}"/usr/share/applications/
}

package_ppsspp-qt-git() {
  depends+=('qt5-base' 'qt5-multimedia')
  provides=('ppsspp')
  conflicts=('ppsspp' 'ppsspp-git' 'ppsspp-qt')

  cd ppsspp/build-qt

  install -dm 755 "${pkgdir}"/usr/{bin,share/{applications,man/man1,pixmaps}}
  install -m 755 PPSSPPQt "${pkgdir}"/usr/bin/ppsspp
  cp -dr --no-preserve='ownership' assets "${pkgdir}"/usr/share/ppsspp/
  cp -dr --no-preserve='ownership' ../icons/hicolor "${pkgdir}"/usr/share/icons/
  install -m 644 ../icons/icon-512.svg "${pkgdir}"/usr/share/pixmaps/ppsspp.svg
  install -m 644 ../../ppsspp.desktop "${pkgdir}"/usr/share/applications/
}

# vim ts=2 sw=2 et:
