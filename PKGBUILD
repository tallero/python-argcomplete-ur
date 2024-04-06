# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Andrey Mikhaylenko <neithere at gmail dot com>

pkgname=python-argcomplete
_pyname=argcomplete
pkgver=2.0.0
pkgrel=2
pkgdesc='Easy, extensible command line tab completion of arguments for your Python script'
url='https://github.com/kislyuk/argcomplete'
arch=('any')
license=('Apache-2.0')
depends=('python')
makedepends=('git' 'python-setuptools')
checkdepends=('python-pexpect' 'tcsh' 'fish' 'python-pip')
source=(${_pyname}::"git+$url?signed#tag=v$pkgver")
sha512sums=('20c09309c8d1ec1363d8f987390ef27bf3f36cb0d68e999c82242c7c8318a15a8908976a4b348db973bfd54084242e3b271b4e46271275bbeefe306aea9405ec')
validpgpkeys=('29BCBADB4ECAAAC2382699388AFAFCD242818A52') # Andrey Kislyuk <kislyuk@gmail.com>

pkgver() {
  cd ${_pyname}
  git describe --tags --match 'v*' | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd ${_pyname}
  python setup.py build
}

check() {
  cd ${_pyname}
  # workaround for https://github.com/kislyuk/argcomplete/issues/337
  echo "set enable-bracketed-paste off" > .inputrc
  INPUTRC=$PWD/.inputrc python test/test.py -v
}

package() {
  cd ${_pyname}
  python setup.py install -O1 --root="${pkgdir}" --skip-build
}

# vim: ts=2 sw=2 et:
