# Contributor: Adrian Petrescu <apetresc@gmail.com>
# Maintainer: Adrian Petrescu <apetresc@gmail.com>

pkgname=sabaki
pkgver=0.40.0
pkgrel=1
pkgdesc='An elegant SGF editor for the game of Go'
arch=('any')
url='http://sabaki.yichuanshen.de/'
license=('MIT')
depends=('nodejs' 'gconf')
makedepends=('npm')
install=${pkgname}.install
source=("https://github.com/SabakiHQ/Sabaki/archive/v${pkgver}.tar.gz"
        "${pkgname}.desktop"
        'sabaki.xml')
md5sums=('553c1ac7cf135bd84bf3a0b91385f4dd'
         'b39f3b91292cb3983124bd38035fbd8e'
         'efbd547e892c7781a5ece702d389dd9e')


build() {
  cd $srcdir/Sabaki-$pkgver

  npm install --cache "${srcdir}/npm-cache"
  npm run build
}

check() {
  cd $srcdir/Sabaki-$pkgver
  npm test
}

package() {
  mkdir $pkgdir/opt

  cp -r $srcdir/Sabaki-$pkgver/dist/linux-unpacked $pkgdir/opt/Sabaki
  install -Dm644 ${srcdir}/${pkgname}.desktop ${pkgdir}/usr/share/applications/${pkgname}.desktop
  install -Dm644 ${srcdir}/${pkgname}.xml ${pkgdir}/usr/share/mime/packages/${pkgname}.xml
}
