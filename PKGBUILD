# Maintainer: Brandon Invergo <brandon@invergo.net>
# Contributor: Travis Willard <travisw@wmpub.ca> 

pkgname=gnuradius
_pkgname=radius
pkgver=1.6.1
pkgrel=3
pkgdesc="GNU radius authentication server"
url="http://www.gnu.org/software/radius/"
license="GPL"
arch=('i686' 'x86_64')
depends=('guile' 'libmariadbclient')
backup=()
install=gnuradius.install
options=(!libtool)
source=(ftp://ftp.gnu.org/gnu/radius/radius-$pkgver.tar.gz scheme.c.patch)
md5sums=('586f1f735de7634b4a6805e880b76594' 
         'fccd7343e044a35a3be22372e2933cf1'
)

build() {
  cd "$srcdir/$_pkgname-$pkgver"
  patch -uN radiusd/scheme.c ../scheme.c.patch || return 1
  ./configure --prefix=/usr \
              --sysconfdir=/etc \
              --enable-client \
              --with-mysql \
              --with-readline \
              --enable-pam \
              --enable-snmp || return 1
  make || return 1
}

package() {
  cd "$srcdir/$_pkgname-$pkgver"
  make DESTDIR="$pkgdir" install || return 1
  rm $startdir/pkg/usr/libexec -r
}
