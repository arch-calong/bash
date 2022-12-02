# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Bernhard Landauer <bernhard[at]manjaro[dot]org>
# Contributor: Helmut Stult

# Arch credits:
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Contributor:  Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: Aaron Griffin <aaron@archlinux.org>

pkgname=('bash' 'bashrc-manjaro')
pkgbase=bash
_basever=5.2
_patchlevel=0
pkgver=${_basever}.${_patchlevel}
pkgrel=1
pkgdesc="The GNU Bourne Again shell"
arch=('x86_64')
url="https://www.gnu.org/software/bash/bash.html"
license=('GPL')
depends=('bash-completion')
source=("https://ftp.gnu.org/gnu/bash/bash-$_basever.tar.gz"{,.sig}
    'dot.bashrc'
    'dot.bash_profile'
    'dot.bash_logout'
    'system.bashrc'
    'system.bash_logout')
sha256sums=('a139c166df7ff4471c5e0733051642ee5556c1cc8a4a78f145583c5c81ab32fb'
            'SKIP'
            'dc8186a0808a4fc2ffeabafee16cf1ffc946a77426147866b7b35502deafe75e'
            'e149407c2bee17779caec70a7edd3d0000d172e7e4347429b80cb4d55bcec9c2'
            '4330edf340394d0dae50afb04ac2a621f106fe67fb634ec81c4bfb98be2a1eb5'
            '5fdc20c44bc9058f728d11111327f4dbb5598fec4d948dd5265211598667f9f0'
            '025bccfb374a3edce0ff8154d990689f30976b78f7a932dc9a6fcef81821811e')
validpgpkeys=('7C0135FB088AAF6C66C650B9BB5869F064EA74AB') # Chet Ramey

if [[ $((10#${_patchlevel})) -gt 0 ]]; then
  for (( _p=1; _p<=$((10#${_patchlevel})); _p++ )); do
    source=(${source[@]} https://ftp.gnu.org/gnu/bash/bash-$_basever-patches/bash${_basever//.}-$(printf "%03d" $_p){,.sig})
  done
fi

prepare() {
  cd $pkgbase-$_basever

  for (( _p=1; _p<=$((10#${_patchlevel})); _p++ )); do
    echo "applying patch bash${_basever//.}-$(printf "%03d" $_p)"
    patch -p0 -i ../bash${_basever//.}-$(printf "%03d" $_p)
  done
}

build() {
  cd $pkgbase-$_basever
  _bashconfig=(-DDEFAULT_PATH_VALUE=\'\"/usr/local/sbin:/usr/local/bin:/usr/bin\"\'
               -DSTANDARD_UTILS_PATH=\'\"/usr/bin\"\'
               -DSYS_BASHRC=\'\"/etc/bash.bashrc\"\'
               -DSYS_BASH_LOGOUT=\'\"/etc/bash.bash_logout\"\'
               -DNON_INTERACTIVE_LOGIN_SHELLS)
  export CFLAGS="${CFLAGS} ${_bashconfig[@]}"

  ./configure \
    --prefix=/usr \
    --with-curses \
    --enable-readline \
    --without-bash-malloc \
    --with-installed-readline
  make
}

check() {
  make -C $pkgname-$_basever check
}

package_bash() {
  pkgdesc='The GNU Bourne Again shell'
  backup=(etc/bash.bash_logout etc/skel/.bash{_profile,_logout})
  depends=('readline'
           'libreadline.so'
           'glibc'
           'ncurses'
           'bashrc')
  optdepends=('bash-completion: for tab completion')
  provides=('sh')

  make -C $pkgname-$_basever DESTDIR="$pkgdir" install
  ln -s bash "$pkgdir/usr/bin/sh"

  # Don't overwrite /usr/share/info/dir
  rm "$pkgdir/usr/share/info/dir"

  # system-wide configuration files
  install -Dm644 system.bash_logout "$pkgdir/etc/bash.bash_logout"

  # user configuration file skeletons
  install -Dm644 dot.bash_profile "$pkgdir/etc/skel/.bash_profile"
  install -m644 dot.bash_logout "$pkgdir/etc/skel/.bash_logout"
}

package_bashrc-manjaro() {
  pkgdesc="Manjaro's default bashrc"
  arch=('any')
  backup=('etc/bash.bashrc' 'etc/skel/.bashrc')
  depends=('bash')
  provides=('bashrc')

  install -Dm644 system.bashrc "$pkgdir/etc/bash.bashrc"
  install -Dm644 dot.bashrc "$pkgdir/etc/skel/.bashrc"
}
