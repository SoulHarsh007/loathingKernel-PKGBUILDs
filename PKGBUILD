# Maintainer: korjjj <korjjj+aur[at]gmail[dot]com>

pkgname=gns3-server
pkgver=1.3.7
pkgrel=1
pkgdesc='GNS3 network simulator. Server package.'
arch=('any')
url='https://github.com/GNS3/gns3-server'
license=('GPL3')
makedepends=('python-setuptools')
depends=('python-netifaces' 'python-jsonschema' 'python-dateutil' 'python-aiohttp' 'python-jinja' 'python-raven')
optdepends=('dynamips: Cisco router emulator.'
            'vboxwrapper: VirtualBox wrapper for GNS3.'
            'iouyap: Bridge IOU to UDP, TAP and Ethernet.'
            'qemu: Used by GNS3 to run Cisco ASA, PIX and IDS.'
            'vpcs: Simple PC emulation for basic network operations.'
            'gns3-gui: graphical user interface for GNS3 server.'
)
install="${pkgname}.install"
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/GNS3/${pkgname}/archive/v${pkgver}.tar.gz"
        "${pkgname}@.service")
md5sums=('4549f94aeea503b2b431471c34da3a5c'
         'f602390385890dab14f68e5e0a8cac2d')

package() {
  cd ${srcdir}/${pkgname}-${pkgver}
  python setup.py install --root=${pkgdir} --optimize=1
  install -Dm644 ${srcdir}/${pkgname}-${pkgver}/LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
  install -Dm644 ${srcdir}/${pkgname}@.service ${pkgdir}/usr/lib/systemd/system/${pkgname}@.service
}

# vim:set ts=2 sw=2 et:
