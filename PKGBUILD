# Maintainer: Cantoraz Zhou <cantoraz@gmail.com>

pkgname=xkeyboard-config+codeman
pkgver=2.39
pkgrel=1
pkgdesc="X keyboard configuration files, extended with Codeman layout"
arch=(any)
license=('custom')
url="https://github.com/cantoraz/xkeyboard-config"
makedepends=('xorg-xkbcomp' 'libxslt' 'python' 'meson')
provides=('xkbdata' 'xkeyboard-config')
replaces=('xkbdata')
conflicts=('xkbdata' 'xkeyboard-config')
source=(https://xorg.freedesktop.org/archive/individual/data/${pkgname%+*}/${pkgname%+*}-${pkgver}.tar.xz{,.sig}
        codeman.patch)
validpgpkeys=('FFB4CCD275AAA422F5F9808E0661D98FC933A145') # Sergey Udaltsov <sergey.udaltsov@gmail.com>
sha256sums=('5ac5f533eff7b0c116805fe254fd79b2c9882700a4f9f2c070f8c4eae5aaa682'
            'SKIP'
            'bf64718f0e9ea889a18f21b32c62b811dfa2da8a0a74a21af8b90ac6b63fc930')

prepare() {
  cd ${pkgname%+*}-${pkgver}
  patch -Np1 -i ../codeman.patch
}

build() {
  arch-meson ${pkgname%+*}-${pkgver} build \
        -D xkb-base="/usr/share/X11/xkb" \
        -D compat-rules=true \
        -D xorg-rules-symlinks=true

  # Print config
  meson configure build

  ninja -C build

 }

 package() {

  DESTDIR="$pkgdir" ninja -C build install

  install -m755 -d "${pkgdir}/var/lib/xkb"
  install -m755 -d "${pkgdir}/usr/share/licenses/${pkgname%+*}"
  install -m644 ${pkgname%+*}-${pkgver}/COPYING "${pkgdir}/usr/share/licenses/${pkgname%+*}/"
}
