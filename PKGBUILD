# Maintainer: Ronald van Haren <ronald.archlinux.org>

pkgname=suitesparse
pkgver=5.2.0
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
source=("http://faculty.cse.tamu.edu/davis/SuiteSparse/SuiteSparse-$pkgver.tar.gz")
sha1sums=('e80fb66c7c8613e24cc87c9fb4482e8348f690e9')

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
