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
source=("$pkgname::git+$url.git")
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/$pkgname"
  printf "0.1.r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package() {
  cd "$srcdir/$pkgname"
  install -Dm755 waydroid-focus "$pkgdir/usr/bin/waydroid-focus"
  install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
