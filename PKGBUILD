# Maintainer: Ronald van Haren <ronald.archlinux.org>

pkgname=suitesparse
pkgver=4.5.3
pkgrel=1
pkgdesc="A collection of sparse matrix libraries"
url="http://faculty.cse.tamu.edu/davis/suitesparse.html"
arch=('i686' 'x86_64')
conflicts=('umfpack')
provides=('umfpack')
replaces=('umfpack')
depends=('blas' 'lapack' 'intel-tbb')
makedepends=('gcc-fortran' 'cmake' 'chrpath')
license=('GPL')
options=('staticlibs')
source=("http://faculty.cse.tamu.edu/davis/SuiteSparse/SuiteSparse-$pkgver.tar.gz" suitesparse-link-tbb.patch)
sha1sums=('2403007be38266e3607edfbf3833bee7f6bcb0f1'
          '4f0b3836e8c3c1ec5be01f988f136cee4a2cb936')

prepare() {
# Fix linking with intel-tbb
  cd SuiteSparse
  patch -p1 -i ../suitesparse-link-tbb.patch
}

build() {
   cd "$srcdir"/SuiteSparse

   BLAS=-lblas TBB=-ltbb SPQR_CONFIG=-DHAVE_TBB make
}


package() {
   cd "${srcdir}"/SuiteSparse
   install -dm755 "${pkgdir}"/usr

   pushd metis-5.1.0
     make install DESTDIR="$pkgdir"
     mv "$pkgdir"/build/suitesparse/src/SuiteSparse/* "$pkgdir"/usr && rm -r "$pkgdir"/build
   popd
   BLAS=-lblas TBB=-ltbb SPQR_CONFIG=-DHAVE_TBB make INSTALL_LIB="${pkgdir}"/usr/lib INSTALL_INCLUDE="${pkgdir}"/usr/include install

   # fix RPATH
   chrpath -d "$pkgdir"/usr/lib/*
}
