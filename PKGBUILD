# Maintainer: Florian Dejonckheere <florian@floriandejonckheere.be>
# Contributor: Robert Ransom <rransom.8774@gmail.com>
# Contributor: Corrado Primier <bardo@aur.archlinux.org>
# Contributor: William Rea <sillywilly@gmail.com>
# Contributor: Daniel J Griffiths <ghost1227@archlinux.us>

pkgname=paman
pkgver=0.9.4
pkgrel=6
pkgdesc='Inspects and alters the state of the PulseAudio sound server'
arch=('i686' 'x86_64')
url='http://0pointer.de/lennart/projects/paman'
license=('GPL')
depends=('libglademm' 'pulseaudio')
changelog=ChangeLog
source=("http://0pointer.de/lennart/projects/paman/${pkgname}-${pkgver}.tar.gz")
md5sums=('4a77b129b0de8d261f2794ce3db518cc')

prepare()
{
	cd "${srcdir}/${pkgname}-${pkgver}"
	CXXFLAGS="-std=c++11 -O2" ./configure --prefix=/usr --disable-lynx
}

build()
{
	cd "${srcdir}/${pkgname}-${pkgver}"
	make
}

package()
{
	cd "${srcdir}/${pkgname}-${pkgver}"
	make DESTDIR=${pkgdir} install
}
