# Maintainer: Doug Newgard <scimmia at archlinux dot info>

pkgname=chromium-widevine
pkgdesc='A browser plugin designed for the viewing of premium video content'
pkgver=1.4.8.824
pkgrel=2
epoch=1
arch=('i686' 'x86_64')
url='http://www.google.com/chrome'
license=('custom:chrome')
options=('!strip')
_chrome_ver=49.0.2623.75
depends=("chromium")
source=('chrome-eula_text.html::https://www.google.com/chrome/intl/en/eula_text.html')
source_i686=("http://mirror.pcbeta.com/google/chrome/deb/pool/main/g/google-chrome-stable/google-chrome-stable_48.0.2564.116-1_i386.deb")
source_x86_64=("https://dl.google.com/linux/deb/pool/main/g/google-chrome-stable/google-chrome-stable_${_chrome_ver}-1_amd64.deb")
sha256sums=('b35811bb330576631e64f7885c66720e0be4ca81afb04328b3a0f288a708e37f')
sha256sums_i686=('7401ad3698a28bf2b45e350fd2b941c44cb51dbb3f87b0e7dd1a2da72c42f594')
sha256sums_x86_64=('5016c5f0162013baeabae3313b6dee7518a08a5da178c25834feb64aab2c1107')

pkgver() {
  bsdtar -xf data.tar.xz opt/google/chrome/{chrome,libwidevinecdm.so}
  strings opt/google/chrome/chrome | sed -n '/ (version:/{n;p}'
}

package() {
  install -Dm644 opt/google/chrome/libwidevinecdm.so -t "$pkgdir/usr/lib/chromium/"
  install -Dm644 chrome-eula_text.html "$pkgdir/usr/share/licenses/$pkgname/eula_text.html"
}
