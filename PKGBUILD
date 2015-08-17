# Maintainer: Bjonnh < bjonnh-aur at bjonnh dot net>
# Contributor: Robert Knauer <robert@privatdemail.net>
# Contributor: Rodrigo Grumiche Silva <grumiche at integrityit dot com dot br>
# Contributor: nozog
# Contributor: davidhjelm
# Contributor: Ray Kohler <ataraxia937 at gmail dot com>
# Contributor: Nathan Owe < ndowens04 at gmail dot com>

pkgname=poco-devel
pkgname_=poco
pkgver=1.5.4
pkgrel=1
pkgdesc="C++ class libraries for network-centric, portable applications, complete edition"
arch=('i686' 'x86_64')
url="http://www.pocoproject.org/"
license=('custom:boost')
depends=('unixodbc' 'libmariadbclient' 'openssl')
makedepends=('gcc' 'make' 'unixodbc' 'libmariadbclient' 'openssl' 'chrpath')
provides=('poco')
conflicts=('poco')
replaces=('poco')
source=(
  "${pkgname_}-${pkgver}-all.tar.bz2"::"http://pocoproject.org/releases/${pkgname_}-${pkgver}/${pkgname_}-${pkgver}-all.tar.gz"
)
sha256sums=('a8391d37f8a93ef0969d82b860b0e16d26b8c0cec67915a9592f90008ab37c8e')

build()
{
  cd "${srcdir}/${pkgname_}-${pkgver}-all"
  ./configure --prefix=/usr --no-samples --no-tests
  make -j2 ODBCLIBDIR="/usr/lib"
}

package()
{
  cd "${srcdir}/${pkgname_}-${pkgver}-all"
  make ODBCLIBDIR="/usr/lib" DESTDIR="${pkgdir}" install
  install -Dm644 'LICENSE' "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  # remove rpath information from binaries
  chrpath -d "${pkgdir}/usr/bin/cpspc"
  chrpath -d "${pkgdir}/usr/bin/cpspcd"
  chrpath -d "${pkgdir}/usr/bin/f2cpspd"
  chrpath -d "${pkgdir}/usr/bin/f2cpsp"
  # remove debugging libraries
  rm "${pkgdir}/usr/lib/libPoco"*"d.so"*
}
