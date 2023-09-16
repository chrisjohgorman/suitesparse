# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Contributor: Ronald van Haren <ronald.archlinux.org>

pkgname=suitesparse
pkgver=7.2.0
pkgrel=1
pkgdesc='A collection of sparse matrix libraries'
url='http://faculty.cse.tamu.edu/davis/suitesparse.html'
arch=(x86_64)
depends=(lapack mpfr)
makedepends=(gcc-fortran cmake lapack)
replaces=('suitesparse64<7.1.0')
license=(GPL)
source=(https://github.com/DrTimothyAldenDavis/SuiteSparse/archive/v$pkgver/$pkgname-$pkgver.tar.gz)
sha256sums=('ce63c34f566d0aeae3c85fdc5b72d293f7e834d10ec0a0417b4c0823ce6c0474')

build() {
  cd SuiteSparse-$pkgver
  CXXFLAGS+=" -ffat-lto-objects" \
  CMAKE_OPTIONS="-DBLA_VENDOR=Generic \
  -DCMAKE_INSTALL_PREFIX=/usr \
  -DCMAKE_BUILD_TYPE=None" \
  make
}

package() {
  cd SuiteSparse-$pkgver
  DESTDIR="$pkgdir" make install
}
