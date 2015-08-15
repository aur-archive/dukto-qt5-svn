# Maintainer: Mr_Men <tetcheve (at) gmail dot com>
# Contributors: Stefan Husmann, tomk, Dan Serban

pkgname=dukto-qt5-svn
pkgver=6.0
pkgrel=3
pkgdesc="A simple, fast and multi-platform file transfer tool for LAN users"
arch=('i686' 'x86_64')
url="http://code.google.com/p/dukto/"
license=('GPL')
depends=('qt5-quick1' 'qt5-script' 'qt5-xmlpatterns')
makedepends=('subversion')
source=('dukto-qt5.4.patch')
sha256sums=('02cdc944a5d9cbb7b3dd71a09f3789670de38525ee5aa238121fbabb3a81495e')
_svntrunk="http://dukto.googlecode.com/svn/trunk/"
_svnmod="dukto-read-only"

prepare() {
  svn co ${_svntrunk} ${_svnmod}
  cd $srcdir/dukto-read-only
  #sed -i "47i#include <unistd.h>" qtsingleapplication/qtlocalpeer.cpp
  patch -p0 -i ../dukto-qt5.4.patch
}

build()
{
  cd $srcdir/dukto-read-only
  qmake dukto.pro
  make
}

package (){
  cd $srcdir/$_svnmod
  install -Dm755 dukto "${pkgdir}"/usr/bin/dukto
  mkdir -p "${pkgdir}"/usr/share/pixmaps
  install -Dm644 dukto.png "${pkgdir}"/usr/share/pixmaps/dukto.png
  mkdir -p "${pkgdir}"/usr/share/applications
  DESKTOPFILE="${pkgdir}"/usr/share/applications/dukto.desktop
  echo "[Desktop Entry]" > "${DESKTOPFILE}"
  echo "Name=Dukto" >> "${DESKTOPFILE}"
  echo "Icon=dukto.png" >> "${DESKTOPFILE}"
  echo "GenericName=Transfer files across the LAN" >> "${DESKTOPFILE}"
  echo "Comment=Transfer files across the LAN" >> "${DESKTOPFILE}"
  echo "Exec=dukto" >> "${DESKTOPFILE}"
  echo "Terminal=false" >> "${DESKTOPFILE}"
  echo "Type=Application" >> "${DESKTOPFILE}"
  echo "Categories=Network;Application;" >> "${DESKTOPFILE}"
}

