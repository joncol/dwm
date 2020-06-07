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
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'st' 'dmenu')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
        dwm-fancybar-hide_vacant_tags-6.2.diff
        https://dwm.suckless.org/patches/actualfullscreen/dwm-actualfullscreen-20191112-cb3f58a.diff
        https://dwm.suckless.org/patches/attachaside/dwm-attachaside-6.1.diff
        https://dwm.suckless.org/patches/autostart/dwm-autostart-20161205-bb3bd6f.diff
        https://dwm.suckless.org/patches/center/dwm-center-6.2.diff
        https://dwm.suckless.org/patches/centeredmaster/dwm-centeredmaster-6.1.diff
        https://dwm.suckless.org/patches/noborder/dwm-noborderfloatingfix-6.2.diff
        https://dwm.suckless.org/patches/pertag/dwm-pertag-6.2.diff
        https://dwm.suckless.org/patches/vanitygaps/dwm-vanitygaps-20190508-6.2.diff
        config.h
        dwm.desktop)
sha256sums=('97902e2e007aaeaa3c6e3bed1f81785b817b7413947f1db1d3b62b8da4cd110e'
            'b3533b2ca3564c7040d0bab0198dd605d2600d87c00dab0ec0c2e4d7be84df16'
            '7b4cabdccc8af6ee3d3819452e5028dd9d926b1edc4496f102e19210f0fcd785'
            '86bdb4291c0f8f9b0c6fbbac9f05403224872b786fc5e74f3b141c8f2ce6c7a1'
            'e2b59b2c591c76ff95efec8288ef7796313951c52b24dd49ab23fdae98460608'
            'd101eee27b6bf0e8847a93e3b95bf63a64e00251c8ff3cc581c55af5e9a7a60e'
            '4914086ae33aee6c34e1ffded484ada465d1eff3bf39372087e84cd6bba04fb0'
            'a2cc6b3ac8b33e13a94356beb433cc6e62ac8ef03e14c0bc6706df8883679d84'
            '055da0f12dbfde9e50df54e1f2d87966466404a36c056efb94bb21ab03b94b10'
            '148e47ed1e8fdbc510b68db27051e0e640d0d55fdcf214afb07d6ecb6ac841fc'
            'b2d8b3f1571a03f1a9471a0facd54a57e1c469f78a0f35a13b6a3d70dfba7ebc'
            'bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81')

_sourcedir=$pkgname-$pkgver

prepare() {
  patch --verbose --directory="$_sourcedir" -Np1 < dwm-actualfullscreen-20191112-cb3f58a.diff
  patch --verbose --directory="$_sourcedir" -Np1 < dwm-attachaside-6.1.diff
  patch --verbose --directory="$_sourcedir" -Np1 < dwm-autostart-20161205-bb3bd6f.diff
  patch --verbose --directory="$_sourcedir" -Np1 < dwm-center-6.2.diff
  patch --verbose --directory="$_sourcedir" -Np1 < dwm-centeredmaster-6.1.diff
  patch --verbose --directory="$_sourcedir" -Np1 < dwm-fancybar-hide_vacant_tags-6.2.diff
  patch --verbose --directory="$_sourcedir" -Np1 < dwm-noborderfloatingfix-6.2.diff
  patch --verbose --directory="$_sourcedir" -Np1 < dwm-pertag-6.2.diff
  patch --verbose --directory="$_sourcedir" -Np1 < dwm-vanitygaps-20190508-6.2.diff
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
