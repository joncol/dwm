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
        https://dwm.suckless.org/patches/autostart/dwm-autostart-20161205-bb3bd6f.diff
        https://dwm.suckless.org/patches/pertag/dwm-pertag-6.2.diff
        https://dwm.suckless.org/patches/vanitygaps/dwm-vanitygaps-20190508-6.2.diff
        config.h
        dwm.desktop)
sha256sums=('97902e2e007aaeaa3c6e3bed1f81785b817b7413947f1db1d3b62b8da4cd110e'
            'e2b59b2c591c76ff95efec8288ef7796313951c52b24dd49ab23fdae98460608'
            '055da0f12dbfde9e50df54e1f2d87966466404a36c056efb94bb21ab03b94b10'
            '148e47ed1e8fdbc510b68db27051e0e640d0d55fdcf214afb07d6ecb6ac841fc'
            'e5d9a223994bddfe673f5a8e59e500fc2318e5cba2e91c8d3c8a23e8fc99bc59'
            'bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81')
_sourcedir=$pkgname-$pkgver

prepare() {
  patch --directory="$_sourcedir" -p1 < dwm-autostart-20161205-bb3bd6f.diff
  patch --directory="$_sourcedir" -p1 < dwm-pertag-6.2.diff
  patch --directory="$_sourcedir" -p1 < dwm-vanitygaps-20190508-6.2.diff
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
