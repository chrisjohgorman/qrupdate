# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Contributor: Marco Maso <demind@gmail.com>
# Contributor: Adrian Benson <adrian_benson@yahoo.co.nz>
# Contributor: Chris Gorman <chrisjohgorman@gmail.com>

pkgname=qrupdate64
_pkgname=qrupdate
pkgver=1.1.5
pkgrel=1
pkgdesc='Fortran library for fast updates of QR and Cholesky decompositionsi (64 bit version)'
url='https://sourceforge.net/projects/qrupdate'
makedepends=(gcc-fortran cmake)
depends=(lapack)
arch=(x86_64)
license=(GPL3)
source=(https://github.com/mpimd-csc/qrupdate-ng/archive/v$pkgver/$_pkgname-$pkgver.tar.gz
        qrupdate64.patch)
sha256sums=('912426f7cb9436bb3490c3102a64d9a2c3883d700268a26d4d738b7607903757'
            '6757505f43ab9ace1b867aba7f6b0f5bbda85a54c6c9061f5e447e6207a6abd6')

prepare() {
    patch -d $_pkgname-ng-$pkgver -p1 < qrupdate64.patch
}

build() {
  cmake -B build -S $_pkgname-ng-$pkgver \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_Fortran_FLAGS="-fdefault-integer-8" \
    -DBLAS_LIBRARIES=/usr/lib/libblas64.so \
    -DLAPACK_LIBRARIES=/usr/lib/liblapack64.so 
  cmake --build build
}

check() {
  cmake --build build --target test
}

package() {
  DESTDIR="$pkgdir" cmake --install build
#FIXME find way to do this in the source code
#  cd "$pkgdir"/usr/lib/cmake/
#  mv qrupdate qrupdate64
}
