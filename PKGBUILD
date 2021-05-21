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
source=($pkgname-$pkgver.tar.gz::https://github.com/DataDog/datadogpy/archive/refs/tags/v0.41.0.tar.gz)
sha256sums=('e441e81c173413fc05fe9379d6335453d7d1ffbf04c00f18fde16197234dbdfd')

build() {
	cd "$pkgname-$pkgver"
}

package() {
	cd "$pkgname-$pkgver"
	/usr/bin/python setup.py install --root="$pkgdir/"
}
