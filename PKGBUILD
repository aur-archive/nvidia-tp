# Contributor: Missed <Jerry87905@gmail.com>

pkgname=nvidia-tp
pkgver=173.14.09
_kernver='2.6.25-tp'
pkgrel=1
pkgdesc="NVIDIA drivers for kernel26tp."
arch=('i686' 'x86_64')
[ "$CARCH" = "i686"   ] && ARCH=x86
[ "$CARCH" = "x86_64" ] && ARCH=x86_64
url="http://www.nvidia.com/"
depends=('kernel26tp>=2.6.25-1' 'kernel26tp<2.6.26' 'nvidia-utils')
conflicts=('nvidia-96xx' 'nvidia-71xx' 'nvidia-legacy')
license=('custom')
install=nvidia.install
source=(http://us.download.nvidia.com/XFree86/Linux-$ARCH/${pkgver}/NVIDIA-Linux-$ARCH-${pkgver}-pkg0.run)
md5sums=('20b4952c99e3312984793410cb06a609')
[ "$CARCH" = "x86_64" ] && md5sums=('223dedf255d74eaa2e63808586f030f1')

build()
{
  # Extract
  cd $startdir/src/
  sh NVIDIA-Linux-$ARCH-${pkgver}-pkg0.run --extract-only
  cd NVIDIA-Linux-$ARCH-${pkgver}-pkg0
  
  # Any extra patches are applied in here...

  cd usr/src/nv/
  ln -s Makefile.kbuild Makefile
  make SYSSRC=/lib/modules/${_kernver}/build module || return 1
  
  # install kernel module
  mkdir -p $startdir/pkg/lib/modules/${_kernver}/kernel/drivers/video/
  install -m644 nvidia.ko $startdir/pkg/lib/modules/${_kernver}/kernel/drivers/video/

  sed -i -e "s/KERNEL_VERSION='.*'/KERNEL_VERSION='${_kernver}'/" $startdir/*.install
} 
