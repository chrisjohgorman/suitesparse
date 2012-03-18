# Maintainer: Ronald van Haren <ronald.archlinux.org>

pkgname=suitesparse
pkgver=3.7.0
pkgrel=1
pkgdesc="A collection of sparse matrix libraries"
url="http://www.cise.ufl.edu/research/sparse/SuiteSparse/"
arch=('i686' 'x86_64')
conflicts=('umfpack')
provides=('umfpack')
replaces=('umfpack')
depends=('blas' 'lapack')
makedepends=('gcc-fortran')
license=('GPL')
source=(http://www.cise.ufl.edu/research/sparse/SuiteSparse/SuiteSparse-$pkgver.tar.gz)
sha1sums=('d0eb24b43ee2f7def032e80eaa7a589f94f546fc')

build() {
   cd "$srcdir"/SuiteSparse
   export CFLAGS=" ${CFLAGS} -DNPARTITION"
   
   make -C UFconfig/xerbla
   make -C UFconfig 
   for _lib in AMD CAMD COLAMD BTF KLU LDL CCOLAMD UMFPACK CHOLMOD CXSparse SPQR; do
      make -C ${_lib} library
   done
}


package() {
   cd "${srcdir}"/SuiteSparse
   install -dm755 "${pkgdir}"/usr/{lib,include}
   
   for _lib in UFconfig AMD CAMD COLAMD BTF KLU LDL CCOLAMD UMFPACK CHOLMOD CXSparse SPQR; do
      make -C ${_lib} INSTALL_LIB="${pkgdir}"/usr/lib INSTALL_INCLUDE="${pkgdir}"/usr/include install
   done

   chmod 644 "${pkgdir}"/usr/include/*.{h,hpp}
}
