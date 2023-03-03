# Maintainer: Cantoraz Zhou <cantoraz@gmail.com>

pkgname=xkeyboard-config+codeman
pkgver=2.37
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
sha256sums=('eb1383a5ac4b6210d7c7302b9d6fab052abdf51c5d2c9b55f1f779997ba68c6c'
            'SKIP'
            'a1e8f755d969c9e10327267445de9d1a8c109b45db224d187554225676f952be')

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
