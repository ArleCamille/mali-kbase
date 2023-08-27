# Mali Bifrost kernel driver for mainline kernel (linux-hikey960)
# Maintainer: Hyeseon Oh <okw1003@gmail.com>

buildarch=8

pkgname=mali-kbase
pkgdesc="Mali Bifrost kernel driver for linux-hikey960"
pkgver=r44p0_01eac0
pkgrel=1
arch=('aarch64')
url='https://developer.arm.com/downloads/-/mali-drivers/bifrost-kernel'
license=('GPL2')
makedepends=('xmlto' 'docbook-xsl' 'kmod' 'inetutils' 'bc' 'git' 'dtc' 'linux-hikey960-headers')
install=${pkgname}.install
_filename="BX304L01B-SW-99002-${pkgver//_/-}.tar"
_revision='5e09ea55-e10b-41c5-beb7-cc0f7d4457dc'
source=("${_filename}::https://developer.arm.com/-/media/Files/downloads/mali-drivers/kernel/mali-bifrost-gpu/${_filename}?rev=${_revision//-/}&revision=${_revision}"
	"${pkgname}.conf")
md5sums=('fe6f79845ca9fbd1fd50e58e8f447fa1'
	 '3fb0f882fe0d474f2b3f038d419e469e')
_kernver="${KERNVER:-`uname -r`}"
_kernsrc="${KERNSRC:-"/usr/lib/modules/${_kernver}/build"}"
install=${pkgname}.install
options=('!strip')

build() {
	cd "${srcdir}/driver/product/kernel/drivers/gpu/arm/midgard"

	unset LDFLAGS
	make ${MAKEFLAGS} KERNEL_SRC="${_kernsrc}" CONFIG_MALI_PLATFORM_NAME=devicetree CONFIG_MALI_MIDGARD=m
}

package() {
	# Install Mali kernel module
	install -Dm755 "${srcdir}/driver/product/kernel/drivers/gpu/arm/midgard/${pkgname//-/_}.ko" "${pkgdir}"/usr/lib/modules/${KERNVER}/extramodules/${pkgname//-/_}.ko

	# Blacklists conflicting module
	install -Dm644 ${pkgname}.conf "${pkgdir}/usr/lib/modprobe.d/${pkgname}.conf"
}

