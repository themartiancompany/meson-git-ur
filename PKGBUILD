# Maintainer: nontlikeuname
# Contributor: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Contributor: Truocolo <truocolo@aol.com>

_py="python"
_pkg="meson"
pkgname="${_pkg}-git"
pkgver=0.63.0rc1.r10.c2c9359d4
pkgrel=1
_pkgdesc=(
  "SCons-like build system that use python"
  "as a front-end language and Ninja as a building backend")
pkgdesc="${_pkgdesc[*]}"
arch=(
  any)
_gh="https://github.com"
_ns="${_pkg}build"
url="http://${_ns}.com/"
_url="${_gh}/${_ns}/${_pkg}"
license=(
  'Apache')
depends=(
  "${_py}"
  'ninja')
makedepends=(
  'git')
provides=(
  "${_pkg}"
  "${_py}-${_pkg}"
  "${_py}-${_pkg}-git")
conflicts=(
  "${_pkg}"
  "${_py}-${_pkg}")
source=(
  "git+${_url}"
  "arch-${_pkg}")
md5sums=(
  'SKIP'
  'e1a31b2f4993cf627c640cf6795a17f5')

pkgver() {
  cd \
    "${srcdir}/${_pkg}"
  printf \
    "%s" \
    "$(git \
         describe \
	 --long | \
	 sed \
	   's/\([^-]*-\)g/r\1/;s/-/./g')"
}

package() {
  cd \
    "${srcdir}/${_pkg}"
  "${_py}" \
    setup.py \
      install \
      --root="${pkgdir}" \
      --optimize=1
  install \
    -Dm644 \
    COPYING \
    "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
  for _f \
    in data/syntax-highlighting/vim/*/*; do
    install \
      -Dt \
      "${pkgdir}/usr/share/vim/vimfiles/$( \
        basename \
	  "$(dirname \
	       "${_f}")")" \
      -m644 \
      "${_f}"
  done
  install \
    -Dt \
      "${pkgdir}/usr/share/zsh/site-functions" \
    -m644 \
      data/shell-completions/zsh/*

  # Arch packaging helper
  install \
    -D \
      ../arch-meson \
    -t \
      "${pkgdir}/usr/bin"
}
