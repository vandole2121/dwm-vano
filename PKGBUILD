# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.3
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="https://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2')
source=(dwm.desktop
        https://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
        https://dwm.suckless.org/patches/fullgaps/dwm-fullgaps-toggle-20200830.diff
        https://dwm.suckless.org/patches/statuspadding/dwm-statuspadding-6.3.diff
        https://dwm.suckless.org/patches/rotatestack/dwm-rotatestack-20161021-ab9571b.diff
        https://dwm.suckless.org/patches/hide_vacant_tags/dwm-hide_vacant_tags-6.3.diff
        vano-patch.diff
        vano-color-patch.diff
        config.h)
sha256sums=('bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81'
            'badaa028529b1fba1fd7f9a84f3b64f31190466c858011b53e2f7b70c6a3078d'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  cp "$srcdir/config.h" config.h
  patch < ../dwm-fullgaps-toggle-20200830.diff
  patch < ../dwm-statuspadding-6.3.diff
  patch < ../dwm-rotatestack-20161021-ab9571b.diff
  patch < ../dwm-hide_vacant_tags-6.3.diff
  patch < ../vano-patch.diff
  patch < ../vano-color-patch.diff
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
  install -Dm644 "$srcdir/dwm.desktop" "$pkgdir/usr/share/xsessions/dwm.desktop"
}
