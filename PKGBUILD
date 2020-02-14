# Maintainer: Eli Schwartz <eschwartz@archlinux.org>

# All my PKGBUILDs are managed at https://github.com/eli-schwartz/pkgbuilds

pkgname=pacman-static
pkgver=5.2.1
_cares_ver=1.15.0
_nghttp2_ver=1.39.2
_curlver=7.68.0
_sslver=1.1.1d
_zlibver=1.2.11
_xzver=5.2.4
_bzipver=1.0.8
_zstdver=1.4.4
_libarchive_ver=3.4.2
_gpgerrorver=1.37
_libassuanver=2.5.3
_gpgmever=1.13.1
pkgrel=3
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
validpgpkeys+=('8657ABB260F056B1E5190839D9C4D26D0E604491'  # Matt Caswell <matt@openssl.org>
               '7953AC1FBC3DC8B3B292393ED5E9E43F7DF9EE8C') # Richard Levitte <levitte@openssl.org>
# zlib
source+=("https://zlib.net/zlib-${_zlibver}.tar.gz"{,.asc})
validpgpkeys+=('5ED46A6721D365587791E2AA783FCD8E58BCAFBA') # Mark Adler <madler@alumni.caltech.edu>
# xz
source+=("https://tukaani.org/xz/xz-${_xzver}.tar.gz"{,.sig})
validpgpkeys+=('3690C240CE51B4670D30AD1C38EE757D69184620') # Lasse Collin <lasse.collin@tukaani.org>
# bzip2
source+=("https://sourceware.org/pub/bzip2/bzip2-${_bzipver}.tar.gz"{,.sig})
validpgpkeys+=('EC3CFE88F6CA0788774F5C1D1AA44BE649DE760A') # Mark Wielaard <mark@klomp.org>
# zstd
source+=("zstd-${_zstdver}.tar.gz::https://github.com/facebook/zstd/archive/v${_zstdver}.tar.gz")
# libgpg-error
source+=("https://gnupg.org/ftp/gcrypt/libgpg-error/libgpg-error-${_gpgerrorver}.tar.bz2"{,.sig})
validpgpkeys+=('D8692123C4065DEA5E0F3AB5249B39D24F25E3B6'  # Werner Koch
               '031EC2536E580D8EA286A9F22071B08A33BD3F06') # NIIBE Yutaka (GnuPG Release Key) <gniibe@fsij.org>
# libassuan
source+=("https://gnupg.org/ftp/gcrypt/libassuan/libassuan-${_libassuanver}.tar.bz2"{,.sig})
# gpgme
source+=("https://www.gnupg.org/ftp/gcrypt/gpgme/gpgme-${_gpgmever}.tar.bz2"{,.sig})
# libarchive
source+=("https://github.com/libarchive/libarchive/releases/download/v${_libarchive_ver}/libarchive-${_libarchive_ver}.tar.xz"{,.asc})
validpgpkeys+=('A5A45B12AD92D964B89EEE2DEC560C81CEC2276E') # Martin Matuska <mm@FreeBSD.org>

sha512sums=('7814420b8d71090313f1bc7d9a513138bda74c5cbcb43d9741acc27ea7b4d180a38848a7d7059969cc7afed1b108d26ba2622a16d8761566357c50a5da456981'
            'SKIP'
            'd8c971543e3e87736dfafebca55e9ecd0644e304c9731edaccba34170205824476595861a439077289b438ad489dd6008dedf2c6b2c111920300329be1b1bf34'
            'a1de6c5e7e1a6a13c926aae690e83d5caa51e7313d63da1cf2af6bc757c41d585aad5466bc3ba7b7f7793cb1748fa589f40972b196728851c8b059cfc8c3be50'
            'SKIP'
            '58b42c08b1cf4cb6e68f8e469d5b5f6298eebe286ba2677ad29e1a7eefd15b8609af54544f4c5a7dadebbd3b23bd77700830f2f60fbea7ae3f2f306e640010b0'
            'SKIP'
            '2bc9f528c27fe644308eb7603c992bac8740e9f0c3601a130af30c9ffebbf7e0f5c28b76a00bbb478bad40fbe89b4223a58d604001e1713da71ff4b7fe6a08a7'
            'SKIP'
            '3857c298663728a465b5f95a3ef44547efbfb420d755e9dde7f20aa3905171b400e1c126d8db5c2b916c733bbd0724d8753cad16c9baf7b12dcd225a3ee04a97'
            '73fd3fff4adeccd4894084c15ddac89890cd10ef105dd5e1835e1e9bbb6a49ff229713bd197d203edfa17c2727700fce65a2a235f07568212d820dca88b528ae'
            'SKIP'
            'e5bf6eb88365d2dbdc774db49261fb9fae0544ed297891fc20f1ed223f4072cb0357cbd98146ac35b6d29410a12b6739bbd111cd57d4a225bef255ed46988578'
            'SKIP'
            '083f5e675d73f3233c7930ebe20425a533feedeaaa9d8cc86831312a6581cefbe6ed0d08d2fa89be81082f2a5abdabca8b3c080bf97218a1bd59dc118a30b9f3'
            'SKIP'
            '8209837e8eb14e474dfe21d5511085f46cef93b03ab77613fd41e7b8be652418231c38852669c8e0b55b78ad41ea2cb8008d0da122a83f8f27e32b5c86f045cf'
            'fa12977237fcc872e944cda39ca43ee7d2cc9c52e243ede6077f4a31ae135e322dc848b4b55cffdc4ec53f27601ba30ddb368b090a94cd00d9345a55b323f179'
            'SKIP'
            'e7ccb651ea75b07b2e687d48d86d0ab83cba8e2af7f30da2aec794808e13e6ec93f21d607db50d3431f1c23cb3a07a2793b71170e69fa2f5a82cffb81961f617'
            'SKIP'
            '11de670c6cf512508103fe67af56d9fbb2a9dda6fc6fa3cd321371bbe337c7c2c81913ca557d07187adb2a63d37ea1a44da97ab22345bbe6022c405d0cb083b8'
            'SKIP'
            'c144f88e3149923e2657ab3f6c9d3457ac779f856b1c6934b0012dbb3a8cefaa2873061f3060720ee52d67a78aa5e0afff17e0f1282c032322f35a9bbfcccc57'
            'SKIP')
