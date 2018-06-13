# Maintainer: Bernhard Landauer <oberon@manjaro.org>
# Maintainer:  Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: Aaron Griffin <aaron@archlinux.org>

pkgbase=bash
pkgname=('bash' 'bashrc-manjaro')
_basever=4.4
_patchlevel=023
pkgver=${_basever}.${_patchlevel}
pkgrel=1
license=('GPL')
url='http://www.gnu.org/software/bash/bash.html'
groups=('base')
source=(https://ftp.gnu.org/gnu/bash/bash-$_basever.tar.gz{,.sig}
    'dot.bashrc'
    'dot.bash_profile'
    'dot.bash_logout'
    'system.bashrc'
    'system.bash_logout')
md5sums=('148888a7c95ac23705559b6f477dfe25'
    'SKIP'
    '7330b61cf37870d609c5fdfd3fa8f60a'
    '2902e0fee7a9168f3a4fd2ccd60ff047'
    '42f4400ed2314bd7519c020d0187edc5'
    'd8f3f334e72c0e30032eae1a1229aef1'
    '472f536d7c9e8250dc4568ec4cfaf294'
    '817d01a6c0af6f79308a8b7b649e53d8'
    'SKIP'
    '765e14cff12c7284009772e8e24f2fe0'
    'SKIP'
    '49e7da93bf07f510a2eb6bb43ac3e5a2'
    'SKIP'
    '4557d674ab5831a5fa98052ab19edaf4'
    'SKIP'
    'cce96dd77cdd1d293beec10848f6cbb5'
    'SKIP'
    'd3379f8d8abce5c6ee338f931ad008d5'
    'SKIP'
    'ec38c76ca439ca7f9c178e9baede84fc'
    'SKIP'
    'e0ba18c1e3b94f905da9b5bf9d38b58b'
    'SKIP'
    'e952d4f44e612048930c559d90eb99bb'
    'SKIP'
    '57b5b35955d68f9a09dbef6b86d2c782'
    'SKIP'
    'cc896e1fa696b93ded568e557e2392d5'
    'SKIP'
    'fa47fbfa56fb7e9e5367f19a9df5fc9e'
    'SKIP'
    '5e6a20166efe166267972cc78025417b'
    'SKIP'
    '00a8877a8787dbd78d97767db1115b0a'
    'SKIP'
    '2409586fd19e3104197ead86ce549eca'
    'SKIP'
    '4b31183db086daf8be8943d7f7ea7526'
    'SKIP'
    'c15c8844f1eb87bdbcde71417c9bd342'
    'SKIP'
    'b25e3373fc8de00523116dfe151ac4e0'
    'SKIP'
    '8f43e1d277b02f3319a34c1cd4a4ff3e'
    'SKIP'
    '5217ff08c444446ec306dce60437c288'
    'SKIP'
    '282c7d9b38da8005d25b4f816328a2f4'
    'SKIP'
    '0b709c9d7f8e6cf267a8b863efb899f7'
    'SKIP'
    'fe2e0ca4cf9409ff0e9428e1236f983e'
    'SKIP')
validpgpkeys=('7C0135FB088AAF6C66C650B9BB5869F064EA74AB') # Chet Ramey

if [[ $((10#${_patchlevel})) -gt 0 ]]; then
    for (( _p=1; _p<=$((10#${_patchlevel})); _p++ )); do
    source=(${source[@]} https://ftp.gnu.org/gnu/bash/bash-$_basever-patches/bash${_basever//.}-$(printf "%03d" $_p){,.sig})
    done
fi

prepare() {
    cd $pkgname-$_basever

    for (( _p=1; _p<=$((10#${_patchlevel})); _p++ )); do
    msg "applying patch bash${_basever//.}-$(printf "%03d" $_p)"
    patch -p0 -i ../bash${_basever//.}-$(printf "%03d" $_p)
    done
}

build() {
    cd $pkgname-$_basever

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
    arch=('i686' 'x86_64')
    backup=(etc/bash.bash_logout} etc/skel/.bash{_profile,_logout})
    depends=('glibc'
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

package_bashrc-manjaro(){
    pkgdesc='Manjaro's default bashrc'
    arch=('any')
    backup=(etc/bash.bash{rc,_logout} etc/skel/.bash{rc,_profile,_logout})
    depends=('bash')
    provides=('bashrc')

    install -Dm644 system.bashrc $pkgdir/etc/bash.bashrc
    install -Dm644 dot.bashrc "$pkgdir"/etc/skel/.bashrc
}
