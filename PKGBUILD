# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Contributor: Ronald van Haren <ronald.archlinux.org>

pkgname=suitesparse
pkgver=7.6.0
pkgrel=1
pkgdesc='A collection of sparse matrix libraries'
url='http://faculty.cse.tamu.edu/davis/suitesparse.html'
arch=(x86_64)
depends=(blas
         gcc-libs
         glibc
         gmp
         lapack
         mpfr)
makedepends=(cmake
             gcc-fortran)
replaces=('suitesparse64<7.1.0')
license=(GPL)
source=(https://github.com/DrTimothyAldenDavis/SuiteSparse/archive/v$pkgver/$pkgname-$pkgver.tar.gz)
sha256sums=('19cbeb9964ebe439413dd66d82ace1f904adc5f25d8a823c1b48c34bd0d29ea5')

build() {
  cd SuiteSparse-$pkgver
  CMAKE_OPTIONS="-DBLA_VENDOR=Generic \
                 -DCMAKE_INSTALL_PREFIX=/usr \
                 -DCMAKE_BUILD_TYPE=None \
                 -DNSTATIC=ON" \
  make
}

package() {
  cd SuiteSparse-$pkgver
  DESTDIR="$pkgdir" make install
}