b2sums=('be5a11624eecfe6c5a54088ce8872a1f2e24f2ac3f5a32a848a115b873b8ac3ee2a3aae5ab9f706be4fc359ef5cbde374688f012f799ff7ecda8669797160a52'
        'SKIP'
        '4569774c33f17d51ac889c385697fcead82106db421399ceb22ad2aafabe64a576445d9272adcf37e2fec47cdd6ac1dc6423efd49012ca7be0aa2087609a0397'
        'c4028bb2840af23274b79c73600bfcf73a348c7ab63ae3c215829e0fe2cf149f4ad38a3ec657c3997bad818ced3cacaed0579dd0dd2ef42eaffd074bdc4f22ed'
        'SKIP'
        '2dec41e9acef615e5e4db2b2ff44a4c72c4c2a51be9a3020134ae8f36f8563ff269f45e60c94134fd33cc923e2dcdb806575bef2499aaaf9fb4e921522ee9be1'
        'SKIP'
        'd3155f07b487ebd8dd4fe25396c874f9af18b5cfd7e622298d29c4f2c8ce14ad4534609d321314a4bcd0d44414e1306190340daaacd3c8fca061c04498446244'
        'SKIP'
        'e2ff99e8236487f43171c771d0ee89137b73f3d0b2756bcb0d6525c810ffa9f5a3763c3744327fb47cef21eabfc50fff96632f4bbe2cd244206a99daffa0c25a'
        '6bfc4bca5dcadba8a0d4121a2b3ed0bfe440c261003521862c8e6381f1a6f0a72d3fc037351d30afd7ef321e8e8d2ec817c046ac749f2ca0c97fbdc2f7e840b7'
        'SKIP'
        '877242324afd3c7eb21d3a9414c53843f4d1bb089206e8e545e280b32ff5372f7fb4a1b0c27cb6fdf0d0a27a668e9772ecc3fffc181df95d081ca9c2e987b83b'
        'SKIP'
        '22ab3acd84f4db8c3d6f59340c252faedfd4447cea00dafbd652e65b6cf8a20adf6835c22e58563004cfafdb15348c924996230b4b23cae42da5e25eeac4bdad'
        'SKIP'
        'e21841a53b6c60703e5500cfc2a02923c4c3e57975aa57e1060310171e0d83d7c8eda1bd0510d5736db5c310d76847d2105ac5f614867fc3a9dc3086a035dfd7'
        '70666749aa0156652405ee15e4307f29bdf748f06728da5c672c0208053e0d3a041aaef882b263dd828e2aa7dd8a2f77334447af2c499f81f7602150d84f593f'
        'SKIP'
        'ae3a5a9a03e85d62cf87271cd4a0718a2b89a4f90ea814837913e4b2bb6e5af9746e766d99685cc0cc3a801efaee597e491a2bc03d42ac26059580ea4680fd7a'
        'SKIP'
        '17fff261ab76b72e096aa42cc847443bfd3bbf0eb6d04af1d38561ddce1d11cfe9a98b6ced268b28f33e2cb7d900a9e6b3dfc56f1c784a021dbefbf493522e70'
        'SKIP'
        'b309c8283d65cc975569926ad866d49df53f386a50c4433ad9557f62693d48d3768ad68147241d748d2b5f86c6d26f381bbdbf22b0dbd961468a1cba2e62a922'
        'SKIP')

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

# keep using xz-compressed packages, because one use of the package is to
# recover on systems with broken zstd support in libarchive
[[ $PKGEXT = .pkg.tar.zst ]] && PKGEXT=.pkg.tar.xz

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

    # zlib
    cd "${srcdir}/"zlib-${_zlibver}
    ./configure --prefix="${srcdir}"/temp/usr \
                --static
    make libz.a
    make install

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
