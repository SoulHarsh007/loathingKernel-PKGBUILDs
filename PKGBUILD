# Maintainer: Hyacinthe Cartiaux <hyacinthe.cartiaux@free.fr>
# Contributor: korjjj <korjjj+aur[at]gmail[dot]com>

pkgname=gns3-gui
pkgver=2.1.5
pkgrel=1
pkgdesc='GNS3 network simulator. Graphical user interface package.'
arch=('any')
url='https://github.com/GNS3/gns3-gui'
license=('GPL3')
groups=('gns3')
makedepends=('python-setuptools')
depends=('python-jsonschema' 'gns3-converter' 'python-raven' 'python-psutil' 'python-pyqt5' 'qt5-svg' 'qt5-websockets')
optdepends=('gns3-server: GNS3 backend. Manages emulators such as Dynamips, VirtualBox or Qemu/KVM.'
            'dynamips: Cisco router emulator.'
            'xterm: Default terminal emulator for CLI management of virtual instances.'
            'wireshark-qt: Live packet capture.')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/GNS3/${pkgname}/archive/v${pkgver}.tar.gz"
        'gns3.desktop')
sha256sums=('032faac3febc0032167bbbfaa9d73a9f7aee9811174b99044d52028eb30c2d24'
            '51e6db5b47e6af3d008d85e8c597755369fafb75ddb2af9e79a441f943f4c166')

package() {
  cd ${srcdir}/${pkgname}-${pkgver}
  python setup.py install --root=${pkgdir} --optimize=1
  install -Dm644 ${srcdir}/gns3.desktop ${pkgdir}/usr/share/applications/gns3.desktop
  install -Dm644 ${srcdir}/${pkgname}-${pkgver}/resources/images/gns3_icon_256x256.png ${pkgdir}/usr/share/pixmaps/gns3.png
  install -Dm644 ${srcdir}/${pkgname}-${pkgver}/LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
}

# vim:set ts=2 sw=2 et:
