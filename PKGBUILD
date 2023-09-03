# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Bernhard Landauer <bernhard[at]manjaro[dot]org>
# Contributor: Helmut Stult

# Arch credits:
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: Aaron Griffin <aaron@archlinux.org>

pkgbase=bash
pkgname=('bash' 'bashrc-manjaro')
_basever=5.1
_patchlevel=016
pkgver=${_basever}.${_patchlevel}
pkgrel=3
pkgdesc='The GNU Bourne Again shell'
arch=('x86_64')
license=('GPL')
url='https://www.gnu.org/software/bash/bash.html'
depends=('bash-completion')
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
  install=bash.install

  make -C $pkgname-$_basever DESTDIR="$pkgdir" install
  ln -s bash "$pkgdir/usr/bin/sh"
  ln -s bash "$pkgdir/usr/bin/rbash"

  # system-wide configuration files
  install -Dm644 system.bash_logout "$pkgdir/etc/bash.bash_logout"

  # user configuration file skeletons
  install -dm755 "$pkgdir/etc/skel/"
  install -m644 dot.bash_profile "$pkgdir/etc/skel/.bash_profile"
  install -m644 dot.bash_logout "$pkgdir/etc/skel/.bash_logout"

  # Don't overwrite /usr/share/info/dir
  rm "$pkgdir/usr/share/info/dir"
}

package_bashrc-manjaro() {
  pkgdesc="Manjaro's default bashrc"
  arch=('any')
  depends=('bash')
  provides=('bashrc')
  backup=('etc/bash.bashrc' 'etc/skel/.bashrc')

  install -Dm644 system.bashrc "$pkgdir/etc/bash.bashrc"
  install -Dm644 dot.bashrc "$pkgdir/etc/skel/.bashrc"
}

sha256sums=('cc012bc860406dcf42f64431bcd3d2fa7560c02915a601aba9cd597a39329baa'
            'SKIP'
            'dc8186a0808a4fc2ffeabafee16cf1ffc946a77426147866b7b35502deafe75e'
            'e149407c2bee17779caec70a7edd3d0000d172e7e4347429b80cb4d55bcec9c2'
            '4330edf340394d0dae50afb04ac2a621f106fe67fb634ec81c4bfb98be2a1eb5'
            '1a3bbc54faaa620d4c0aa3ca6e4202c827fe4b31122f395df6aeeaab3c276883'
            '025bccfb374a3edce0ff8154d990689f30976b78f7a932dc9a6fcef81821811e'
            'ebb07b3dbadd98598f078125d0ae0d699295978a5cdaef6282fe19adef45b5fa'
            'SKIP'
            '15ea6121a801e48e658ceee712ea9b88d4ded022046a6147550790caf04f5dbe'
            'SKIP'
            '22f2cc262f056b22966281babf4b0a2f84cb7dd2223422e5dcd013c3dcbab6b1'
            'SKIP'
            '9aaeb65664ef0d28c0067e47ba5652b518298b3b92d33327d84b98b28d873c86'
            'SKIP'
            'cccbb5e9e6763915d232d29c713007a62b06e65126e3dd2d1128a0dc5ef46da5'
            'SKIP'
            '75e17d937de862615c6375def40a7574462210dce88cf741f660e2cc29473d14'
            'SKIP'
            'acfcb8c7e9f73457c0fb12324afb613785e0c9cef3315c9bbab4be702f40393a'
            'SKIP'
            'f22cf3c51a28f084a25aef28950e8777489072628f972b12643b4534a17ed2d1'
            'SKIP'
            'e45cda953ab4b4b4bde6dc34d0d8ca40d1cc502046eb28070c9ebcd47e33c3ee'
            'SKIP'
            'a2c8d7b2704eeceff7b1503b7ad9500ea1cb6e9393faebdb3acd2afdd7aeae2a'
            'SKIP'
            '58191f164934200746f48459a05bca34d1aec1180b08ca2deeee3bb29622027b'
            'SKIP'
            '10f189c8367c4a15c7392e7bf70d0ff6953f78c9b312ed7622303a779273ab98'
            'SKIP'
            'c7acb66df435d284304c16ca83a5265f9edd9368612095b01a733d45c77ed5ad'
            'SKIP'
            '6a4ee0c81b437b96279a792c1efcec4ba56f009195a318083db6b53b096f83d0'
            'SKIP'
            '1b37692ef1f6cc3dcec246773443276066e6b1379868f8c14e01f4dfd4df80f0'
            'SKIP'
            '8899144f76a5db1fb41a89ed881c9f19add95728dd71db324f772ef225c5384f'
            'SKIP')
