# Maintainer: Gerard Ribugent <ribugent <at> gmail <dot> com>
# Maintainer: Georgel Preput <georgelpreput <at> mailbox <dot> org>
pkgname=databricks-cli-bin
_pkgname=databricks-cli
provides=($_pkgname)
conflicts=('python-databricks-cli' 'python-dbx')
pkgver=0.241.1
pkgrel=2
pkgdesc="Databricks CLI"
arch=('x86_64' 'aarch64')
url="https://github.com/databricks/cli"
license=('custom:databricks')
makedepends=('unzip')
depends=()
source_x86_64=("https://github.com/databricks/cli/releases/download/v${pkgver}/databricks_cli_${pkgver}_linux_amd64.zip")
source_aarch64=("https://github.com/databricks/cli/releases/download/v${pkgver}/databricks_cli_${pkgver}_linux_arm64.zip")
sha256sums_x86_64=('452ce5b76d3aedf737f3effe7b4c246ba0e18d2d1ffe9b6a0277ea0c925acd7a')
sha256sums_aarch64=('c5460c93d958922cfa5063bc2a9e3056607190fbf11cc886a58e25c6a5b151fd')

package() {
	install -Dm0755 $srcdir/databricks $pkgdir/usr/bin/databricks
	install -Dm0644 $srcdir/LICENSE "$pkgdir/usr/share/licenses/$_pkgname/LICENSE"
}
