# Maintainer: Jan de Groot <jgc@archlinux.org>
# Maintainer: Andreas Radke <andyrtr@archlinux.org>

pkgbase=mesa
pkgname=('mesa' 'libgl' 'libgles' 'libegl' 'ati-dri' 'intel-dri' 'unichrome-dri' 'mach64-dri' 'mga-dri' 'r128-dri' 'savage-dri' 'sis-dri' 'tdfx-dri' 'nouveau-dri')

#_git=true
_git=false

if [ "${_git}" = "true" ]; then
    pkgver=7.10.0.git20110215
  else
    pkgver=7.10.2
fi
pkgrel=2
arch=('i686' 'x86_64')
makedepends=('glproto>=1.4.12' 'pkgconfig' 'libdrm>=2.4.23' 'libxxf86vm>=1.1.0' 'libxdamage>=1.1.3' 'expat>=2.0.1' 'libx11>=1.3.5' 'libxt>=1.0.8' 
             'gcc-libs>=4.5' 'dri2proto=2.3' 'python2' 'libxml2' 'imake')
url="http://mesa3d.sourceforge.net"
license=('custom')
source=(LICENSE gnome-shell-shader-fix.patch)
if [ "${_git}" = "true" ]; then
	# mesa git shot from 7.10 branch - see for state: http://cgit.freedesktop.org/mesa/mesa/commit/?h=7.10&id=cc1636b6db85604510f97f8a37d7fd0ecf453866
	source=(${source[@]} 'ftp://ftp.archlinux.org/other/mesa/mesa-cc1636b6db85604510f97f8a37d7fd0ecf453866.tar.bz2')
  else
	source=(${source[@]} "ftp://ftp.freedesktop.org/pub/mesa/${pkgver}/MesaLib-${pkgver}.tar.bz2"
)
fi
md5sums=('5c65a0fe315dd347e09b1f2826a1df5a'
         '3ec78f340f9387abd7a37b195e764cbf'
         'f5de82852f1243f42cc004039e10b771')

build() {
if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*   
    autoreconf -vfi
  else
    cd "${srcdir}/Mesa-${pkgver}" 
fi

#backport from master to fix gnome-shell shader
#https://bugs.freedesktop.org/show_bug.cgi?id=35714
patch -Np1 -i "${srcdir}/gnome-shell-shader-fix.patch"

if [ "${_git}" = "true" ]; then
    ./autogen.sh --prefix=/usr \
    --with-dri-driverdir=/usr/lib/xorg/modules/dri \
    --enable-gallium-radeon \
    --enable-gallium-r600 \
    --enable-gallium-nouveau \
    --enable-gallium-swrast \
    --enable-glx-tls \
    --with-driver=dri \
    --enable-xcb \
    --with-state-trackers=dri,glx \
    --disable-glut \
    --enable-gles1 \
    --enable-gles2 \
    --enable-egl \
    --disable-gallium-egl
  else
    ./configure --prefix=/usr \
    --with-dri-driverdir=/usr/lib/xorg/modules/dri \
    --enable-gallium-radeon \
    --enable-gallium-r600 \
    --enable-gallium-nouveau \
    --enable-gallium-swrast \
    --enable-glx-tls \
    --with-driver=dri \
    --enable-xcb \
    --with-state-trackers=dri,glx \
    --disable-glut \
    --enable-gles1 \
    --enable-gles2 \
    --enable-egl \
    --disable-gallium-egl
fi

  make
}

package_libgl() {
  depends=('libdrm>=2.4.22' 'libxxf86vm>=1.1.0' 'libxdamage>=1.1.3' 'expat>=2.0.1')
  pkgdesc="Mesa 3-D graphics library and DRI software rasterizer"

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*   
  else
    cd "${srcdir}/Mesa-${pkgver}" 
fi
  install -m755 -d "${pkgdir}/usr/lib"
  install -m755 -d "${pkgdir}/usr/lib/xorg/modules/extensions"

  bin/minstall lib/libGL.so* "${pkgdir}/usr/lib/"

  cd src/mesa/drivers/dri
  #make -C swrast DESTDIR="${pkgdir}" install
if [ "${_git}" = "true" ]; then
    make -C ${srcdir}/mesa-*/src/gallium/targets/dri-swrast DESTDIR="${pkgdir}" install
  else
    make -C ${srcdir}/Mesa-${pkgver}/src/gallium/targets/dri-swrast DESTDIR="${pkgdir}" install
fi
  ln -s swrastg_dri.so "${pkgdir}/usr/lib/xorg/modules/dri/swrast_dri.so"
  ln -s libglx.xorg "${pkgdir}/usr/lib/xorg/modules/extensions/libglx.so"

  install -m755 -d "${pkgdir}/usr/share/licenses/libgl"
  install -m644 "${srcdir}/LICENSE" "${pkgdir}/usr/share/licenses/libgl/"
}

