# Mainainer: Sébastien "Seblu" Luttringer <seblu@archlinux.org>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: Andreas Radke <andyrtr@archlinux.org>

pkgname=tar
pkgver=1.34
pkgrel=1
pkgdesc='Utility used to store, backup, and transport files'
arch=('x86_64')
url='https://www.gnu.org/software/tar/'
license=('GPL3')
depends=('glibc' 'acl' 'attr')
options=('!emptydirs')
validpgpkeys=('325F650C4C2B6AD58807327A3602B07F55D0C732') # Sergey Poznyakoff
source=("https://ftp.gnu.org/gnu/$pkgname/$pkgname-$pkgver.tar.xz"{,.sig})
sha256sums=('63bebd26879c5e1eea4352f0d03c991f966aeb3ddeb3c7445c902568d5411d28'
            'SKIP')

prepare() {
  cd $pkgname-$pkgver
  # apply patch from the source array (should be a pacman feature)
  local src
  for src in "${source[@]}"; do
    src="${src%%::*}"
    src="${src##*/}"
    [[ $src = *.patch ]] || continue
    msg2 "Applying patch $src..."
    patch -Np1 < "../$src"
  done
  :
}

build() {
  cd $pkgname-$pkgver
  ./configure --prefix=/usr --libexecdir=/usr/lib/tar
  make
}

check() {
  cd $pkgname-$pkgver
  make check
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install
}

# vim:set ts=2 sw=2 et:
