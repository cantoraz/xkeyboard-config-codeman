# Maintainer: Cantoraz Zhou <cantoraz@gmail.com>

pkgname=xkeyboard-config+codeman
pkgver=2.43
pkgrel=1
pkgdesc="X keyboard configuration files, extended with Codeman layout"
arch=(any)
license=('LicenseRef-xkeyboard-config')
url="https://github.com/cantoraz/xkeyboard-config"
makedepends=('xorg-xkbcomp' 'libxslt' 'python' 'meson') # 'git')
provides=('xkbdata' 'xkeyboard-config')
replaces=('xkbdata')
conflicts=('xkbdata' 'xkeyboard-config')
# https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config
source=(https://xorg.freedesktop.org/archive/individual/data/${pkgname%+*}/${pkgname%+*}-${pkgver}.tar.xz{,.sig}
        codeman.patch)
sha256sums=('c810f362c82a834ee89da81e34cd1452c99789339f46f6037f4b9e227dd06c01'
            'SKIP'
            'e603dc88665ef3069efc8756144c0492cf29b677163cc0368342db30c1135d3e')
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
  install -Dt "$pkgdir/usr/share/licenses/${pkgname%+*}" -m644 ${pkgname%+*}-$pkgver/COPYING
}
