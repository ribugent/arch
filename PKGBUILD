# Maintainer: Gerard Ribugent <ribugent <at> gmail <dot> com>
# Maintainer: Georgel Preput <georgelpreput <at> mailbox <dot> org>
pkgname=databricks-cli-bin
_pkgname=databricks-cli
provides=($_pkgname)
conflicts=('python-databricks-cli' 'python-dbx')
pkgver=0.262.0
pkgrel=1
pkgdesc="Databricks CLI"
arch=('x86_64' 'aarch64')
url="https://github.com/databricks/cli"
license=('custom:databricks')
makedepends=('unzip')
depends=()
source_x86_64=("https://github.com/databricks/cli/releases/download/v${pkgver}/databricks_cli_${pkgver}_linux_amd64.zip")
source_aarch64=("https://github.com/databricks/cli/releases/download/v${pkgver}/databricks_cli_${pkgver}_linux_arm64.zip")
sha256sums_x86_64=('a6a06ae52edf7557c22f9ce021608888e42c5805a55d212b46c96e3ecac5b142')
sha256sums_aarch64=('d03f52c46a98634f826a75030100394bd59d5dd6caa79c4b38187976fbdb902a')

package() {
	install -Dm0755 $srcdir/databricks $pkgdir/usr/bin/databricks
	install -Dm0644 $srcdir/LICENSE "$pkgdir/usr/share/licenses/$_pkgname/LICENSE"
}