package_libgles() {
  depends=('libgl')
  pkgdesc="Mesa GLES libraries and headers"

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*   
  else
    cd "${srcdir}/Mesa-${pkgver}" 
fi
  install -m755 -d "${pkgdir}/usr/lib"
  install -m755 -d "${pkgdir}/usr/lib/pkgconfig"
  install -m755 -d "${pkgdir}/usr/include"
  install -m755 -d "${pkgdir}/usr/include/GLES"
  install -m755 -d "${pkgdir}/usr/include/GLES2"
  bin/minstall lib/libGLESv* "${pkgdir}/usr/lib/"
  bin/minstall src/mapi/es1api/glesv1_cm.pc "${pkgdir}/usr/lib/pkgconfig/"
  bin/minstall src/mapi/es2api/glesv2.pc "${pkgdir}/usr/lib/pkgconfig/"
  bin/minstall include/GLES/* "${pkgdir}/usr/include/GLES/"
  bin/minstall include/GLES2/* "${pkgdir}/usr/include/GLES2/"
  bin/minstall include/GLES2/* "${pkgdir}/usr/include/GLES2/"

  install -m755 -d "${pkgdir}/usr/share/licenses/libgles"
  install -m644 "${srcdir}/LICENSE" "${pkgdir}/usr/share/licenses/libgles/"
}

package_libegl() {
  depends=('libgl')
  pkgdesc="Mesa libEGL libraries and headers"

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*   
  else
    cd "${srcdir}/Mesa-${pkgver}" 
fi
  install -m755 -d "${pkgdir}/usr/lib"
  install -m755 -d "${pkgdir}/usr/lib/egl"
  install -m755 -d "${pkgdir}/usr/lib/pkgconfig"
  install -m755 -d "${pkgdir}/usr/include"
  install -m755 -d "${pkgdir}/usr/include/"
  install -m755 -d "${pkgdir}/usr/include/EGL"
  install -m755 -d "${pkgdir}/usr/include/KHR"
  install -m755 -d "${pkgdir}/usr/share"
  install -m755 -d "${pkgdir}/usr/share/doc"
  install -m755 -d "${pkgdir}/usr/share/doc/libegl"
  bin/minstall lib/libEGL.so* "${pkgdir}/usr/lib/"
  bin/minstall lib/egl/* "${pkgdir}/usr/lib/egl/"
  bin/minstall src/egl/main/egl.pc "${pkgdir}/usr/lib/pkgconfig/"
  bin/minstall include/EGL/* "${pkgdir}/usr/include/EGL/"
  bin/minstall include/KHR/khrplatform.h "${pkgdir}/usr/include/KHR/"
  bin/minstall docs/egl.html "${pkgdir}/usr/share/doc/libegl/"

  install -m755 -d "${pkgdir}/usr/share/licenses/libegl"
  install -m644 "${srcdir}/LICENSE" "${pkgdir}/usr/share/licenses/libegl/"
}
package_mesa() {
  depends=('libgl' 'libx11>=1.3.5' 'libxt>=1.0.8' 'gcc-libs>=4.5' 'dri2proto=2.3' 'libdrm>=2.4.22' 'glproto>=1.4.12')
  optdepends=('opengl-man-pages: for the OpenGL API man pages')
  pkgdesc="Mesa 3-D graphics libraries and include files"

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*   
  else
    cd "${srcdir}/Mesa-${pkgver}" 
fi
  make DESTDIR="${pkgdir}" install

  rm -f "${pkgdir}/usr/lib/libGL.so"*
  rm -f "${pkgdir}/usr/lib/libGLESv"*
  rm -f "${pkgdir}/usr/lib/libEGL"*
  rm -rf "${pkgdir}/usr/lib/egl"
  rm -f ${pkgdir}/usr/lib/pkgconfig/{glesv1_cm.pc,glesv2.pc,egl.pc}
  rm -rf "${pkgdir}/usr/lib/xorg"
  rm -f "${pkgdir}/usr/include/GL/glew.h"
  rm -f "${pkgdir}/usr/include/GL/glxew.h"
  rm -f "${pkgdir}/usr/include/GL/wglew.h"
  rm -f "${pkgdir}/usr/include/GL/glut.h"
  rm -rf ${pkgdir}/usr/include/{GLES,GLES2,EGL,KHR}

  install -m755 -d "${pkgdir}/usr/share/licenses/mesa"
  install -m644 "${srcdir}/LICENSE" "${pkgdir}/usr/share/licenses/mesa/"
}

package_ati-dri() {
  depends=("libgl=${pkgver}")
  pkgdesc="Mesa DRI + Gallium3D r300 drivers for AMD/ATI Radeon"
  conflicts=('xf86-video-ati<6.9.0-6')

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*/src/mesa/drivers/dri
  else
    cd "${srcdir}/Mesa-${pkgver}/src/mesa/drivers/dri"
fi
  make -C radeon DESTDIR="${pkgdir}" install
  make -C r200 DESTDIR="${pkgdir}" install
  # classic mesa driver for R300 r300_dri.so
  #make -C r300 DESTDIR="${pkgdir}" install  <------- deprecated
  # gallium3D driver for R300 r300_dri.so
if [ "${_git}" = "true" ]; then
    make -C ${srcdir}/mesa-*/src/gallium/targets/dri-r300 DESTDIR="${pkgdir}" install
    make -C ${srcdir}/mesa-*/src/gallium/targets/dri-r600 DESTDIR="${pkgdir}" install
  else
    make -C ${srcdir}/Mesa-${pkgver}/src/gallium/targets/dri-r300 DESTDIR="${pkgdir}" install
    make -C ${srcdir}/Mesa-${pkgver}/src/gallium/targets/dri-r600 DESTDIR="${pkgdir}" install
fi
  #make -C r600 DESTDIR="${pkgdir}" install
}

