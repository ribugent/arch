# Maintainer: Gerard Ribugent <ribugent <at> gmail <dot> com>
pkgname=python-dbx
_name=dbx
pkgver=0.6.10
pkgrel=1
pkgdesc="DataBricks CLI eXtensions - aka dbx is a CLI tool for advanced Databricks jobs management."
arch=(any)
url="https://docs.databricks.com/dev-tools/dbx.html"
license=('CUSTOM')
depends=(
	'python>=3.8'
	"python-databricks-cli>=0.16.4"
	"python-click>=7.1.2"
	"python-retry>=0.9.2"
	"python-requests>=2.24.0"
	"python-mlflow>=1.23.0"
	"python-scipy>=1.8.0"
	"python-tqdm>=4.50.0"
	"python-azure-identity>=1.7.1"
	"python-azure-mgmt-datafactory>=2.2.0"
	"python-azure-mgmt-subscription>=3.0.0"
	"python-ruamel-yaml>=0.17.10"
	"python-cryptography>=3.3.1" "python-cryptography<38.0.0"
	"python-emoji>=1.6.1"
	"python-cookiecutter>=1.7.2"
	"python-jinja>=2.11.2"
)
makedepends=(python-build python-installer python-wheel)
source=($pkgname-$pkgver.tar.gz::https://github.com/databrickslabs/dbx/archive/refs/tags/v$pkgver.tar.gz)
sha512sums=('ade8d0915330ccf4cffb1f42210ed2bdccf1623fc41fff377553e90f0f648a3292d368017ecb609b963ad8c5a6def33f6c675d932ff803a79211290db132ac93')

build() {
	cd "$_name-$pkgver"
	python -m build --wheel --no-isolation
}

package() {
	cd "$_name-$pkgver"
	python -m installer --destdir="$pkgdir" dist/*.whl
}
