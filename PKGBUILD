# Maintainer: Bernhard Landauer <bernhard@manjaro.org>
# Author: Roman Gilg <subdiff@gmail.com>
# Contributor: Antonio Rojas <arojas@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

_pkgname=kwin
__pkgname=${_pkgname}ft
pkgname=$__pkgname-git
_pkgver=5.20.0
pkgver=5.22.80.r18962.gedc9640a2
pkgrel=1
pkgdesc='Drop-in replacement for KWin with additional libwayland wrapping Qt/C++ library Wrapland'
arch=(x86_64 aarch64)
url="https://gitlab.com/$__pkgname/$__pkgname"
license=(LGPL)
depends=(breeze-git
    kdisplay-git
    kinit-git
    kscreenlocker-git
    plasma-framework-git
    qt5-script
    wrapland-git
    xcb-util-cursor
    wlroots-git
    python)
makedepends=(extra-cmake-modules-git
    git
    kdoctools-git
    qt5-tools)
optdepends=('qt5-virtualkeyboard: virtual keyboard support for kwin-wayland')
provides=("$_pkgname" "$_pkgname-git" "$__pkgname")
conflicts=("$_pkgname" "$__pkgname")
source=("git+$url.git")
sha256sums=('SKIP')
install=$__pkgname.install

pkgver() {
  cd $__pkgname
  _ver="$(cat CMakeLists.txt | grep -m1 'set(PROJECT_VERSION' | cut -d '"' -f2 | tr - .)"
  echo "${_ver}.r$(git rev-list --count HEAD).g$(git rev-parse --short HEAD)"
}

prepare() {
  mkdir -p build
}

build() {
  cd build
  cmake ../$__pkgname -Wno-dev \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DCMAKE_INSTALL_LIBEXECDIR=lib \
    -DKDE_INSTALL_USE_QT_SYS_PATHS=ON \
    -DBUILD_TESTING=OFF
  make
}

package() {
  cd build
  make DESTDIR="$pkgdir" install
}
