# Maintainer: 
# Contributor: David Wu <xdavidwuph@gmail.com>
# Contributor: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Ben Reedy <thebenj88@gmail.com>
# Contributor: Clement Guerin <geecko.dev@free.fr>
# Contributor: Thiago Kenji Okada <thiago.mast3r@gmail.com>
# Contributor: uberushaximus <uberushaximus@gmail.com>

pkgname=(
  ppsspp-git
  ppsspp-assets-git
)
pkgver=1.15.4.r357.42d4b5d41d
pkgrel=1
pkgdesc='A PSP emulator written in C++'
arch=(x86_64)
url=https://www.ppsspp.org/
license=(GPL2)
makedepends=(
  clang
  lld
  cmake
  git
  glew
  glu
  libglvnd
  libzip
  ninja
  python
  qt5-base
  qt5-multimedia
  qt5-tools
  sdl2
  snappy
  zlib
)
options=(!lto)
source=(
  git+https://github.com/hrydgard/ppsspp.git
  git+https://github.com/Kingcom/armips.git
  git+https://github.com/discordapp/discord-rpc.git
  git+https://github.com/hrydgard/ppsspp-ffmpeg.git
  armips-filesystem::git+https://github.com/Kingcom/filesystem.git
  git+https://github.com/google/cpu_features.git
  git+https://github.com/KhronosGroup/glslang.git
  git+https://github.com/hrydgard/ppsspp-lang.git
  ppsspp-miniupnp::git+https://github.com/hrydgard/miniupnp.git
  git+https://github.com/Tencent/rapidjson.git
  git+https://github.com/KhronosGroup/SPIRV-Cross.git
  git+https://github.com/RetroAchievements/rcheevos.git
  ppsspp-sdl.desktop
  ppsspp-qt.desktop
)
b2sums=('SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'c6bcdfedee866dfdcc82a8c333c31ff73ed0beec65b63acec8bc8186383c0bc9f0912f21bb9715b665e8dc1793b1a85599761f9037856fa54ad8aa3bfdbfd468'
        '328e2ba47b78d242b0ec6ba6bfa039c77a36d1ef7246e5c2c2432d8e976e9360baf505eb05f48408ede1a30545cbbb7f875bf5ebd0252cef35523d449b8254a0')

pkgver() {
  cd ppsspp
  git describe --tags | sed 's/^v//; s/-/.r/; s/-g/./'
}

prepare() {
  cd ppsspp
  for submodule in assets/lang ext/miniupnp ffmpeg; do
    git submodule init ${submodule}
    git config submodule.${submodule}.url ../ppsspp-${submodule#*/}
    git -c protocol.file.allow=always submodule update ${submodule}
  done
  for submodule in ext/{armips,cpu_features,discord-rpc,glslang,rapidjson,SPIRV-Cross,rcheevos}; do
    git submodule init ${submodule}
    git config submodule.${submodule}.url ../${submodule#*/}
    git -c protocol.file.allow=always submodule update ${submodule}
  done
  cd ext/armips
  for submodule in ext/filesystem; do
    git submodule init ${submodule}
    git config submodule.${submodule}.url ../../../armips-${submodule#*/}
    git -c protocol.file.allow=always submodule update ${submodule}
  done
}

build() {
  export CC=clang
  export CXX=clang++
  # Rebuild ffmpeg locally
  pushd ppsspp/ffmpeg
  ./linux_x86-64.sh
  popd
  cmake -S ppsspp -B build-sdl -G Ninja \
    -Wno-dev \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_SKIP_RPATH=ON \
    -DHEADLESS=ON \
    -DOpenGL_GL_PREFERENCE=GLVND \
    -DUSE_SYSTEM_FFMPEG=OFF \
    -DUSE_SYSTEM_MINIUPNPC=OFF \
    -DUSE_SYSTEM_LIBZIP=ON \
    -DUSE_SYSTEM_SNAPPY=ON \
    -DUSE_SYSTEM_ZSTD=ON \
    -DUSING_QT_UI=OFF
  cmake --build build-sdl -v
  cmake -S ppsspp -B build-qt -G Ninja \
    -Wno-dev \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_SKIP_RPATH=ON \
    -DHEADLESS=OFF \
    -DOpenGL_GL_PREFERENCE=GLVND \
    -DUSE_SYSTEM_FFMPEG=OFF \
    -DUSE_SYSTEM_MINIUPNPC=OFF \
    -DUSE_SYSTEM_LIBZIP=ON \
    -DUSE_SYSTEM_SNAPPY=ON \
    -DUSE_SYSTEM_ZSTD=ON \
    -DUSING_QT_UI=ON
  cmake --build build-qt -v
}

package_ppsspp-git() {
  depends=(
    glew
    glibc
    hicolor-icon-theme
    libgl
    libzip
    ppsspp-assets-git
    qt5-base
    qt5-multimedia
    sdl2
    snappy
    zlib
    zstd
  )
  provides=(ppsspp)
  conflicts=(ppsspp)
  install -Dm 755 build-sdl/PPSSPPSDL -t "${pkgdir}"/usr/bin/
  install -Dm 755 build-sdl/PPSSPPHeadless -t "${pkgdir}"/usr/bin/
  install -Dm 755 build-qt/PPSSPPQt -t "${pkgdir}"/usr/bin/
  install -dm 755 "${pkgdir}"/usr/share/icons
  cp -dr --no-preserve=ownership ppsspp/icons/hicolor "${pkgdir}"/usr/share/icons/
  install -Dm 644 ppsspp/icons/icon-512.svg "${pkgdir}"/usr/share/pixmaps/ppsspp.svg
  install -Dm 644 ppsspp-sdl.desktop -t "${pkgdir}"/usr/share/applications/
  install -Dm 644 ppsspp-qt.desktop -t "${pkgdir}"/usr/share/applications/
}

package_ppsspp-assets-git() {
  provides=(ppsspp-assets)
  conflicts=(ppsspp-assets)
  install -dm 755 "${pkgdir}"/usr/share/ppsspp
  cp -dr --no-preserve=ownership build-sdl/assets "${pkgdir}"/usr/share/ppsspp/
}

# vim: ts=2 sw=2 et:
