# Maintainer: Eli Schwartz <eschwartz@archlinux.org>

# All my PKGBUILDs are managed at https://github.com/eli-schwartz/pkgbuilds

pkgname=pacman-static
pkgver=5.1.3
_cares_ver=1.15.0
_nghttp2_ver=1.36.0
_curlver=7.64.1
_sslver=1.1.1b
_xzver=5.2.4
_bzipver=1.0.6
_zstdver=1.3.8
_libarchive_ver=3.3.3
_gpgerrorver=1.36
_libassuanver=2.5.3
_gpgmever=1.13.0
pkgrel=2
pkgdesc="Statically-compiled pacman (to fix or install systems without libc)"
arch=('i686' 'x86_64' 'arm' 'armv6h' 'armv7h' 'aarch64')
url="https://www.archlinux.org/pacman/"
license=('GPL')
depends=('pacman')
makedepends=('musl' 'kernel-headers-musl')

# pacman
source=("https://sources.archlinux.org/other/pacman/pacman-${pkgver}.tar.gz"{,.sig})
validpgpkeys=('6645B0A8C7005E78DB1D7864F99FFE0FEAE999BD'  # Allan McRae <allan@archlinux.org>
              'B8151B117037781095514CA7BBDFFC92306B1121') # Andrew Gregory (pacman) <andrew@archlinux.org>
# nghttp2
source+=("https://github.com/nghttp2/nghttp2/releases/download/v$_nghttp2_ver/nghttp2-$_nghttp2_ver.tar.xz")
# c-ares
source+=("https://c-ares.haxx.se/download/c-ares-${_cares_ver}.tar.gz"{,.asc})
validpgpkeys+=('27EDEAF22F3ABCEB50DB9A125CC908FDB71E12C2') # Daniel Stenberg <daniel@haxx.se>
# curl
source+=("https://curl.haxx.se/download/curl-${_curlver}.tar.gz"{,.asc})
# openssl
source+=("https://www.openssl.org/source/openssl-${_sslver}.tar.gz"{,.asc}
         "ca-dir.patch")
validpgpkeys+=('8657ABB260F056B1E5190839D9C4D26D0E604491') # Matt Caswell <matt@openssl.org>
# xz
source+=("https://tukaani.org/xz/xz-${_xzver}.tar.gz"{,.sig})
validpgpkeys+=('3690C240CE51B4670D30AD1C38EE757D69184620') # Lasse Collin <lasse.collin@tukaani.org>
# bzip2
source+=("https://sources.archlinux.org/other/packages/bzip2/bzip2-${_bzipver}.tar.gz")
# zstd
source+=("https://github.com/facebook/zstd/releases/download/v${_zstdver}/zstd-${_zstdver}.tar.gz")
# libgpg-error
source+=("https://gnupg.org/ftp/gcrypt/libgpg-error/libgpg-error-${_gpgerrorver}.tar.bz2"{,.sig})
validpgpkeys+=('D8692123C4065DEA5E0F3AB5249B39D24F25E3B6'  # Werner Koch
               '031EC2536E580D8EA286A9F22071B08A33BD3F06') # NIIBE Yutaka (GnuPG Release Key) <gniibe@fsij.org>
# libassuan
source+=("https://gnupg.org/ftp/gcrypt/libassuan/libassuan-${_libassuanver}.tar.bz2"{,.sig})
# gpgme
source+=("https://www.gnupg.org/ftp/gcrypt/gpgme/gpgme-${_gpgmever}.tar.bz2"{,.sig})

# libarchive
source+=("libarchive-${_libarchive_ver}.tar.gz::https://github.com/libarchive/libarchive/archive/v${_libarchive_ver}.tar.gz")

