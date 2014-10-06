# Maintainer: Ronald van Haren <ronald.archlinux.org>

pkgname=suitesparse
pkgver=4.3.1
pkgrel=2
pkgdesc="A collection of sparse matrix libraries"
url="http://www.cise.ufl.edu/research/sparse/SuiteSparse/"
arch=('i686' 'x86_64')
conflicts=('umfpack')
provides=('umfpack')
replaces=('umfpack')
depends=('blas' 'lapack')
makedepends=('gcc-fortran')
license=('GPL')
options=('staticlibs')
source=(http://www.cise.ufl.edu/research/sparse/SuiteSparse/SuiteSparse-$pkgver.tar.gz http://pkgs.fedoraproject.org/cgit/suitesparse.git/plain/suitesparse-math.patch)
sha1sums=('f7087d6178331d570c1ec811bbd17cbce70ce2f5'
          'a6b3f29df0cc813be0aa7afb65592c2eb431bba4')

build() {
   cd "$srcdir"/SuiteSparse
   export CFLAGS=" ${CFLAGS} -DNPARTITION -fPIC"
   patch -Np1 -i "$srcdir"/suitesparse-math.patch
   
   make -C SuiteSparse_config/xerbla
   make -C SuiteSparse_config 
   for _lib in AMD CAMD COLAMD BTF KLU LDL CCOLAMD UMFPACK CHOLMOD CXSparse SPQR; do
      make -C ${_lib} library
   done
   mkdir shared
   ld -shared -soname libsuitesparseconfig.so.4 -o \
      shared/libsuitesparseconfig.so.4.3.1 --whole-archive \
      SuiteSparse_config/libsuitesparseconfig.a -lm && \
      ln -sf libsuitesparseconfig.so.4.3.1 shared/libsuitesparseconfig.so
   ld -shared -soname libamd.so.2 -o shared/libamd.so.2.4.0 \
      --whole-archive AMD/Lib/libamd.a -L./shared -lsuitesparseconfig -lm && \
      ln -sf libamd.so.2.4.0 shared/libamd.so
   ld -shared -soname libcamd.so.2 -o shared/libcamd.so.2.4.0 \
      --whole-archive CAMD/Lib/libcamd.a -L./shared -lsuitesparseconfig -lm && \
      ln -sf libcamd.so.2.4.0 shared/libcamd.so
   ld -shared -soname libcolamd.so.2 -o shared/libcolamd.so.2.9.0 \
      --whole-archive COLAMD/Lib/libcolamd.a -L./shared -lsuitesparseconfig -lm \
      && ln -sf libcolamd.so.2.9.0 shared/libcolamd.so
   ld -shared -soname libccolamd.so.2 -o shared/libccolamd.so.2.9.0 \
      --whole-archive CCOLAMD/Lib/libccolamd.a -L./shared -lsuitesparseconfig -lm \
      && ln -sf libccolamd.so.2.9.0 shared/libccolamd.so
   ld -shared -soname libbtf.so.1 -o shared/libbtf.so.1.2.0 \
      --whole-archive BTF/Lib/libbtf.a && \
      ln -sf libbtf.so.1.2.0 shared/libbtf.so
   ld -shared -soname libldl.so.2 -o shared/libldl.so.2.2.0 \
      --whole-archive LDL/Lib/libldl.a && \
      ln -sf libldl.so.2.2.0 shared/libldl.so
   ld -shared -soname libcholmod.so.3 -o shared/libcholmod.so.3.0.1 \
      --whole-archive CHOLMOD/Lib/libcholmod.a -lblas -llapack \
      -L./shared -lamd -lcamd -lcolamd -lccolamd -lsuitesparseconfig -lm && \
      ln -sf libcholmod.so.3.0.1 shared/libcholmod.so
   ld -shared -soname libspqr.so.1 -o shared/libspqr.so.1.3.3 \
      --whole-archive SPQR/Lib/libspqr.a -lblas -llapack \
      -L./shared -lcholmod -lsuitesparseconfig -lm && \
      ln -sf libspqr.so.1.3.3 shared/libspqr.so
   ld -shared -soname libcxsparse.so.3 -o shared/libcxsparse.so.3.1.3 \
      --whole-archive CXSparse/Lib/libcxsparse.a && \
      ln -sf libcxsparse.so.3.1.3 shared/libcxsparse.so
   ld -shared -soname libklu.so.1 -o shared/libklu.so.1.3.0 \
      --whole-archive KLU/Lib/libklu.a -L./shared -lamd -lbtf \
      -lsuitesparseconfig -lm && ln -sf libklu.so.1.3.0 shared/libklu.so
   ld -shared -soname libumfpack.so.5 -o shared/libumfpack.so.5.7.0 \
      --whole-archive UMFPACK/Lib/libumfpack.a -lblas -llapack -L./shared \
      -lamd -lcholmod -lsuitesparseconfig -lm && \
      ln -sf libumfpack.so.5.7.0 shared/libumfpack.so
}


package() {
   cd "${srcdir}"/SuiteSparse
   install -dm755 "${pkgdir}"/usr/{lib,include}
   
   for _lib in SuiteSparse_config AMD CAMD COLAMD BTF KLU LDL CCOLAMD UMFPACK CHOLMOD CXSparse SPQR; do
      make -C ${_lib} INSTALL_LIB="${pkgdir}"/usr/lib INSTALL_INCLUDE="${pkgdir}"/usr/include install
   done

   rm -f "${pkgdir}"/usr/lib/*.a
   cp -d shared/*.so* "${pkgdir}"/usr/lib/
   ldconfig -n "${pkgdir}"/usr/lib/
   chmod 644 "${pkgdir}"/usr/include/*.{h,hpp}
}
