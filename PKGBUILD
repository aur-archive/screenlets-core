# $Id$
# Maintainer: Artiom MOLCHANOV <ar.molchanov@gmail.com>
# Contributor: Roman Kyrylych <roman@archlinux.org>
# Contributor: javonera <javonera@gmail.com>

pkgname=screenlets-core
_pkgname=screenlets
pkgver=0.1.6
pkgrel=4
pkgdesc="Screenlets — a framework for desktop widgets"
arch=('any')
url="http://screenlets.org/"
license=('GPL3')
depends=('dbus-python' 'gstreamer0.10-python' 'gnome-python-desktop'
'python2-gconf' 'python2-gnomekeyring' 'python2-gnomevfs' 'python2-rsvg'
'python2-wnck' 'pyxdg' 'notification-daemon' 'xdg-utils' 'hicolor-icon-theme'
'python-beautifulsoup')
optdepends=('screenlets-pack: Screenlets')
#install=screenlets.install
source=(https://code.launchpad.net/$_pkgname/trunk/$pkgver/+download/$_pkgname-$pkgver.tar.bz2 
init.patch utils.patch xdg1.patch Screenlets.directory)
conflicts=(screenlets)
md5sums=('028ce6b6c8764190d435436d5cbaf68c'
         '1fdece77448ebe8f941cc53e6566aed5'
         'c4113ddcdce907081d258e5afbf23afe'
         'c99662aa83cb7a26c1efa256195a0b91'
         'd4ccc8afaf67291a76eba0d49ba8138c')
build() {
  cd "$srcdir/${_pkgname}-${pkgver}"
  for _file in $( find ./src -type f ) ; do 
    sed -i 's:python\([^2]\):python2\1:g' ${_file}
    sed -i 's:python$:python2:' ${_file}
  done
  patch -p0 < $srcdir/init.patch
  patch -p0 < $srcdir/utils.patch
  patch -p0 < $srcdir/xdg1.patch
}

package() {
  cd "$srcdir/${_pkgname}-${pkgver}"
  mkdir -p "$pkgdir"/etc/screenlets
  echo /usr > "$pkgdir"/etc/screenlets/prefix

  python2 setup.py install --root="$pkgdir"

  install -D -m644 "$srcdir/Screenlets.directory" "$pkgdir/usr/share/desktop-directories/Screenlets.directory"
 
  install -D -m644 desktop-menu/screenlets.svg "$pkgdir/usr/share/icons/screenlets.svg"
  install -D -m644 desktop-menu/mono-dark/screenlets-tray.svg "$pkgdir/usr/share/icons/screenlets-tray.svg"

  cd desktop-menu/
  for i in $(find -name '*.desktop'); do install -D -m644 $i "$pkgdir"/usr/share/applications/$(echo $i | sed 's|./applications||') ; done
}
