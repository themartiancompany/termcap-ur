# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer:  Pellegrino Prevete <cGVsbGVncmlub3ByZXZldGVAZ21haWwuY29tCg== | base -d>
# Maintainer:  Truocolo <truocolo@aol.com>
# Maintainer: Beej <beej@beej.us>
# Maintainer: Ivan c00kiemon5ter Kanakarakis <ivan.kanak@gmail.com>
pkgname="termcap"
pkgver="1.3.1"
pkgrel=6
pkgdesc="Enables programs to use display computer terminals in a device-independent manner"
arch=(
  'i686'
  'x86_64'
  'aarch64'
  'arm'
)
url="http://www.catb.org/~esr/terminfo/"
license=(
  "GPL"
)
source=(
  "http://ftp.gnu.org/gnu/${pkgname}/${pkgname}-${pkgver}.tar.gz"
)
sha256sums=(
  '91a0e22e5387ca4467b5bcb18edf1c51b930262fd466d5fda396dd9d26719100'
)

_cc="$( \
  command \
    -v \
    "cc" \
    "gcc" \
    "clang" | \
  head \
    -n \
    1)"

_build() {
  local \
    _file="${1}" \
    _opts=()
  _opts=(
    -DHAVE_STRING_H=1
    -DHAVE_UNISTD_H=1
    -DSTDC_HEADERS=1
  )
  "${_cc}" \
    -fPIC \
    -c \
    "${_file}" \
    "${_opts[@]}"
}

build() {
  cd \
    "${srcdir}/${pkgname}-${pkgver}"
  _build \
    "${pkgname}.c"
  _build \
    "tparam.c"
  _build \
    "version.c"
  gcc \
    -shared \
    -Wl,-soname,"lib${pkgname}.so" \
    -o \
      "lib${pkgname}.so.${pkgver}" \
    "${pkgname}.o" \
    "tparam.o" \
    "version.o"
}

package() {
  cd \
    "${srcdir}/${pkgname}-${pkgver}"
  install \
    -Dm755 \
    "lib${pkgname}.so.${pkgver}" \
    "${pkgdir}/usr/lib/lib${pkgname}.so.${pkgver}"
  ln \
    -s \
    "${pkgdir}/usr/lib/lib${pkgname}.so.${pkgver}" \
    "${pkgdir}/usr/lib/lib${pkgname}.so"
    for infofile \
      in termcap.info* ; do
      install \
	-Dm644 \
	"${srcdir}/${pkgname}-${pkgver}/${infofile}" \
	"${pkgdir}/usr/share/info/${infofile}"
    done
}

# vim:set sw=2 sts=-1 et:
