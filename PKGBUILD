# Maintainer: Ronald van Haren <ronald.archlinux.org>

pkgname=suitesparse
pkgver=5.4.0
pkgrel=1
pkgdesc="A collection of sparse matrix libraries"
url="http://faculty.cse.tamu.edu/davis/suitesparse.html"
arch=('x86_64')
conflicts=('umfpack')
provides=('umfpack')
replaces=('umfpack')
depends=('metis' 'lapack' 'intel-tbb')
makedepends=('gcc-fortran' 'cmake' 'chrpath')
license=('GPL')
options=('staticlibs')
source=("http://faculty.cse.tamu.edu/davis/SuiteSparse/SuiteSparse-$pkgver.tar.gz"
        suitesparse-no-demo.patch)
sha1sums=('23bb875f50c2b1ea7d9e7885e1956fa02e210824'
          '2737ae324e50d3f3941619fbc64ba6e0a8d6993e')

prepare() {
  patch -p0 -i suitesparse-no-demo.patch # Don't run test application at build time
}

build() {
   cd SuiteSparse

   BLAS=-lblas TBB=-ltbb SPQR_CONFIG=-DHAVE_TBB MY_METIS_LIB=/usr/lib/libmetis.so make
}


package() {
   cd SuiteSparse
   install -dm755 "${pkgdir}"/usr/{include,lib}

   BLAS=-lblas TBB=-ltbb SPQR_CONFIG=-DHAVE_TBB MY_METIS_LIB=/usr/lib/libmetis.so \
     make INSTALL_LIB="${pkgdir}"/usr/lib INSTALL_INCLUDE="${pkgdir}"/usr/include install

   # fix RPATH
   chrpath -d "$pkgdir"/usr/lib/*
}
