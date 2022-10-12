# Maintainer: Cantoraz Zhou <cantoraz@gmail.com>

pkgname=xkeyboard-config+codeman
pkgver=2.37
pkgrel=1
pkgdesc="X keyboard configuration files, extended with Codeman layout"
arch=(any)
license=('custom')
url="https://github.com/cantoraz/xkeyboard-config-codeman"
makedepends=('xorg-xkbcomp' 'libxslt' 'python' 'meson' 'git')
provides=('xkbdata' 'xkeyboard-config')
replaces=('xkbdata')
conflicts=('xkbdata' 'xkeyboard-config')
source=(${pkgname}-${pkgver}::git+https://github.com/cantoraz/xkeyboard-config-codeman.git#tag=${pkgname}-${pkgver})
validpgpkeys=('FFB4CCD275AAA422F5F9808E0661D98FC933A145') # Sergey Udaltsov <sergey.udaltsov@gmail.com>
sha256sums=('SKIP')

build() {
  arch-meson ${pkgname}-${pkgver} build \
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
  install -m644 ${pkgname}-${pkgver}/COPYING "${pkgdir}/usr/share/licenses/${pkgname%+*}/"
}
