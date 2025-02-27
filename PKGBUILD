# Maintainer: Gerard Ribugent <ribugent <at> gmail <dot> com>
# Maintainer: Georgel Preput <georgelpreput <at> mailbox <dot> org>
pkgname=databricks-cli-bin
_pkgname=databricks-cli
provides=($_pkgname)
conflicts=('python-databricks-cli' 'python-dbx')
pkgver=0.242.0
pkgrel=2
pkgdesc="Databricks CLI"
arch=('x86_64' 'aarch64')
url="https://github.com/databricks/cli"
license=('custom:databricks')
makedepends=('unzip')
depends=()
source_x86_64=("https://github.com/databricks/cli/releases/download/v${pkgver}/databricks_cli_${pkgver}_linux_amd64.zip")
source_aarch64=("https://github.com/databricks/cli/releases/download/v${pkgver}/databricks_cli_${pkgver}_linux_arm64.zip")
sha256sums_x86_64=('6d4c6a1ac2a36079b33e8dad6a41a400095f8da0dc79d26f53ce6c417d29bac1')
sha256sums_aarch64=('15b0c9619af92fed16f5e4a8adb7184834342beaba9a06928d5300358bc43f01')

package() {
	install -Dm0755 $srcdir/databricks $pkgdir/usr/bin/databricks
	install -Dm0644 $srcdir/LICENSE "$pkgdir/usr/share/licenses/$_pkgname/LICENSE"
}
