# Maintainer: loathingkernel <loathingkernel @at gmail .dot com>

pkgname=dxvk-mingw
pkgver=2.3
pkgrel=3
pkgdesc='Vulkan-based implementation of D3D9, D3D10 and D3D11 for Linux / Wine, MingW version'
arch=('x86_64')
url="https://github.com/doitsujin/dxvk"
license=('zlib/libpng')
makedepends=('ninja' 'meson>=0.43' 'glslang' 'git' 'mingw-w64-gcc')
provides=('dxvk' 'd9vk' "dxvk=$pkgver")
conflicts=('dxvk' 'd9vk')
options=(!lto !staticlibs)
source=(
    "git+https://github.com/doitsujin/dxvk.git#tag=v$pkgver"
    "dxvk-extraopts.patch"
    "setup_dxvk.sh"
    "setup_dxvk"
)

prepare() {
    cd dxvk

    # Explicitly set origin URL for submodules using relative paths
    git remote set-url origin https://github.com/doitsujin/dxvk.git
    git submodule update --init --filter=tree:0 --recursive

    # Uncomment to enable extra optimizations
    # Patch crossfiles with extra optimizations from makepkg.conf
    patch -p1 -i "$srcdir"/dxvk-extraopts.patch

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
    meson setup dxvk "build/x64" \
        --cross-file dxvk/build-win64.txt \
        --prefix "/usr/share/dxvk/x64" \
        --bindir "" --libdir "" \
        --buildtype "plain" \
        --strip
    ninja -C "build/x64" -v

    meson setup dxvk "build/x32" \
        --cross-file dxvk/build-win32.txt \
        --prefix "/usr/share/dxvk/x32" \
        --bindir "" --libdir "" \
        --buildtype "plain" \
        --strip
    ninja -C "build/x32" -v
}

package() {
    depends=('vulkan-icd-loader' 'lib32-vulkan-icd-loader' 'wine' 'bash')

    DESTDIR="$pkgdir" ninja -C "build/x32" install
    DESTDIR="$pkgdir" ninja -C "build/x64" install
    install -Dm 755 -t "$pkgdir/usr/share/dxvk" setup_dxvk.sh
    install -Dm 644 -t "$pkgdir/usr/share/dxvk" dxvk/dxvk.conf
    install -Dm 644 -t "$pkgdir/usr/share/doc/$pkgname" dxvk/README.md
    install -Dm 644 -t "$pkgdir/usr/share/licenses/$pkgname" dxvk/LICENSE
    install -Dm 755 -t "$pkgdir/usr/bin" setup_dxvk
}

sha256sums=('SKIP'
            'bcc15521e4c7f966a0192a1dabb7fb4935b33db39344ab5b861f9d81486f1362'
            'e1d8623ea117be3d2537cc7f7465cae6e45d0309a502a0ed2b3bd9cd41e14e0e'
            'c1f6a18b03d1612b60f8081428f00cfac5e66315fe9d42719f01cf5564deeeff')
