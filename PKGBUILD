# Maintainer: talgarr
pkgname=yubikey-notifier-git
_pkgname=yubikey-notifier
pkgver=r9.ef5d003
pkgrel=1
pkgdesc="Desktop notifier for yubikey-touch-detector D-Bus events"
arch=('x86_64')
url="https://github.com/talgarr/yubikey-notifier"
license=('MIT')
depends=('glibc')
makedepends=('git' 'go')
optdepends=('yubikey-touch-detector: emit the D-Bus signals this tool listens for')
provides=('yubikey-notifier')
conflicts=('yubikey-notifier')
source=("$_pkgname::git+https://github.com/talgarr/yubikey-notifier.git")
sha256sums=('SKIP')

pkgver() {
    cd "$_pkgname"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
    cd "$_pkgname"
    go build -trimpath -ldflags "-s -w" -o yubikey-notifier .
}

package() {
    cd "$_pkgname"
    install -Dm755 yubikey-notifier "$pkgdir/usr/bin/yubikey-notifier"
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}