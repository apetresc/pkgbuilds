# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Maintainer: Peter Jung <ptr1337@archlinux.org>
# Maintainer: Adrian Petrescu <adrian@apetre.sc>

_pkgbasename=ghostty
pkgname=${_pkgbasename}-font-bitmap-glyphs
pkgver=1.0.0
pkgrel=1
pkgdesc='Fast, native, feature-rich terminal emulator pushing modern features - sin-ack fork with fix for pixel-perfect bitmap fonts'
arch=(x86_64 aarch64 i686)
url="https://github.com/sin-ack/${_pkgbasename}#font-bitmap-glyphs"
provides=('ghostty')
conflicts=('ghostty')
license=(MIT)
depends=(bzip2
         fontconfig libfontconfig.so
         freetype2 libfreetype.so
         gcc-libs # ld-linux-x86-64.so
         glibc # libc.so libm.so
         glib2 libglib-2.0.so libgio-2.0.so libgobject-2.0.so
         gtk4 libgtk-4.so
         harfbuzz libharfbuzz.so
         libadwaita libadwaita-1.so
         libpng
         oniguruma # libonig.so
         pixman
         zlib)
makedepends=(pandoc-cli
             zig)
_archive="$pkgname-$pkgver"
source=("git+https://github.com/sin-ack/${_pkgbasename}#branch=font-bitmap-glyphs")
sha256sums=('SKIP')

prepare() {
  cd "${srcdir}/${_pkgbasename}"
	ZIG_GLOBAL_CACHE_DIR="$srcdir/zig-global-cache/" ./nix/build-support/fetch-zig-cache.sh
}

build() {
  cd "${srcdir}/${_pkgbasename}"
	zig build \
		--summary all \
		--prefix "$PWD/build/usr" \
		--system "$srcdir/zig-global-cache/p" \
		-Doptimize=ReleaseFast \
		-Dcpu=baseline \
		-Dpie=true \
		-Demit-docs
}

package() {
	depends+=(ghostty-shell-integration
	          ghostty-terminfo)
  cd "${srcdir}/${_pkgbasename}"
	cp -a build/* "$pkgdir/"
	install -Dm0644 -t "$pkgdir/usr/share/licenses/$pkgname/" LICENSE
	rm -r "$pkgdir"/usr/share/terminfo
	rm -r "$pkgdir"/usr/share/ghostty/shell-integration
}
