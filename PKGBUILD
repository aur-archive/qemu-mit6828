# Contributor: Tobias Powalowski <tpowa@archlinux.org>
# Maintainer: Liu Zhe <cruise.pas@gmail.com>

pkgname=qemu-mit6828
pkgver=2.3.0
pkgrel=1
pkgdesc="QEMU is a generic and open source processor emulator which achieves a good emulation speed by using dynamic translation. This version is specified for MIT's operating system lesson(6.828)"
arch=('i686' 'x86_64')
license=('GPL2' 'LGPL2.1')
url="http://wiki.qemu.org/Index.html"
makedepends=('git' 'python2')
depends=('seabios' 'libcacard' 'sdl')
conflicts=('qemu')
source=(git://github.com/geofft/qemu.git#branch=6.828-${pkgver})
md5sums=('SKIP')

build()
{
    cd ${srcdir}/qemu
    ./configure --prefix=/usr \
                --sysconfdir=/etc \
                --libexecdir=/usr/lib/qemu \
                --target-list="i386-softmmu x86_64-softmmu" \
                --python=/bin/python2
    make
}

package() {
  cd ${srcdir}/qemu
  make DESTDIR=${pkgdir} libexecdir=/usr/lib/qemu install

  # provided by seabios package
  rm ${pkgdir}/usr/share/qemu/bios.bin
  rm ${pkgdir}/usr/share/qemu/acpi-dsdt.aml
  rm ${pkgdir}/usr/share/qemu/q35-acpi-dsdt.aml
  rm ${pkgdir}/usr/share/qemu/vgabios-cirrus.bin
  rm ${pkgdir}/usr/share/qemu/vgabios-qxl.bin
  rm ${pkgdir}/usr/share/qemu/vgabios-stdvga.bin
  rm ${pkgdir}/usr/share/qemu/vgabios-vmware.bin

  # provided by libcacard package
  rm -rf ${pkgdir}/usr/include/cacard
  rm -rf ${pkgdir}/usr/lib/libcacard*
  rm -rf ${pkgdir}/usr/lib/pkgconfig/libcacard.pc
  rm -rf ${pkgdir}/usr/bin/vscclient

  rm -r ${pkgdir}/usr/var

  rmdir ${pkgdir}/usr/include
  rmdir ${pkgdir}/usr/lib/pkgconfig

  ln -s qemu-system-i386 ${pkgdir}/usr/bin/qemu
}
