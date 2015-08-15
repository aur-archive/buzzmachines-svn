# Maintainer: speps <speps at aur dot archlinux dot org>

_name=buzzmachines
pkgname=$_name-svn
pkgver=160
pkgrel=1
pkgdesc="Collection of freely available buzz machine sources."
arch=('i686' 'x86_64')
url="http://www.buzztard.org"
license=('LGPL')
makedepends=('subversion')
provides=("$_name")
conflicts=("$_name")
options=('!libtool')

_svntrunk="https://buzzmachines.svn.sourceforge.net/svnroot/$_name/trunk/$_name"
_svnmod="$_name"

build() {
  cd "$srcdir"

  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  #
  # BUILD
  #

  ./autogen.sh
  ./configure --prefix=/usr \
              --enable-static=no
  make
}

package() {
  cd "$srcdir/$_svnmod-build"
  make DESTDIR="$pkgdir/" install
}