sha512sums=('b556b6d01d651a675ce1e153ede776e682ca0eb671cd2be00d7b7c602504dd119291f38ef5c318e675b4ce865db7e1c57e0ebc157510f0fc72e656feb8947e54'
            'SKIP'
            '4e0d5c5cdb4f1b7e5f12790850237f36649af4aa9596033392725972e4e0e5a33bb78bd1aa0735e35e489b523b7e9a236a7b5847dfca69bd7583fcab36c13c76'
            'a1de6c5e7e1a6a13c926aae690e83d5caa51e7313d63da1cf2af6bc757c41d585aad5466bc3ba7b7f7793cb1748fa589f40972b196728851c8b059cfc8c3be50'
            'SKIP'
            'c8f8c4397e0e2975e7553f36637b7e7caa29d7953229dcf4d8051f9bae0cf55572d6e25fc27d9c34fe8783cf87893d96d447601c74662374b8bbd393b6cb6825'
            'SKIP'
            'b54025fbb4fe264466f3b0d762aad4be45bd23cd48bdb26d901d4c41a40bfd776177e02230995ab181a695435039dbad313f4b9a563239a70807a2e19ecf045d'
            'SKIP'
            '3857c298663728a465b5f95a3ef44547efbfb420d755e9dde7f20aa3905171b400e1c126d8db5c2b916c733bbd0724d8753cad16c9baf7b12dcd225a3ee04a97'
            'e5bf6eb88365d2dbdc774db49261fb9fae0544ed297891fc20f1ed223f4072cb0357cbd98146ac35b6d29410a12b6739bbd111cd57d4a225bef255ed46988578'
            'SKIP'
            '00ace5438cfa0c577e5f578d8a808613187eff5217c35164ffe044fbafdfec9e98f4192c02a7d67e01e5a5ccced630583ad1003c37697219b0f147343a3fdd12'
            '5c1c0a7a998b814a9edc1466f6d321b0d8ffcf927295fd5499137c9075a8823be03d98f61ea5212d1969f8d52b32e940b1cc10d1507d7702424ea2eea0e79a1b'
            '6e5f853f77dc04f0091d94b224cab8e669042450f271b78d0ea0219658d059c9cab1ab0eaa020a4227f451520b417fc340b85971a6f5e144fa69be57e15df346'
            'SKIP'
            'e7ccb651ea75b07b2e687d48d86d0ab83cba8e2af7f30da2aec794808e13e6ec93f21d607db50d3431f1c23cb3a07a2793b71170e69fa2f5a82cffb81961f617'
            'SKIP'
            '47a7a67dcc6d111cddd805d288d42e870948114a6dc09ce0675ad8b3d1580bbc2a683e1e70cb2f416919cf2129c72a9ff30e2e3b9527809d04e863cc1f87267b'
            'SKIP'
            '10063764b610c0c966ba0177cac0d2cb781e297a45545cc8a587741513089af26f40769670894c86e7985b73c47e9cb985253bc3bef3a12fa83fe2a6a30acb6d')

export LDFLAGS="$LDFLAGS -static"
export CC=musl-gcc
export CXX=musl-gcc

# https://www.openwall.com/lists/musl/2014/11/05/3
# fstack-protector and musl do not get along but only on i686
if [[ $CARCH = i686 ]]; then
    # silly build systems have configure checks or buildtime programs that don't CFLAGS but do do CC
    export CC="musl-gcc -fno-stack-protector"
    export CXX="musl-gcc -fno-stack-protector"
    export CFLAGS="${CFLAGS/-fstack-protector-strong/}"
    export CXXFLAGS="${CXXFLAGS/-fstack-protector-strong/}"
fi

prepare() {
    cd "${srcdir}"/libarchive-${_libarchive_ver}
    autoreconf -fi
}

