# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Bernhard Landauer <bernhard[at]manjaro[dot]org>
# Maintainer: Helmut Stult <helmut[at]manjaro[dot]org>

# Arch credits:
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: Aaron Griffin <aaron@archlinux.org>

pkgbase=bash
pkgname=('bash' 'bashrc-manjaro')
_basever=5.1
_patchlevel=0
pkgver=${_basever}.${_patchlevel}
pkgrel=2
pkgdesc='The GNU Bourne Again shell'
arch=('x86_64')
license=('GPL')
url='https://www.gnu.org/software/bash/bash.html'
source=(https://ftp.gnu.org/gnu/bash/bash-$_basever.tar.gz{,.sig}
    'dot.bashrc'
    'dot.bash_profile'
    'dot.bash_logout'
    'system.bashrc'
    'system.bash_logout')

validpgpkeys=('7C0135FB088AAF6C66C650B9BB5869F064EA74AB') # Chet Ramey

if [[ $((10#${_patchlevel})) -gt 0 ]]; then
  for (( _p=1; _p<=$((10#${_patchlevel})); _p++ )); do
    source=(${source[@]} https://ftp.gnu.org/gnu/bash/bash-$_basever-patches/bash${_basever//.}-$(printf "%03d" $_p){,.sig})
  done
fi

prepare() {
  cd $pkgbase-$_basever

  for (( _p=1; _p<=$((10#${_patchlevel})); _p++ )); do
    msg "applying patch bash${_basever//.}-$(printf "%03d" $_p)"
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

sha256sums=('cc012bc860406dcf42f64431bcd3d2fa7560c02915a601aba9cd597a39329baa'
            'SKIP'
            'ea3fb1f21b1ad236701e59598a57fe3d903ad844c85ae4691ed76aa2f0af49a2'
            'e149407c2bee17779caec70a7edd3d0000d172e7e4347429b80cb4d55bcec9c2'
            '4330edf340394d0dae50afb04ac2a621f106fe67fb634ec81c4bfb98be2a1eb5'
            '5fdc20c44bc9058f728d11111327f4dbb5598fec4d948dd5265211598667f9f0'
            '025bccfb374a3edce0ff8154d990689f30976b78f7a932dc9a6fcef81821811e')
