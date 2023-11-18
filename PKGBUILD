# Maintainer: loathingkernel <loathingkernel @at gmail .dot com>

pkgname=vkd3d-proton-mingw
pkgver=2.10
pkgrel=1
pkgdesc='Fork of VKD3D. Development branches for Protons Direct3D 12 implementation'
arch=('x86_64')
url="https://github.com/HansKristian-Work/vkd3d-proton"
license=('LGPL-2.1')
makedepends=('ninja' 'meson>=0.43' 'glslang' 'git' 'mingw-w64-gcc' 'mingw-w64-tools')
provides=('vkd3d-proton' 'd3d12.dll' "vkd3d-proton=$pkgver")
conflicts=('vkd3d-proton' 'd3d12.dll')
options=(!lto !staticlibs)
source=(
    "git+https://github.com/HansKristian-Work/vkd3d-proton.git#tag=v$pkgver"
    "setup_vkd3d_proton"
    "vkd3d-proton-extraopts.patch"
)

prepare() {
    cd vkd3d-proton

    # Explicitly set origin URL for submodules using relative paths
    git remote set-url origin https://github.com/HansKristian-Work/vkd3d-proton.git
    git submodule update --init --filter=tree:0 --recursive

    # Uncomment to enable extra optimizations
    # Patch crossfiles with extra optimizations from makepkg.conf
    patch -p1 -i "$srcdir"/vkd3d-proton-extraopts.patch

    # By default export FLAGS used by proton and ignore makepkg
    # This overrides FLAGS from makepkg.conf, if you comment these you are on your own
    # If you want the "best" possible optimizations for your system you can use
    # `-march=native` and remove the `-mtune=core-avx2` option.
    export CFLAGS="-O2 -march=nocona -mtune=core-avx2 -pipe"
    export CXXFLAGS="-O2 -march=nocona -mtune=core-avx2 -pipe"
    export LDFLAGS="-Wl,-O1,--sort-common,--as-needed"

    # These flags are taken from Proton
    CFLAGS+=" -mfpmath=sse -fwrapv -fno-strict-aliasing"
    CXXFLAGS+=" -mfpmath=sse -fwrapv -fno-strict-aliasing -std=c++17"
    LDFLAGS+=" -Wl,--file-alignment,4096"

    # If using -march=native and the CPU supports AVX, launching a d3d9
    # game can cause an Unhandled exception. The cause seems to be the
    # combination of AVX instructions and tree vectorization (implied by O3),
    # all tested archictures from sandybridge to haswell are affected.
    # Disabling AVX (and AVX2 as a side-effect).
    # Since Wine 5.16 AVX is supported. Testing showed 32bit applications
    # crashing with AVX regardless, but 64bit applications worked just fine.
    # So disable AVX only for the 32bit binaries and AVX2 for the 64bit.
    # AVX2 seems to degrade performance. So disregard the above.
    # Relevant Wine issues
    # https://bugs.winehq.org/show_bug.cgi?id=45289
    # https://bugs.winehq.org/show_bug.cgi?id=43516
    CFLAGS+=" -mno-avx2"
    CXXFLAGS+=" -mno-avx2"

    local cross_ldflags="$LDFLAGS"

    local cross_cflags="$CFLAGS -mcmodel=small"
    local cross_cxxflags="$CXXFLAGS -mcmodel=small"
    sed -i build-win64.txt \
        -e "s|@CARGS@|\'${cross_cflags// /\',\'}\'|g" \
        -e "s|@CXXARGS@|\'${cross_cxxflags// /\',\'}\'|g" \
        -e "s|@LDARGS@|\'${cross_ldflags// /\',\'}\'|g"

    local cross_cflags="$CFLAGS -mstackrealign -mno-avx"
    local cross_cxxflags="$CXXFLAGS -mstackrealign -mno-avx"
    sed -i build-win32.txt \
        -e "s|@CARGS@|\'${cross_cflags// /\',\'}\'|g" \
        -e "s|@CXXARGS@|\'${cross_cxxflags// /\',\'}\'|g" \
        -e "s|@LDARGS@|\'${cross_ldflags// /\',\'}\'|g"
}

build() {
    meson setup vkd3d-proton "build/x64" \
        --prefix "/usr/share/vkd3d-proton/x64" \
        --cross-file vkd3d-proton/build-win64.txt \
        --bindir "" --libdir "" \
        --buildtype "plain" \
        --strip \
        -Denable_tests=false
    ninja -C "build/x64" -v

    meson setup vkd3d-proton "build/x86" \
        --cross-file vkd3d-proton/build-win32.txt \
        --prefix "/usr/share/vkd3d-proton/x86" \
        --bindir "" --libdir "" \
        --buildtype "plain" \
        --strip \
        -Denable_tests=false
    ninja -C "build/x86" -v
}

package() {
    depends=('vulkan-icd-loader' 'lib32-vulkan-icd-loader' 'wine' 'bash')

    DESTDIR="$pkgdir" ninja -C "build/x86" install
    DESTDIR="$pkgdir" ninja -C "build/x64" install
    install -Dm 755 -t "$pkgdir/usr/share/vkd3d-proton" vkd3d-proton/setup_vkd3d_proton.sh
    install -Dm 644 -t "$pkgdir/usr/share/doc/$pkgname" vkd3d-proton/README.md
    install -Dm 644 -t "$pkgdir/usr/share/licenses/$pkgname" vkd3d-proton/LICENSE
    install -Dm 755 -t "$pkgdir/usr/bin" setup_vkd3d_proton
}

sha256sums=('SKIP'
            '67815eed9d47bbf610e23c6a1e4954c11371886c2ca73555dd9f1d6fbebb1323'
            '8fc019d1dca8c52b6af96c40ff06a6c215aad3e713ae17be72c7422f1ba45634')
