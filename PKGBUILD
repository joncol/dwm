# $Id$
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.2
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
        dwm-fancybar-hide_vacant_tags-6.2.diff
        dwm-swallow.diff
        dwm-vanitygaps-20190508-6.2.diff
        https://dwm.suckless.org/patches/actualfullscreen/dwm-actualfullscreen-20191112-cb3f58a.diff
        https://dwm.suckless.org/patches/alpha/dwm-alpha-20180613-b69c870.diff
        https://dwm.suckless.org/patches/attachaside/dwm-attachaside-6.1.diff
        https://dwm.suckless.org/patches/autostart/dwm-autostart-20161205-bb3bd6f.diff
        https://dwm.suckless.org/patches/center/dwm-center-6.2.diff
        https://dwm.suckless.org/patches/centeredmaster/dwm-centeredmaster-6.1.diff
        https://dwm.suckless.org/patches/noborder/dwm-noborderfloatingfix-6.2.diff
        https://dwm.suckless.org/patches/pertag/dwm-pertag-6.2.diff
        https://dwm.suckless.org/patches/selfrestart/dwm-r1615-selfrestart.diff
        config.h
        dwm.desktop)
md5sums=('9929845ccdec4d2cc191f16210dd7f3d'
         '55486b80d31b59c92c6766029f55218d'
         'bc7417af1a2f931b28d7eae6108ab9ce'
         '331d572c27d8b8f66deeb5f57d106fb0'
         'd91950eed1d7cd232be05c7d3d0666ec'
         '4e5893e04c443530168223639c97bc47'
         'e67fab561c52b8380050130350fe0267'
         '46ff022e2a2c6139e71399eb19d1aebb'
         '234bb304c6d4330e077ffe4e894eed84'
         '55b414c803f0b9bbd0c368c340aa27df'
         'a55c836f0d328c898ed00dedb4e9a286'
         '630051fbd9750a4344c599eb42bf69fb'
         'aa3d5f3c45057a2a6ee73aede3fc218a'
         '67740f804d8e5450a94507f6078454de'
         '939f403a71b6e85261d09fc3412269ee')

_sourcedir=$pkgname-$pkgver

prepare() {
  patch --directory="$_sourcedir" -Np1 < dwm-actualfullscreen-20191112-cb3f58a.diff
  patch --directory="$_sourcedir" -Np1 < dwm-alpha-20180613-b69c870.diff
  patch --directory="$_sourcedir" -Np1 < dwm-attachaside-6.1.diff
  patch --directory="$_sourcedir" -Np1 < dwm-autostart-20161205-bb3bd6f.diff
  patch --directory="$_sourcedir" -Np1 < dwm-center-6.2.diff
  patch --directory="$_sourcedir" -Np1 < dwm-centeredmaster-6.1.diff
  patch --directory="$_sourcedir" -Np1 < dwm-fancybar-hide_vacant_tags-6.2.diff
  patch --directory="$_sourcedir" -Np1 < dwm-noborderfloatingfix-6.2.diff
  patch --directory="$_sourcedir" -Np1 < dwm-pertag-6.2.diff
  rm -f "$_sourcedir"/selfrestart.c
  patch --directory="$_sourcedir" -Np1 < dwm-r1615-selfrestart.diff
  patch --directory="$_sourcedir" -Np1 < dwm-swallow.diff
  patch --directory="$_sourcedir" -Np1 < dwm-vanitygaps-20190508-6.2.diff

  cd "$srcdir/$pkgname-$pkgver"
  cp "$srcdir/config.h" config.h
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
  install -m644 -D "$srcdir/dwm.desktop" "$pkgdir/usr/share/xsessions/dwm.desktop"
}
