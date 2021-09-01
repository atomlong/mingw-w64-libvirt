# Maintainer: Jack O'Sullivan <jackos1998 at gmail dot com>

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

pkgname=mingw-w64-libvirt
pkgver=7.6.0
pkgrel=1
pkgdesc="API for controlling virtualization engines (remote only for windows)"
arch=('any')
url="https://libvirt.org/"
license=('LGPL')
depends=('mingw-w64-crt' 'mingw-w64-gnutls' 'mingw-w64-libgpg-error' 'mingw-w64-libgcrypt'
         'mingw-w64-gettext' 'mingw-w64-libxml2' 'mingw-w64-portablexdr' 'mingw-w64-libssh2'
         'mingw-w64-curl')
makedepends=('mingw-w64-configure' 'gettext' 'libxslt' 'python' 'perl')
options=('!strip' 'staticlibs' '!buildflags')
validpgpkeys=('C74415BA7C9C7F78F02E1DC34606B8A5DE95BC1F')
source=("https://libvirt.org/sources/libvirt-${pkgver}.tar.xz"{,.asc})

sha256sums=('8f967106d00aabb3cd692724bdd4a9c09e71cb2245053b98193690ee01766141'
            'SKIP')

build() {
  cd "${srcdir}/libvirt-${pkgver}"

  for _arch in ${_architectures}; do
    mkdir -p build-${_arch} && pushd build-${_arch}
    ${_arch}-configure
    make
    popd
  done
}

package() {
  for _arch in ${_architectures}; do
    cd "${srcdir}/libvirt-${pkgver}/build-${_arch}"
    make DESTDIR="${pkgdir}" install
    find "${pkgdir}/usr/${_arch}" -name '*.exe' | xargs -rtl1 ${_arch}-strip
    find "${pkgdir}/usr/${_arch}" -name '*.dll' | xargs -rtl1 ${_arch}-strip -x
    find "${pkgdir}/usr/${_arch}" -name '*.a' -o -name '*.dll' | xargs -rtl1 ${_arch}-strip -g
  done
}

# vim:set ts=2 sw=2 et:
