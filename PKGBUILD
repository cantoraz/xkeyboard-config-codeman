# Maintainer: Cantoraz Zhou <cantoraz@gmail.com>

pkgname=xkeyboard-config+codeman
pkgver=2.40
pkgrel=1
pkgdesc="X keyboard configuration files, extended with Codeman layout"
arch=(any)
license=('custom')
url="https://github.com/cantoraz/xkeyboard-config"
makedepends=('xorg-xkbcomp' 'libxslt' 'python' 'meson') # 'git')
provides=('xkbdata' 'xkeyboard-config')
replaces=('xkbdata')
conflicts=('xkbdata' 'xkeyboard-config')
# https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config
source=(https://xorg.freedesktop.org/archive/individual/data/${pkgname%+*}/${pkgname%+*}-${pkgver}.tar.xz{,.sig}
        codeman.patch)
sha256sums=('7a3dba1bec7dc7191432da021242d17c9cf6c89690e6c57b0de048ff8c9d2ae3'
            'SKIP'
            'a0e17094ca5cfbcdfe5201af3b1b520712c4760a5453ea3696bbbade69247ba9')
validpgpkeys=('FFB4CCD275AAA422F5F9808E0661D98FC933A145') # Sergey Udaltsov <sergey.udaltsov@gmail.com>

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

# check() {
#   meson test -C build --print-errorlogs
# }

package() {

  DESTDIR="$pkgdir" ninja -C build install

  install -m755 -d "${pkgdir}/var/lib/xkb"
  install -m755 -d "${pkgdir}/usr/share/licenses/${pkgname%+*}"
  install -m644 ${pkgname%+*}-${pkgver}/COPYING "${pkgdir}/usr/share/licenses/${pkgname%+*}/"
}
