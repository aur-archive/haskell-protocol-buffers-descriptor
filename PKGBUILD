# Maintainer: Sean Bartell <wingedtachikoma@gmail.com>
_hkgname=protocol-buffers-descriptor
pkgname=haskell-$_hkgname
pkgver=2.0.14
pkgrel=1
pkgdesc="Uses protocol-buffers package"
arch=('i686' 'x86_64')
url="http://hackage.haskell.org/package/$_hkgname"
license=('BSD')
depends=('ghc>=7.6.2' 'haskell-protocol-buffers')
makedepends=()
install=$pkgname.install
source=(http://hackage.haskell.org/packages/archive/$_hkgname/$pkgver/$_hkgname-$pkgver.tar.gz)
md5sums=('6635e3289390a58b101b5f5c8701e0ba')
sha256sums=('43d67ff6505a9db5a25e348e2198948e4e421be62aabf51313e439a252ad7775')

build() {
  cd "$srcdir/$_hkgname-$pkgver"

  runhaskell Setup configure -O -p --enable-split-objs --enable-shared \
    --prefix=/usr --docdir="/usr/share/doc/$pkgname" \
    --libsubdir=\$compiler/site-local/\$pkgid
  runhaskell Setup build
  runhaskell Setup haddock
  runhaskell Setup register   --gen-script
  runhaskell Setup unregister --gen-script
  sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}

package() {
  cd "$srcdir/$_hkgname-$pkgver"

  install -D -m744 register.sh   "$pkgdir/usr/share/haskell/$pkgname/register.sh"
  install     -m744 unregister.sh "$pkgdir/usr/share/haskell/$pkgname/unregister.sh"
  install -d -m755 "$pkgdir/usr/share/doc/ghc/html/libraries"
  ln -s "/usr/share/doc/$pkgname/html" "$pkgdir/usr/share/doc/ghc/html/libraries/$_hkgname"
  runhaskell Setup copy --destdir="$pkgdir"
  install -D -m644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  rm -f "$pkgdir/usr/share/doc/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
