# Maintainer: loathingkernel <loathingkernel _a_ gmail _d_ com>

pkgname=proton-ge-custom
_srctag=GE-Proton8-13
_commit=ac6be1b9c3c1d402874e604b8d13c9652306b93f
pkgver=${_srctag//-/.}
_geckover=2.47.3
_monover=8.0.1
pkgrel=3
epoch=2
pkgdesc="Compatibility tool for Steam Play based on Wine and additional components, GloriousEggroll's custom build"
url="https://github.com/GloriousEggroll/proton-ge-custom"
arch=(x86_64 x86_64_v3)
options=(!staticlibs !lto emptydirs)
license=('custom')

depends=(
  attr             lib32-attr
  fontconfig       lib32-fontconfig
  libxcursor       lib32-libxcursor
  libxrandr        lib32-libxrandr
  libxi            lib32-libxi
  gettext          lib32-gettext
  freetype2        lib32-freetype2
  gcc-libs         lib32-gcc-libs
  libpcap          lib32-libpcap
  lzo              lib32-lzo
  libxkbcommon     lib32-libxkbcommon
  libvpx           lib32-libvpx
  'sdl2>=2.0.16'   'lib32-sdl2>=2.0.16'
  libsoup          lib32-libsoup
  libgudev         lib32-libgudev
#  blas             lib32-blas
#  lapack           lib32-lapack
  desktop-file-utils
  python
  steam-native-runtime
  cabextract
)

makedepends=(autoconf bison perl flex mingw-w64-gcc
  git wget rsync mingw-w64-tools lld nasm
  meson cmake fontforge afdko python-pefile
  glslang vulkan-headers
  clang
  giflib                lib32-giflib
  gnutls                lib32-gnutls
  libxinerama           lib32-libxinerama
  libxcomposite         lib32-libxcomposite
  libxxf86vm            lib32-libxxf86vm
  v4l-utils             lib32-v4l-utils
  alsa-lib              lib32-alsa-lib
  libxcomposite         lib32-libxcomposite
  mesa                  lib32-mesa
  mesa-libgl            lib32-mesa-libgl
  opencl-icd-loader     lib32-opencl-icd-loader
  libpulse              lib32-libpulse
  gtk3                  lib32-gtk3
  gst-plugins-base-libs lib32-gst-plugins-base-libs
  vulkan-icd-loader     lib32-vulkan-icd-loader
  'sdl2>=2.0.16'        'lib32-sdl2>=2.0.16'
  rust                  lib32-rust-libs
  libgphoto2
  opencl-headers
)

optdepends=(
  giflib                lib32-giflib
  gnutls                lib32-gnutls
  v4l-utils             lib32-v4l-utils
  libpulse              lib32-libpulse
  alsa-plugins          lib32-alsa-plugins
  alsa-lib              lib32-alsa-lib
  libxcomposite         lib32-libxcomposite
  libxinerama           lib32-libxinerama
  opencl-icd-loader     lib32-opencl-icd-loader
  gtk3                  lib32-gtk3
  gst-plugins-base-libs lib32-gst-plugins-base-libs
  vulkan-icd-loader     lib32-vulkan-icd-loader
  libgphoto2
)

makedepends=(${makedepends[@]} ${depends[@]})
provides=('proton')
install=${pkgname}.install
source=(
    proton-ge-custom::git+https://github.com/gloriouseggroll/proton-ge-custom.git#commit=${_commit}
    https://dl.winehq.org/wine/wine-gecko/${_geckover}/wine-gecko-${_geckover}-x86{,_64}.tar.xz
    https://github.com/madewokherd/wine-mono/releases/download/wine-mono-${_monover}/wine-mono-${_monover}-x86.tar.xz
    0001-AUR-Pkgbuild-changes.patch
    0002-AUR-Do-not-update-cargo-crates.patch
    0003-AUR-Remove-kaldi-openfst-vosk-api-modules-because-of.patch
    0004-AUR-Copy-DLL-dependencies-of-32bit-libvkd3d-dlls-int.patch
    fix_hwnd_changes_meaning.patch
)
# Optional patches
source+=(
    0005-AUR-Strip-binaries-early.patch
)
noextract=(
    wine-gecko-${_geckover}-{x86,x86_64}.tar.xz
    wine-mono-${_monover}-x86.tar.xz
)

_make_wrappers () {
    #     _arch     prefix   gcc    ld             as     strip
    local _i686=(  "i686"   "-m32" "-melf_i386"   "--32" "elf32-i386")
    local _x86_64=("x86_64" "-m64" "-melf_x86_64" "--64" "elf64-x86-64")
    local _opts=(_i686 _x86_64)
    declare -n _opt
    for _opt in "${_opts[@]}"; do
        for l in ar ranlib nm; do
            ln -s /usr/bin/gcc-$l wrappers/${_opt[0]}-pc-linux-gnu-$l
        done
        for t in gcc g++; do
            install -Dm755 /dev/stdin wrappers/${_opt[0]}-pc-linux-gnu-$t <<EOF
#!/usr/bin/bash
$(which ccache 2> /dev/null) /usr/bin/$t ${_opt[1]} "\$@"
EOF
        done
        install -Dm755 /dev/stdin wrappers/${_opt[0]}-pc-linux-gnu-ld <<EOF
#!/usr/bin/bash
/usr/bin/ld ${_opt[2]} "\$@"
EOF
        install -Dm755 /dev/stdin wrappers/${_opt[0]}-pc-linux-gnu-as <<EOF
#!/usr/bin/bash
/usr/bin/as ${_opt[3]} "\$@"
EOF
        install -Dm755 /dev/stdin wrappers/${_opt[0]}-pc-linux-gnu-strip <<EOF
#!/usr/bin/bash
/usr/bin/strip -F ${_opt[4]} "\$@"
EOF
    done
}

prepare() {

    # Provide wrappers to compiler tools
    rm -rf wrappers && mkdir wrappers
    _make_wrappers

    [ ! -d build ] && mkdir build

    cd proton-ge-custom

    [ ! -d contrib ] && mkdir -p contrib
    mv "$srcdir"/wine-gecko-${_geckover}-x86{,_64}.tar.xz contrib/
    mv "$srcdir"/wine-mono-${_monover}-x86.tar.xz contrib/

    # Explicitly set origin URL for submodules using relative paths
    git remote set-url origin https://github.com/gloriouseggroll/proton-ge-custom.git
    git -c protocol.file.allow=always submodule update --init --filter=tree:0 --recursive

    for rustlib in gst-plugins-rs media-converter; do
    pushd $rustlib
        export RUSTUP_TOOLCHAIN=stable
        export CARGO_HOME="${SRCDEST}"/proton-cargo
        cargo fetch --locked --target "i686-unknown-linux-gnu"
        cargo fetch --locked --target "x86_64-unknown-linux-gnu"
    popd
    done

    ./patches/protonprep-valve-staging.sh

    patch -p1 -i "$srcdir"/0001-AUR-Pkgbuild-changes.patch
    patch -p1 -i "$srcdir"/0002-AUR-Do-not-update-cargo-crates.patch
    patch -p1 -i "$srcdir"/0003-AUR-Remove-kaldi-openfst-vosk-api-modules-because-of.patch
    patch -p1 -i "$srcdir"/0004-AUR-Copy-DLL-dependencies-of-32bit-libvkd3d-dlls-int.patch
    patch -p1 -i "$srcdir"/fix_hwnd_changes_meaning.patch
    patch -p1 -i "$srcdir"/0005-AUR-Strip-binaries-early.patch
}

build() {
    export PATH="$(pwd)/wrappers:$PATH"

    cd build
    ROOTLESS_CONTAINER="" \
    ../proton-ge-custom/configure.sh \
        --container-engine="none" \
        --proton-sdk-image="" \
        --build-name="${pkgname}"

    # By default export FLAGS used by proton and ignore makepkg
    # This overrides FLAGS from makepkg.conf, if you comment these you are on your own
    # If you want the "best" possible optimizations for your system you can use
    # `-march=native` and remove the `-mtune=core-avx2` option.
    export CFLAGS="-O2 -march=nocona -mtune=core-avx2 -pipe"
    export CXXFLAGS="-O2 -march=nocona -mtune=core-avx2 -pipe"
    export RUSTFLAGS="-C opt-level=2 -C target-cpu=nocona"
    export LDFLAGS="-Wl,-O1,--sort-common,--as-needed"

    # If using -march=native and the CPU supports AVX, launching a d3d9
    # game can cause an Unhandled exception. The cause seems to be the
    # combination of AVX instructions and tree vectorization (implied by O3),
    # all tested archictures from sandybridge to haswell are affected.
    # Since Wine 5.16 AVX is supported. Testing showed 32bit applications
    # crashing with AVX regardless, but 64bit applications worked just fine.
    # Relevant Wine issues
    # https://bugs.winehq.org/show_bug.cgi?id=45289
    # https://bugs.winehq.org/show_bug.cgi?id=43516
    # AVX is "hard" disabled for 32bit in any case.
    # AVX2 for 64bit is disabled below.
    export CFLAGS+=" -mno-avx2"
    export CXXFLAGS+=" -mno-avx2"

    export RUSTUP_TOOLCHAIN=stable
    export CARGO_HOME="${SRCDEST}"/proton-cargo
    export WINEESYNC=0
    export WINEFSYNC=0
    export DISPLAY=
    SUBJOBS=$([[ "$MAKEFLAGS" =~ -j\ *([1-9][0-9]*) ]] && echo "${BASH_REMATCH[1]}" || echo "$(nproc)") \
        make -j1 dist
}

package() {
    cd build

    # Delete the intermediate build directories to free space (mostly for my github actions)
    rm -rf dst-* obj-* src-* pfx-*

    local _compatdir="$pkgdir/usr/share/steam/compatibilitytools.d"
    mkdir -p "$_compatdir/${pkgname}"
    rsync --delete -arx dist/* "$_compatdir/${pkgname}"

    # For some unknown to me reason, 32bit vkd3d (not vkd3d-proton) always links
    # to libgcc_s_dw2-1.dll no matter what linker options I tried.
    # Copy the required dlls into the package, they will be copied later into the prefix
    # by the patched proton script. Bundling the helps to avoid making mingw-w64-gcc package
    # a runtime dependency.
    cp /usr/i686-w64-mingw32/bin/{libgcc_s_dw2-1.dll,libwinpthread-1.dll} \
        "$_compatdir/${pkgname}"/files/lib/vkd3d/
    cp /usr/x86_64-w64-mingw32/bin/{libgcc_s_seh-1.dll,libwinpthread-1.dll} \
        "$_compatdir/${pkgname}"/files/lib64/vkd3d/

    mkdir -p "$pkgdir/usr/share/licenses/${pkgname}"
    mv "$_compatdir/${pkgname}"/LICENSE{,.OFL} \
        "$pkgdir/usr/share/licenses/${pkgname}"

    cd "$_compatdir/${pkgname}/files"
    i686-w64-mingw32-strip --strip-unneeded \
        $(find lib/wine \( -iname fakedlls -or -iname i386-windows \) -prune -false -or -iname "*.dll" -or -iname "*.exe")
    x86_64-w64-mingw32-strip --strip-unneeded \
        $(find lib64/wine \( -iname fakedlls -or -iname x86_64-windows \) -prune -false -or -iname "*.dll" -or -iname "*.exe")

    local _geckodir="share/wine/gecko/wine-gecko-${_geckover}"
    i686-w64-mingw32-strip --strip-unneeded \
        $(find "$_geckodir"-x86 -iname "*.dll" -or -iname "*.exe")
    x86_64-w64-mingw32-strip --strip-unneeded \
        $(find "$_geckodir"-x86_64 -iname "*.dll" -or -iname "*.exe")

    local _monodir="share/wine/mono/wine-mono-${_monover}"
    i686-w64-mingw32-strip --strip-unneeded \
        $(find "$_monodir"/lib/mono -iname "*.dll" -or -iname "*.exe")
    i686-w64-mingw32-strip --strip-unneeded \
        "$_monodir"/lib/x86/*.dll \
        $(find "$_monodir" -iname "*x86.dll" -or -iname "*x86.exe")
    x86_64-w64-mingw32-strip --strip-unneeded \
        "$_monodir"/lib/x86_64/*.dll \
        $(find "$_monodir" -iname "*x86_64.dll" -or -iname "*x86_64.exe")
}

sha256sums=('SKIP'
            '08d318f3dd6440a8a777cf044ccab039b0d9c8809991d2180eb3c9f903135db3'
            '0beac419c20ee2e68a1227b6e3fa8d59fec0274ed5e82d0da38613184716ef75'
            '83f65c9292137a740c4b8ea730b61cee0dbbb82e4eb3607590ba2f4377827464'
            '5bf0acdcf42aba4cd6f51d9d10d875a1f49ee06978c12c3a66ab6c697fb42185'
            '278ca05ea2507fa78e9da28bab2089b967694c795bf12c75ac70dd4ab0569315'
            'd455f8a28a7db526cb46c3f6955bafdc3301e28230ae85269feb287168ac737a'
            '2996051c31609205f154142da04112d9b17d742dbf7104f7fcd286b75aa0b83f'
            '20824bb565fefcad4aa978c54e0f8b9d9d17b7b52fb03fc87943150de148f06f')
# Optional patches
sha256sums+=(
            'SKIP'
)