package_intel-dri() {
  depends=("libgl=${pkgver}")
  pkgdesc="Mesa DRI drivers for Intel"

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*/src/mesa/drivers/dri
  else
    cd "${srcdir}/Mesa-${pkgver}/src/mesa/drivers/dri"
fi
  make -C i810 DESTDIR="${pkgdir}" install
  make -C i915 DESTDIR="${pkgdir}" install
  make -C i965 DESTDIR="${pkgdir}" install
}

package_unichrome-dri() {
  depends=("libgl=${pkgver}")
  pkgdesc="Mesa DRI drivers for S3 Graphics/VIA Unichrome"

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*/src/mesa/drivers/dri
  else
    cd "${srcdir}/Mesa-${pkgver}/src/mesa/drivers/dri"
fi
  make -C unichrome DESTDIR="${pkgdir}" install
}

package_mach64-dri() {
  depends=("libgl=${pkgver}")
  pkgdesc="Mesa DRI drivers for ATI Mach64"
  conflicts=('xf86-video-mach64<6.8.2')

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*/src/mesa/drivers/dri
  else
    cd "${srcdir}/Mesa-${pkgver}/src/mesa/drivers/dri"
fi
  make -C mach64 DESTDIR="${pkgdir}" install
}

package_mga-dri() {
  depends=("libgl=${pkgver}")
  pkgdesc="Mesa DRI drivers for Matrox"
  conflicts=('xf86-video-mga<1.4.11')

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*/src/mesa/drivers/dri
  else
    cd "${srcdir}/Mesa-${pkgver}/src/mesa/drivers/dri"
fi
  make -C mga DESTDIR="${pkgdir}" install
}

package_r128-dri() {
  depends=("libgl=${pkgver}")
  pkgdesc="Mesa DRI drivers for ATI Rage128"
  conflicts=('xf86-video-r128<6.8.1')

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*/src/mesa/drivers/dri
  else
    cd "${srcdir}/Mesa-${pkgver}/src/mesa/drivers/dri"
fi
  make -C r128 DESTDIR="${pkgdir}" install
}

package_savage-dri() {
  depends=("libgl=${pkgver}")
  pkgdesc="Mesa DRI drivers for S3 Sraphics/VIA Savage"
  conflicts=('xf86-video-savage<2.3.1')

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*/src/mesa/drivers/dri
  else
    cd "${srcdir}/Mesa-${pkgver}/src/mesa/drivers/dri"
fi
  make -C savage DESTDIR="${pkgdir}" install
}

package_sis-dri() {
  depends=("libgl=${pkgver}")
  pkgdesc="Mesa DRI drivers for SiS"
  conflicts=('xf86-video-sis<0.10.2')

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*/src/mesa/drivers/dri
  else
    cd "${srcdir}/Mesa-${pkgver}/src/mesa/drivers/dri"
fi
  make -C sis DESTDIR="${pkgdir}" install
}

package_tdfx-dri() {
  depends=("libgl=${pkgver}")
  pkgdesc="Mesa DRI drivers for 3dfx"
  conflicts=('xf86-video-tdfx<1.4.3')

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*/src/mesa/drivers/dri
  else
    cd "${srcdir}/Mesa-${pkgver}/src/mesa/drivers/dri"
fi
  make -C tdfx DESTDIR="${pkgdir}" install
}

package_nouveau-dri() {
  depends=("libgl=${pkgver}")
  pkgdesc="Mesa classic DRI + Gallium3D drivers for Nouveau"

if [ "${_git}" = "true" ]; then
    cd ${srcdir}/mesa-*/src/mesa/drivers/dri
  else
    cd "${srcdir}/Mesa-${pkgver}/src/mesa/drivers/dri"
fi

  # classic mesa driver for nv10 , nv20 nouveau_vieux_dri.so
  make -C nouveau DESTDIR="${pkgdir}" install

  # gallium3D driver for nv30 - nv40 - nv50 nouveau_dri.so
if [ "${_git}" = "true" ]; then
    make -C ${srcdir}/mesa-*/src/gallium/targets/dri-nouveau DESTDIR="${pkgdir}" install
  else
    make -C ${srcdir}/Mesa-${pkgver}/src/gallium/targets/dri-nouveau DESTDIR="${pkgdir}" install
fi
}

