# Maintainer: archtux <antonio dot arias99999 at gmail dot com>

pkgname=kardsgt
pkgver=0.7.1
pkgrel=6
pkgdesc="KardsGT is a general card game suite. Available games are : Crazy Eights, Cribbage, Euchre, Hearts, Old Maid, Spades, War."
arch=('i686' 'x86_64')
url="http://www.kde-apps.org/content/show.php/KardsGT?content=40618"
license=('GPL3')
depends=('qt-assistant-compat')
options=('!makeflags')
source=(http://download.savannah.gnu.org/releases/$pkgname/$pkgname-$pkgver.tar.gz
        kardsgt.desktop)
md5sums=('e2cb00dfea3fc8351ea5d0339514d2cc'
         '257ab422edced6b02770660b33e5f361')

prepare() {
  cd $srcdir/$pkgname-$pkgver

  # Fix for 'QAssistantClient' that was removed in Qt 4.7
  sed -i 's|<QAssistantClient>|"qassistantclient.h"|' src/kardsgtinterface.cpp  
  
  qmake-qt4
}

build() {
  cd $srcdir/$pkgname-$pkgver
  make release
}

package() {
  cd $srcdir/$pkgname-$pkgver

  # Binary
  install -Dm755 release/kardsgt $pkgdir/usr/bin/kardsgt

  # Man page
  install -Dm644 src/doc/kardsgt.6 $pkgdir/usr/share/man/man6/kardsgt.6
  
  # Docs
  mkdir -p $pkgdir/usr/share/kardsgt
  cp -rf src/doc/* $pkgdir/usr/share/kardsgt

  # Desktop icon
  install -Dm644 src/images/kardsgt.png $pkgdir/usr/share/pixmaps/kardsgt.png
  install -Dm644 ../kardsgt.desktop $pkgdir/usr/share/applications/kardsgt.desktop
}