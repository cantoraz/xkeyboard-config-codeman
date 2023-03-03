# Maintainer: Cantoraz Zhou <cantoraz@gmail.com>

pkgname=xkeyboard-config+codeman
pkgver=2.36
pkgrel=3
pkgdesc="X keyboard configuration files, extended with Codeman layout"
arch=(any)
license=('custom')
url="https://github.com/cantoraz/xkeyboard-config"
makedepends=('xorg-xkbcomp' 'libxslt' 'python' 'meson')
provides=('xkbdata' 'xkeyboard-config')
replaces=('xkbdata')
conflicts=('xkbdata' 'xkeyboard-config')
source=(https://xorg.freedesktop.org/archive/individual/data/${pkgname%+*}/${pkgname%+*}-${pkgver}.tar.xz{,.sig}
        alujiskeys.patch::https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config/-/commit/dc1534b4b0cf2153e4b8848310efc8393fb73830.patch
        backslahes-instead-of-slashes.patch::https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config/-/commit/8ac41c50ab0aa7cd3a7e94313074115de2a172d2.patch)
validpgpkeys=('FFB4CCD275AAA422F5F9808E0661D98FC933A145') # Sergey Udaltsov <sergey.udaltsov@gmail.com>
#validpgpkeys=('15CFA5C595041D2CCBEA155F1732AA424A0E86B4') # "Sergey Udaltsov (For GNOME-related tasks) <svu@gnome.org>"
sha256sums=('1f1bb1292a161d520a3485d378609277d108cd07cde0327c16811ff54c3e1595'
            'SKIP'
            'e3ae0fedc48ff32e707372efa211d06620bec8b58b0cca5f1eb991639b2867b8'
            '7a16283051c6bba396ebd81756e02a5c185566f1b843456afa80876155140c14')

prepare() {
  cd ${pkgname%+*}-${pkgver}
  # FS##75007 / https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config/-/issues/325
  patch -Np1 -i ../alujiskeys.patch
  patch -Np1 -i ../backslahes-instead-of-slashes.patch
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