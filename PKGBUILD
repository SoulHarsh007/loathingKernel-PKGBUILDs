# Maintainer: Damjan Georgievski <gdamjan@gmail.com>
pkgname=go2tv
pkgver=1.12.0
pkgrel=1
pkgdesc='cast your videos to UPnP/DLNA MediaRenderer'
arch=('x86_64')
url="https://github.com/alexballas/${pkgname}"
license=('MIT')
depends=('libglvnd')
makedepends=('go' 'libxcursor' 'libxrandr' 'libxinerama' 'libxi')
optdepends=('ffmpeg: transcoding support')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz")

build() {
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"
  export GOFLAGS="-buildmode=pie -trimpath -ldflags=-linkmode=external -mod=readonly -modcacherw"

  cd $pkgname-$pkgver
  go build -ldflags "-s -w" -o go2tv cmd/go2tv/go2tv.go
}

package() {
  install -Dm755 $pkgname-$pkgver/$pkgname   "$pkgdir"/usr/bin/$pkgname
  install -Dm644 $pkgname-$pkgver/LICENSE    "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

sha256sums=('17fb0823c608af0a558a9538bf03fd8638bfee7c68aa01c1b437ffa71cbf94b6')
