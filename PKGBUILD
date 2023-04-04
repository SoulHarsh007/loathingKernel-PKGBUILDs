# Maintainer: loathingkernel <loathingkernel _a_ gmail _d_ com>

pkgname=proton-ge-custom
_srctag=GE-Proton7-54
_commit=a90206a80ebef800d21f53a7dab667b4bbc97add
pkgver=${_srctag//-/.}
_geckover=2.47.3
_monover=7.4.0
pkgrel=1
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
  libldap               lib32-libldap
  openal                lib32-openal
  v4l-utils             lib32-v4l-utils
  alsa-lib              lib32-alsa-lib
  libxcomposite         lib32-libxcomposite
  mesa                  lib32-mesa
  mesa-libgl            lib32-mesa-libgl
  opencl-icd-loader     lib32-opencl-icd-loader
  libpulse              lib32-libpulse
  libva                 lib32-libva
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
  libldap               lib32-libldap
  gnutls                lib32-gnutls
  openal                lib32-openal
  v4l-utils             lib32-v4l-utils
  libpulse              lib32-libpulse
  alsa-plugins          lib32-alsa-plugins
  alsa-lib              lib32-alsa-lib
  libxcomposite         lib32-libxcomposite
  libxinerama           lib32-libxinerama
  opencl-icd-loader     lib32-opencl-icd-loader
  libva                 lib32-libva
  gtk3                  lib32-gtk3
  gst-plugins-base-libs lib32-gst-plugins-base-libs
  vulkan-icd-loader     lib32-vulkan-icd-loader
  libgphoto2
  dosbox
)

