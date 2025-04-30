# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Andrey Mikhaylenko <neithere at gmail dot com>
# Contributor: JisuWoniu <jswn@jswn9945.xyz>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=argcomplete
pkgname="${_py}-${_pkg}"
pkgver=3.5.3
pkgrel=1
_pkgdesc=(
  'Easy, extensible command line'
  'tab completion of arguments for'
  'your Python script'
)
pkgdesc="${_pkgdesc[*]}"
_http="https://github.com"
_ns="kislyuk"
url="${_http}/${_ns}/${_pkg}"
arch=(
  'any'
)
license=(
  'Apache-2.0'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  'git'
  "${_py}-build"
  "${_py}-hatch-vcs"
  "${_py}-hatchling"
  "${_py}-installer"
  "${_py}-wheel"
)
checkdepends=(
  'fish'
  "${_py}-pexpect"
  "${_py}-pip"
  'tcsh'
  'zsh'
)
source=(
  "${_pkg}::git+${url}#tag=v${pkgver}"
)
sha512sums=(
  '446593154b8c16f2d280ed5727723b808c5873cfc2c4715a96e8e68ecc0572d0dc2cca8992e41ea9af6d6f88c53f36ac55583139ea659a173fc2186ee9221520'
)
validpgpkeys=(
  # Andrey Kislyuk <kislyuk@gmail.com>
  '29BCBADB4ECAAAC2382699388AFAFCD242818A52'
)

build() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      "build" \
      --wheel \
      --no-isolation
}

check() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      "venv" \
    --system-site-packages \
    "test-venv"
  "test-venv/bin/${_py}" \
    -m \
      "installer" \
      "dist/"*".whl"
  PATH="${PWD}/test-venv/bin/:${PATH}" \
  "test-venv/bin/${_py}" \
    "test/test.py" \
      -v
}

package() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      "installer" \
      --destdir="${pkgdir}" \
      "dist/"*".whl"
  # Disabled again, see
  # https://gitlab.archlinux.org/archlinux/packaging/packages/python-argcomplete/-/issues/3
  # local \
  #   _site_packages="$( \
  #     "${_py}" \
  #       -c \
  #         "from distutils.sysconfig import get_python_lib; print(get_python_lib())")"
  # install \
  #   -dm755 \
  #     "${pkgdir}/usr/share/bash-completion/completions" \
  #     "${pkgdir}/usr/share/zsh/site-functions"
  # ln \
  #   -s \
  #     "../../../..${_site_packages}/${_pkg}/bash_completion.d/_python-argcomplete" \
  #     -t \
  #     "${pkgdir}/usr/share/bash-completion/completions/"
  # ln \
  #   -s \
  #   "../../../..${_site_packages}/${_pkg}/bash_completion.d/_python-argcomplete" \
  #   -t \
  #   "${pkgdir}/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
