# Maintainer: Doug Newgard <scimmia at archlinux dot org>

pkgname=chromium-widevine
pkgdesc='A browser plugin designed for the viewing of premium video content'
pkgver=4.10.1196.0
_chrome_ver=70.0.3538.102
_license_date=$(curl -sI https://www.google.com/intl/en/chrome/privacy/eula_text.html | sed -n '/^last-modified/ s/.*: //p' | date +"%Y%m%d" -f -)
_license_last=20181101
pkgrel=2
epoch=1
arch=('x86_64')
url='https://www.widevine.com/'
license=('custom')
options=('!strip')
source=("chrome-eula_text-$_license_date.html::https://www.google.com/intl/en/chrome/privacy/eula_text.html"
        "https://dl.google.com/linux/deb/pool/main/g/google-chrome-stable/google-chrome-stable_${_chrome_ver}-1_amd64.deb")
sha256sums=('22e323091aab9730fc9431376e63d95fe03e3df08a1ab7d913b67bd16a6c159b'
            '88979cf1d4c28deb079cf7fdb120b430d9b4b83f9eeeacf2b998c276ee342db6')

prepare() {
  bsdtar -x --strip-components 4 -f data.tar.xz opt/google/chrome/libwidevinecdm.so
}

pkgver() {
  awk 'match($0,/widevine.cdm.version\0Google\0ChromeCDM\0([0-9.]+)/,a) {print a[1];}' libwidevinecdm.so
}

package() {
  depends=('chromium' 'gcc-libs' 'glib2' 'glibc' 'nspr' 'nss')

  install -Dm644 libwidevinecdm.so -t "$pkgdir/usr/lib/chromium/"
  install -Dm644 chrome-eula_text-$_license_date.html "$pkgdir/usr/share/licenses/$pkgname/eula_text.html"
}
