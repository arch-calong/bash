# Maintainer: Bernhard Landauer <oberon@manjaro.org>
# Maintainer:  Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: Aaron Griffin <aaron@archlinux.org>

pkgbase=bash
pkgname=('bash' 'bashrc-manjaro')
_basever=5.0
_patchlevel=009
pkgver=${_basever}.${_patchlevel}
pkgrel=1
arch=('i686' 'x86_64')
license=('GPL')
url='http://www.gnu.org/software/bash/bash.html'
groups=('base')
source=(https://ftp.gnu.org/gnu/bash/bash-$_basever.tar.gz{,.sig}
    'dot.bashrc'
    'dot.bash_profile'
    'dot.bash_logout'
    'system.bashrc'
    'system.bash_logout')
md5sums=('2b44b47b905be16f45709648f671820b'
         'SKIP'
         'f6d012f6bed87567b0df448a5a3a78f2'
         '2902e0fee7a9168f3a4fd2ccd60ff047'
         '42f4400ed2314bd7519c020d0187edc5'
         'd8f3f334e72c0e30032eae1a1229aef1'
         '472f536d7c9e8250dc4568ec4cfaf294'
         'b026862ab596a5883bb4f0d1077a3819'
         'SKIP'
         '2f4a7787365790ae57f36b311701ea7e'
         'SKIP'
         'af7f2dd93fd5429fb5e9a642ff74f87d'
         'SKIP'
         'b60545b273bfa4e00a760f2c648bed9c'
         'SKIP'
         '875a0bedf48b74e453e3997c84b5d8a4'
         'SKIP'
         '4a8ee95adb72c3aba03d9e8c9f96ece6'
         'SKIP'
         '411560d81fde2dc5b17b83c3f3b58c6f'
         'SKIP'
         'dd7cf7a784d1838822cad8d419315991'
         'SKIP'
         'c1b3e937cd6dccbb7fd772f32812a0da'
         'SKIP')
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

    ./configure --prefix=/usr --with-curses --enable-readline \
    --without-bash-malloc --with-installed-readline
    make
}

check() {
    make -C $pkgname-$_basever check
}

package_bash() {
    pkgdesc='The GNU Bourne Again shell'
    backup=(etc/bash.bash_logout etc/skel/.bash{_profile,_logout})
    depends=('bashrc'
        'glibc'
        'ncurses'
        'readline>=7.0')
    optdepends=('bash-completion: for tab completion')
    provides=('sh')
    make -C $pkgname-$_basever DESTDIR="$pkgdir" install
    ln -s bash "$pkgdir"/usr/bin/sh

    # system-wide configuration files
    install -Dm644 system.bash_logout "$pkgdir"/etc/bash.bash_logout

    # user configuration file skeletons
    install -Dm644 dot.bash_profile "$pkgdir"/etc/skel/.bash_profile
    install -m644 dot.bash_logout "$pkgdir"/etc/skel/.bash_logout
}

package_bashrc-manjaro() {
    pkgdesc="Manjaro's default bashrc"
    arch=('any')
    backup=('etc/bash.bashrc' 'etc/skel/.bashrc')
    depends=('bash')
    provides=('bashrc')
    install -Dm644 system.bashrc "$pkgdir"/etc/bash.bashrc
    install -Dm644 dot.bashrc "$pkgdir"/etc/skel/.bashrc
}
