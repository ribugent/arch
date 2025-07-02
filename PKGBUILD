# Maintainer: Gerard Ribugent <ribugent <at> gmail <dot> com>
# Maintainer: Georgel Preput <georgelpreput <at> mailbox <dot> org>
pkgname=databricks-cli-bin
_pkgname=databricks-cli
provides=($_pkgname)
conflicts=('python-databricks-cli' 'python-dbx')
pkgver=0.258.0
pkgrel=1
pkgdesc="Databricks CLI"
arch=('x86_64' 'aarch64')
url="https://github.com/databricks/cli"
license=('custom:databricks')
makedepends=('unzip')
depends=()
source_x86_64=("https://github.com/databricks/cli/releases/download/v${pkgver}/databricks_cli_${pkgver}_linux_amd64.zip")
source_aarch64=("https://github.com/databricks/cli/releases/download/v${pkgver}/databricks_cli_${pkgver}_linux_arm64.zip")
sha256sums_x86_64=('f0b56853d5f16ab38162620f31d1387b6be763efe58b33d7d0a20c440e4c4647')
sha256sums_aarch64=('740a564d2d6c9bb7a0145778a6eec1794e31437d0ceecf70cfabc589470b2641')

package() {
	install -Dm0755 $srcdir/databricks $pkgdir/usr/bin/databricks
	install -Dm0644 $srcdir/LICENSE "$pkgdir/usr/share/licenses/$_pkgname/LICENSE"
}