build() {
    export PKG_CONFIG_PATH="${srcdir}"/temp/usr/lib/pkgconfig
    export PATH="${srcdir}/temp/usr/bin:${PATH}"

    # openssl
    cd "${srcdir}"/openssl-${_sslver}
    case ${CARCH} in
        x86_64)
            openssltarget='linux-x86_64'
            optflags='enable-ec_nistp_64_gcc_128'
            ;;
        i686)
            openssltarget='linux-elf'
            optflags=''
            ;;
        arm|armv6h|armv7h)
            openssltarget='linux-armv4'
            optflags=''
            ;;
        aarch64)
            openssltarget='linux-aarch64'
            optflags='no-afalgeng'
            ;;
    esac
    # mark stack as non-executable: http://bugs.archlinux.org/task/12434
    ./Configure --prefix="${srcdir}"/temp/usr \
                --openssldir=/etc/ssl \
                --libdir=lib \
                -static \
                no-ssl3-method \
                ${optflags} \
                "${openssltarget}" \
                "-Wa,--noexecstack ${CPPFLAGS} ${CFLAGS} ${LDFLAGS}"
    make build_libs
    make install_dev

    # xz
    cd "${srcdir}"/xz-${_xzver}
    ./configure --prefix="${srcdir}"/temp/usr \
                --disable-shared
    cd src/liblzma
    make
    make install

    # bzip2
    cd "${srcdir}"/bzip2-${_bzipver}
    sed -i "s|-O2|${CFLAGS}|g" Makefile
    make libbz2.a
    install -Dvm644 bzlib.h "${srcdir}"/temp/usr/include/
    install -Dvm644 libbz2.a "${srcdir}"/temp/usr/lib/

    cd "${srcdir}"/zstd-${_zstdver}/lib
    make libzstd.a
    make PREFIX="${srcdir}"/temp/usr install-pc install-static install-includes

    # libarchive
    cd "${srcdir}"/libarchive-${_libarchive_ver}
    CPPFLAGS="-I${srcdir}/temp/usr/include" CFLAGS="-L${srcdir}/temp/usr/lib" \
        ./configure --prefix="${srcdir}"/temp/usr \
                    --without-xml2 \
                    --without-nettle \
                    --disable-{bsdtar,bsdcat,bsdcpio} \
                    --without-expat \
                    --disable-shared
    make
    make install-{includeHEADERS,libLTLIBRARIES,pkgconfigDATA,includeHEADERS}

    # nghttp2
    cd "${srcdir}"/nghttp2-${_nghttp2_ver}
    ./configure --prefix="${srcdir}"/temp/usr \
        --disable-shared \
        --disable-examples \
        --disable-python-bindings
    make -C lib
    make -C lib install

    # c-ares
    # needed for curl, which does not use it in the repos
    # but seems to be needed for static builds
    cd "${srcdir}"/c-ares-${_cares_ver}
    ./configure --prefix="${srcdir}"/temp/usr \
        --disable-shared
    make
    make install-{libcares_laHEADERS,libLTLIBRARIES,pkgconfigDATA}

    # curl
    cd "${srcdir}"/curl-${_curlver}
    # c-ares is not detected via pkg-config :(
    ./configure --prefix="${srcdir}"/temp/usr \
                --disable-shared \
                --with-ca-bundle=/etc/ssl/certs/ca-certificates.crt \
                --disable-{dict,gopher,imap,imaps,ldap,ldaps,manual,pop3,pop3s,rtsp,scp,sftp,smb,smbs,smtp,smtps,telnet,tftp} \
                --without-{brotli,libidn2,librtmp,libssh2} \
                --disable-libcurl-option \
                --with-ssl \
                --enable-ares="${srcdir}"/temp/usr
    make -C lib
    make install-pkgconfigDATA
    make -C lib install
    make -C include install

    # libgpg-error
    cd "${srcdir}"/libgpg-error-${_gpgerrorver}
    ./configure --prefix="${srcdir}"/temp/usr \
        --disable-shared
    make -C src
    make -C src install-{{,dist_}binSCRIPTS,libLTLIBRARIES,nodist_includeHEADERS,pkgconfigDATA}

    # libassuan
    cd "${srcdir}"/libassuan-${_libassuanver}
    ./configure --prefix="${srcdir}"/temp/usr \
        --disable-shared
    make -C src
    make -C src install-{binSCRIPTS,libLTLIBRARIES,nodist_includeHEADERS,pkgconfigDATA}

    # gpgme
    cd "${srcdir}"/gpgme-${_gpgmever}
    ./configure --prefix="${srcdir}"/temp/usr \
        --disable-fd-passing \
        --disable-shared \
        --disable-languages
    make -C src
    make -C src install-{binSCRIPTS,libLTLIBRARIES,nodist_includeHEADERS,pkgconfigDATA}

    # ew libtool
    rm "${srcdir}"/temp/usr/lib/lib*.la
    export PKG_CONFIG='pkg-config --static'

    # Finally, it's a pacman!
    cd "${srcdir}"/pacman-${pkgver}
    ./configure --prefix=/usr \
                --libdir=/usr/lib/pacman/lib \
                --sysconfdir=/etc \
                --localstatedir=/var \
                --program-suffix=-static \
                --with-scriptlet-shell=/usr/bin/bash \
                --with-ldconfig=/usr/bin/ldconfig \
                --disable-shared \
                --disable-doc
    make V=1 AM_LDFLAGS=-all-static
}

package() {
    cd "${srcdir}"/pacman-${pkgver}
    make -C lib/libalpm  DESTDIR="${pkgdir}" install-libLTLIBRARIES install-pkgconfigDATA
    make -C src/util  DESTDIR="${pkgdir}" install
    make -C src/pacman  DESTDIR="${pkgdir}" install-binPROGRAMS

    cp -a "${srcdir}"/temp/usr/{bin,include,lib} "${pkgdir}"/usr/lib/pacman/
    sed -i "s@${srcdir}/temp/usr@/usr/lib/pacman@g" \
        "${pkgdir}"/usr/lib/pacman/lib/pkgconfig/*.pc \
        "${pkgdir}"/usr/lib/pacman/bin/*
}
