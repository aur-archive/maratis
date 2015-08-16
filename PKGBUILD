# Maintainer: TDY <tdy@archlinux.info>

pkgname=maratis
pkgver=3.1d_beta
pkgrel=1
pkgdesc="A portable, simple, and visual game development tool for artists and developers"
arch=('i686' 'x86_64')
url="http://www.maratis3d.org/"
license=('GPL')
depends=('libgl' 'libsndfile' 'libxxf86vm' 'openal')
[[ $CARCH == x86_64 ]] && depends=(${depends[@]/#/lib32-})
[[ $CARCH == i686 ]] && makedepends=('chrpath')
source=(http://maratis.googlecode.com/files/Maratis-${pkgver/_/-}-linux-x86.zip
        MaratisEditor.sh
        MaratisEditor.desktop
        MaratisPlayer.sh
        MaratisPlayer.desktop)
md5sums=('91de7a8b9e45dc681e7a82e5eafbf1d0'
         'ca34ea59336bffe2660ca700eea05354'
         '51d2ecdf6aa3b20a3c6728c32bdce8fc'
         'a600295a5b4b3c8f20ee8c53d61f80ec'
         'ba4f9ba9dd24a8dde370f82c6b0f7d12')

build() {
  cd "$srcdir/Maratis-${pkgver/_/-}-linux-x86/Bin"

  # delete rpaths (unfortunately only for i686; chrpath can't do cross-arch formatting)
  if [[ $CARCH == i686 ]]; then
    chrpath -d libM{Engine,Core}.so Maratis{Editor,Player}
  fi
}

package() {
  cd "$srcdir/Maratis-${pkgver/_/-}-linux-x86/Bin"

  # libs
  install -Dm755 libMEngine.so "$pkgdir/usr/lib/libMEngine.so"
  install -Dm755 libMCore.so "$pkgdir/usr/lib/libMCore.so"

  # gui
  install -dm755 "$pkgdir/opt/$pkgname/gui/meshs"
  install -m644 gui/*.* "$pkgdir/opt/$pkgname/gui"
  install -m644 gui/meshs/*.* "$pkgdir/opt/$pkgname/gui/meshs"
  install -Dm644 font/default.tga "$pkgdir/opt/$pkgname/font/default.tga"

  # bins
  install -Dm755 MaratisEditor "$pkgdir/opt/$pkgname/MaratisEditor"
  install -Dm755 MaratisPlayer "$pkgdir/opt/$pkgname/MaratisPlayer"
  install -Dm755 "$srcdir/MaratisEditor.sh" "$pkgdir/usr/bin/MaratisEditor"
  install -Dm755 "$srcdir/MaratisPlayer.sh" "$pkgdir/usr/bin/MaratisPlayer"

  # desktop entries
  install -Dm644 "$srcdir/MaratisEditor.desktop" \
    "$pkgdir/usr/share/applications/MaratisEditor.desktop"
  install -Dm644 "$srcdir/MaratisPlayer.desktop" \
    "$pkgdir/usr/share/applications/MaratisPlayer.desktop"
  install -Dm644 gui/Title.png "$pkgdir/usr/share/pixmaps/$pkgname.png"
}

# vim:set ts=2 sw=2 et:
