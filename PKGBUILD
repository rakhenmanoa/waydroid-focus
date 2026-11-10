# Maintainer: rakhenmanoa
pkgname=waydroid-focus
pkgver=0.1
pkgrel=1
pkgdesc="Lance une appli Waydroid en libérant le GPU pour elle (gel des autres processus, réglages Android)"
arch=('any')
url="https://github.com/rakhenmanoa/waydroid-focus"
license=('0BSD')
depends=('bash' 'sudo' 'waydroid')
makedepends=('git')
# Le clone ne doit pas s'appeler comme le script : makepkg télécharge les sources
# dans le dossier courant, et un "waydroid-focus" y existe déjà.
_src="$pkgname-src"
source=("$_src::git+$url.git")
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/$_src"
  printf "0.1.r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package() {
  cd "$srcdir/$_src"
  install -Dm755 waydroid-focus "$pkgdir/usr/bin/waydroid-focus"
  install -Dm644 disable.list.example "$pkgdir/usr/share/doc/$pkgname/disable.list.example"
  install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
