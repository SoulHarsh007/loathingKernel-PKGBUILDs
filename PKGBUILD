# Maintainer: Otreblan <otreblain@gmail.com>

# Remember to activate multilib for proton.
# It's dependencies requiere to be build in this order:
# wine -> vkd3d-valve -> wine-valve -> proton
pkgname=legendary
pkgver=0.20.21
pkgrel=1
pkgdesc="A free and open-source replacement for the Epic Games Launcher "
arch=('any')
url="https://github.com/derrod/legendary"
license=('GPL3')
groups=()
depends=("python-requests" "python-wheel" "python-setuptools")
makedepends=()
checkdepends=()
optdepends=(
	"proton: Windows binaries support"
	"python-pywebview: Login support"
	"python-cairo: Login support (gtk)"
	"python-gobject: Login support (gtk)"
	"webkit2gtk: Login support (gtk)"
)
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
noextract=()
sha256sums=('44a3a070c109731297df27f875744dc09345bcea64497b721352a931295a21ca')

build() {
	cd "$srcdir/$pkgname-$pkgver"

	python setup.py build
}

package() {
	cd "$srcdir/$pkgname-$pkgver"

	python setup.py install --root="$pkgdir/" --optimize=1 --skip-build
}
