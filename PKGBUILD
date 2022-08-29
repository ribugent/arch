# Maintainer: Gerard Ribugent <ribugent <at> gmail <dot> com>
pkgname=python-dbx
_name=dbx
pkgver=0.7.2
pkgrel=1
pkgdesc="DataBricks CLI eXtensions - aka dbx is a CLI tool for advanced Databricks jobs management."
arch=(any)
url="https://docs.databricks.com/dev-tools/dbx.html"
license=('CUSTOM')
depends=(
	'python>=3.8'
	"python-databricks-cli>=0.17" "python-databricks-cli<0.18"
	"python-click>=8.1.0" "python-click<9.0.0"
	"python-rich=12.5.1"
	"python-typer=0.6.1"
	"python-retry>=0.9.2" "python-retry<1.0.0"
	"python-requests>=2.24.0" "python-requests<3.0.0"
	"python-mlflow-skinny==1.28.0"
	"python-yaml>=6.0"
	"python-pydantic>=1.9.1"
	"python-cryptography>=3.3.1" "python-cryptography<38.0.0"
	"python-cookiecutter>=1.7.2" "python-cookiecutter<3.0.0"
	"python-jinja>=2.11.2"
	"python-aiohttp>=3.8.1"
	"python-pathspec>=0.9.0"

	"python-watchdog-git>=2.1.0" # The community package is stuck at 0.10.7-3
)
makedepends=(python-build python-installer python-wheel)
source=($pkgname-$pkgver.tar.gz::https://github.com/databrickslabs/dbx/archive/refs/tags/v$pkgver.tar.gz)
sha512sums=('339923dfd004c6900a3b2cbcba980ecfa172ff0bec37cfe6773af908d56373928a6cb9c8d18f2811ea02389b4b8133ee701f66e4a0c7a535341f16923488955a')

build() {
	cd "$_name-$pkgver"
	python -m build --wheel --no-isolation
}

package() {
	cd "$_name-$pkgver"
	python -m installer --destdir="$pkgdir" dist/*.whl
	install -Dm0644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
