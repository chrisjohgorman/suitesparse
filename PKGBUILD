# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Contributor: Ronald van Haren <ronald.archlinux.org>
# Contributor: Chris Gorman <chrisjohgorman@gmail.com>

pkgname=suitesparse64
_pkgname=suitesparse
pkgver=7.7.0
pkgrel=1
pkgdesc='A collection of sparse matrix libraries'
url='http://faculty.cse.tamu.edu/davis/suitesparse.html'
arch=(x86_64)
depends=(blas64
         gcc-libs
         glibc
         gmp
         lapack64
         mpfr)
makedepends=(cmake
             gcc-fortran)
replaces=('suitesparse64<7.1.0')
license=(GPL)
source=(https://github.com/DrTimothyAldenDavis/SuiteSparse/archive/v$pkgver/$_pkgname-$pkgver.tar.gz
        suitesparse64.patch)
sha256sums=('529b067f5d80981f45ddf6766627b8fc5af619822f068f342aab776e683df4f3'
            '39bcb00ceff97c125550f261ad217ab7eef2cdf46e7b9ddb2a61cb84f40470c8')

prepare() {
    patch -d SuiteSparse-$pkgver -p1 < suitesparse64.patch
}

build() {
  cd SuiteSparse-$pkgver
  CMAKE_OPTIONS="-DBLA_VENDOR=Generic \
                 -DCMAKE_INSTALL_PREFIX=/usr \
                 -DCMAKE_BUILD_TYPE=None \
                 -DNSTATIC=ON \
                 -DSUITESPARSE_INCLUDEDIR_POSTFIX=suitesparse64 \
                 -DSUITESPARSE_USE_64BIT_BLAS=ON" \
  make
}

package() {
  cd SuiteSparse-$pkgver
  DESTDIR="$pkgdir" make install
  #FIXME use source code to do this
  cd "$pkgdir"/usr/lib/cmake
  mv SuiteSparse SuiteSparse64 
}