makedepends=(${makedepends[@]} ${depends[@]})
provides=('proton')
install=${pkgname}.install
source=(
    proton-ge-custom::git+https://github.com/gloriouseggroll/proton-ge-custom.git#commit=${_commit}
    wine-valve::git+https://github.com/ValveSoftware/wine.git
    dxvk::git+https://github.com/doitsujin/dxvk.git
    openvr::git+https://github.com/ValveSoftware/openvr.git
    liberation-fonts::git+https://github.com/liberationfonts/liberation-fonts.git
    gstreamer::git+https://gitlab.freedesktop.org/gstreamer/gstreamer.git
    gst-plugins-base::git+https://gitlab.freedesktop.org/gstreamer/gst-plugins-base.git
    gst-plugins-good::git+https://gitlab.freedesktop.org/gstreamer/gst-plugins-good.git
    gst-orc::git+https://gitlab.freedesktop.org/gstreamer/orc.git
    vkd3d-proton::git+https://github.com/HansKristian-Work/vkd3d-proton.git
    OpenXR-SDK::git+https://github.com/KhronosGroup/OpenXR-SDK.git
    dxvk-nvapi::git+https://github.com/jp7677/dxvk-nvapi.git
    vkd3d-valve::git+https://github.com/ValveSoftware/vkd3d.git
    Vulkan-Headers::git+https://github.com/KhronosGroup/Vulkan-Headers.git
    SPIRV-Headers::git+https://github.com/KhronosGroup/SPIRV-Headers.git
    Vulkan-Loader::git+https://github.com/KhronosGroup/Vulkan-Loader.git
    glslang::git+https://github.com/KhronosGroup/glslang.git
    gst-libav::git+https://gitlab.freedesktop.org/gstreamer/gst-libav.git
    ffmpeg::git+https://git.ffmpeg.org/ffmpeg.git
    dav1d::git+https://code.videolan.org/videolan/dav1d.git
    gst-plugins-rs::git+https://gitlab.freedesktop.org/gstreamer/gst-plugins-rs.git
    dxil-spirv::git+https://github.com/HansKristian-Work/dxil-spirv.git
    graphene::git+https://github.com/ebassi/graphene.git
    libdisplay-info-dxvk::git+https://gitlab.freedesktop.org/JoshuaAshton/libdisplay-info.git
    wine-staging::git+https://github.com/wine-staging/wine-staging.git
    protonfixes-gloriouseggroll::git+https://github.com/gloriouseggroll/protonfixes.git
    gst-plugins-bad::git+https://gitlab.freedesktop.org/gstreamer/gst-plugins-bad.git
    gst-plugins-ugly::git+https://gitlab.freedesktop.org/gstreamer/gst-plugins-ugly.git
    https://dl.winehq.org/wine/wine-gecko/${_geckover}/wine-gecko-${_geckover}-x86{,_64}.tar.xz
    https://github.com/madewokherd/wine-mono/releases/download/wine-mono-${_monover}/wine-mono-${_monover}-x86.tar.xz
    0001-AUR-Pkgbuild-changes.patch
    0002-AUR-Do-not-update-cargo-crates.patch
)
# Optional patches
source+=(
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

    [ ! -d gecko ] && mkdir gecko
    mv wine-gecko-${_geckover}-x86{,_64}.tar.xz gecko/

    [ ! -d mono ] && mkdir mono
    mv wine-mono-${_monover}-x86.tar.xz mono/

    [ ! -d build ] && mkdir build
    cd proton-ge-custom

    _submodules=(
        wine-valve::wine
        dxvk
        openvr
        liberation-fonts::fonts/liberation-fonts
        gstreamer
        gst-plugins-base
        gst-plugins-good
        gst-orc
        vkd3d-proton
        OpenXR-SDK
        dxvk-nvapi
        vkd3d-valve::vkd3d
        Vulkan-Headers
        SPIRV-Headers
        Vulkan-Loader
        glslang
        gst-libav
        ffmpeg::FFmpeg
        dav1d
        gst-plugins-rs
        graphene
        wine-staging
        protonfixes-gloriouseggroll::protonfixes
        gst-plugins-bad
        gst-plugins-ugly
    )

    for submodule in "${_submodules[@]}"; do
        git submodule init "${submodule#*::}"
        git submodule set-url "${submodule#*::}" "$srcdir"/"${submodule%::*}"
        git -c protocol.file.allow=always submodule update "${submodule#*::}"
    done

    pushd dxvk
        git submodule init include/{vulkan,spirv}
        git submodule set-url include/vulkan "$srcdir/Vulkan-Headers"
        git submodule set-url include/spirv "$srcdir/SPIRV-Headers"
        git -c protocol.file.allow=always submodule update include/{vulkan,spirv}

        git submodule init subprojects/libdisplay-info
        git submodule set-url subprojects/libdisplay-info "$srcdir/libdisplay-info-dxvk"
        git -c protocol.file.allow=always submodule update subprojects/libdisplay-info
    popd

    pushd vkd3d-proton
        for submodule in subprojects/{dxil-spirv,Vulkan-Headers,SPIRV-Headers}; do
            git submodule init "${submodule}"
            git submodule set-url "${submodule}" "$srcdir"/"${submodule#*/}"
            git -c protocol.file.allow=always submodule update "${submodule}"
        done
        pushd subprojects/dxil-spirv
            git submodule init third_party/spirv-headers
            git submodule set-url third_party/spirv-headers "$srcdir"/SPIRV-Headers
            git -c protocol.file.allow=always submodule update third_party/spirv-headers
        popd
    popd

    pushd dxvk-nvapi
        git submodule init external/Vulkan-Headers
        git submodule set-url external/Vulkan-Headers "$srcdir"/Vulkan-Headers
        git -c protocol.file.allow=always submodule update external/Vulkan-Headers
    popd

    for submodule in gst-plugins-rs media-converter; do
    pushd $submodule
        export RUSTUP_TOOLCHAIN=stable
        export CARGO_HOME="${SRCDEST}"/proton-cargo
        cargo fetch --locked --target "i686-unknown-linux-gnu"
        cargo fetch --locked --target "x86_64-unknown-linux-gnu"
    popd
    done

    ./patches/protonprep-valve-staging.sh

    pushd wine
        # From Arch Wine
        sed 's|OpenCL/opencl.h|CL/opencl.h|g' -i configure*
        # Fix openldap 2.5+ detection
        sed 's/-lldap_r/-lldap/' -i configure
    popd

    patch -p1 -i "$srcdir"/0001-AUR-Pkgbuild-changes.patch
    patch -p1 -i "$srcdir"/0002-AUR-Do-not-update-cargo-crates.patch

    # Remove repos from srcdir to save space
    for submodule in "${_submodules[@]}"; do
        rm -rf "$srcdir"/"${submodule%::*}"
    done
    rm -rf "$srcdir"/dxil-spirv
    rm -rf "$srcdir"/Vulkan-Headers
    rm -rf "$srcdir"/SPIRV-Headers
}

build() {
    export PATH="$(pwd)/wrappers:$PATH"

    cd build
    ROOTLESS_CONTAINER="" \
    ../proton-ge-custom/configure.sh \
        --container-engine="none" \
        --proton-sdk-image="" \
        --steam-runtime=native \
        --no-proton-sdk \
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

    local _compatdir="$pkgdir/usr/share/steam/compatibilitytools.d"
    mkdir -p "$_compatdir"
    cp -rf --no-dereference --preserve=mode,links dist "$_compatdir/${pkgname}"

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
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            '08d318f3dd6440a8a777cf044ccab039b0d9c8809991d2180eb3c9f903135db3'
            '0beac419c20ee2e68a1227b6e3fa8d59fec0274ed5e82d0da38613184716ef75'
            '9249ece664bcf2fecb1308ea1d2542c72923df9fe3df891986f137b2266a9ba3'
            'ee4952198ff3bb139d23f29fb591825c664c5df690d251a9716555d085e17c99'
            '697858a2455f05935172113c52ac60fc355d15bcc73270de5f969b3ecb2b2194')
# Optional patches
sha256sums+=(
)

