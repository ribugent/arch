# Maintainer: Gerard Ribugent <ribugent@gmail.com>
pkgname=datadogpy
pkgver=0.41.0
pkgrel=1
pkgdesc="The Datadog Python library and dogshell"
arch=(any)
url="https://github.com/DataDog/datadogpy"
license=('BSD')
depends=(
	'python>=3.5'
	'python-requests>=2.6.0'
)
provides=(datadog-dogshell)
makedepends=(python-setuptools)
source=($pkgname-$pkgver.tar.gz::https://github.com/DataDog/datadogpy/archive/refs/tags/v$pkgver.tar.gz)
sha512sums=('4eee789f6582cdee2e39491a141e8716d20bbee68475ad38a8b311481929b4c0996b53ea19636e0988bb554b1a4451ac95eefa4ee3e005726e7da111cb9d4960')

build() {
	cd "$pkgname-$pkgver"
}

package() {
	cd "$pkgname-$pkgver"
	/usr/bin/python setup.py install --root="$pkgdir/"
}
