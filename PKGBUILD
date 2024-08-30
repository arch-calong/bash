# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Bernhard Landauer <bernhard[at]manjaro[dot]org>
# Maintainer: Mark Wagie <mark at manjaro dot org>
# Contributor: Helmut Stult
# Contributor: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Tobias Powalowski <tpowa@archlinux.org>
# Contributor: Giancarlo Razzolini <grazzolini@archlinux.org>
# Contributor:  Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: Aaron Griffin <aaron@archlinux.org>

pkgname=bash
_basever=5.2
_patchlevel=032
pkgver=${_basever}.${_patchlevel}
pkgrel=2
pkgdesc='The GNU Bourne Again shell'
arch=(x86_64)
license=('GPL-3.0-or-later')
url='https://www.gnu.org/software/bash/bash.html'
backup=(
  etc/bash.bash{rc,_logout}
  etc/skel/.bash{rc,_profile,_logout}
)
depends=(
  readline
  libreadline.so
  glibc
  ncurses
)
optdepends=('bash-completion: for tab completion')
provides=('sh')
conflicts=('bashrc-manjaro')
replaces=('bashrc-manjaro')
install=bash.install
source=(
  https://ftp.gnu.org/gnu/bash/bash-$_basever.tar.gz{,.sig}
  bash-5.2_p15-configure-clang16.patch
  bash-5.2_p15-random-ub.patch
  bash-5.2_p21-configure-strtold.patch
  bash-5.2_p21-wpointer-to-int.patch
  bash-5.2_p32-memory-leaks.patch
  bash-5.2_p32-read-delimiter-in-invalid-mbchar.patch
  dot.bashrc
  dot.bash_profile
  dot.bash_logout
  system.bashrc
  system.bash_logout
)
validpgpkeys=('7C0135FB088AAF6C66C650B9BB5869F064EA74AB') # Chet Ramey

if [[ $((10#${_patchlevel})) -gt 0 ]]; then
  for (( _p=1; _p<=$((10#${_patchlevel})); _p++ )); do
    source=(${source[@]} https://ftp.gnu.org/gnu/bash/bash-$_basever-patches/bash${_basever//.}-$(printf "%03d" $_p){,.sig})
  done
fi
b2sums=('51b196e710794ebad8eac28c31c93eb99ac1a7db30919a13271e39e1cb66a0672f242df75fc7d71627ea873dfbce53ec35c0c56a71c5167143070a7811343fd9'
        'SKIP'
        '5ef332cd2847f46e351e5db6dda79d01d9853f5eda9762deeba0450c2bd400eec549bbb85696777b687f64d0977daac4883d6ce3f1e26cec0d5f73e8ee97f000'
        'adab09c3f2ce3697e3659e01266120155714b80263bd125808edf556a354291af615540189553b1c32a2d462ac41e28a9df8fb9f7d963a3ca3629d297a46e62d'
        '83ec6ff756543ee44c18902f2d30dd662a84237b9594a7e0cfc21a1c16fce49e37cf67729b3a17d59cc978cb6675e04457e3b6b0909d94cb234a1dde96f7c9ea'
        '0c7f5eb5b697abf15c1d17888a973e44d0ead1f095778b41841a6a1937a5b9e7ce5fa6a05e4404504990b0a244fdecfc12ce7c33ee7d67b4c837435e9bfe2b57'
        '373aa3be1f0a6bc65403cde63cbc4dcd612336e86b1cae918670a99e8ca639c665ac7efb467ec8823a62cec0a71c485bd3fda4bbf058d759498377f5cfe90f51'
        'ab7fe139630be59b26a72f92f22e4a2b556594d341d82b0f15f99880724f5ea5cfd912a8de6b6e1db902c14d65395c74a03379e3e01ce69bb4512c681518301d'
        '56eda53e32de12cdcb0a9bed50e11764e094009999a242550599c45ae0f372d37dffc23bfc0ed45587f689c51fb03bf364605824e61ef87d0b52283626f8bc21'
        '2d53f99e485218ed47f2e40907023645594ac8ffcf00d0569050d54a8f4dabe0a2bdcab515a45b663283c2e6299d805b923ea7b7b789c6a4150c37a98a5b117c'
        'dbfe5c1aaea94419305c1f8c9b54b94eab515260910f2309360ff702a27032faa34514e70b31adbb1e41bd912d4e43a610939cb07565f43e05dd19813a81752e'
        'cc50ba471d74fbff5fc8c884d8c83ba40d302669d31a89f8684c1294f4663610f8f60dfc9a97efc12d592da84c36db034ef2ac6bb7bd68b959c6860cffb2b2db'
        'fc924345d5dab10f1ae328bca3cf1053ddff557e074a6e6dff771bd813b93838980ed5d0f20d3a0584cbd1994332fcacc8a6b0e98f7aa376139198ea6a4d6f5a'
        'd00a8b4fb3babf52c67a3e345158c1f70b5b45e5a54100a6671d96f9cfbf893143d5a23df7e7c5f4d5c0bd650519fb0c447b2304db2d6e0751dfffa651a7cf49'
        'SKIP'
        'b3b7e2511823a0527aeed5af2c8d9f44e5ab079fa8b3f48fe84b35a14327d0143e14e04316c16bfbe2a1cac0c7fcf7ab5058a2b00be38ed3243b53b786e969f1'
        'SKIP'
        'd9f358c240d998a331d6aa4513b02191b1fbe7e875f8e96e531fca8968f84d0f4672d3644bbd6258f2aca0cabd2deb6159bbf98ba201e667d61353113a3e8240'
        'SKIP'
        '159fbb7a6dddece1d4db2b38d6de591366ae07eb237ffa8ad61c933560160561736a4e70b8bd5441cd75ae88e8d4a29869367838b169a4533d06d9d3c345d554'
        'SKIP'
        '5afdbe8fa644e1b7108600a7ecc0a8e5774a837f3acff45bfe5eff9ffca1b9e5ab09f19083464a9cfaee4bd6c9b351275c5baef5331c43dbfbc642e226ca8af3'
        'SKIP'
        '68c37f5f5164685d0d1f25a05d5584128b6d8d83efa271aaaf80c82e2ec71bc78a3961ebd5d5d6620ef6a3dcca7e6494f0e666b651056faef9c0ea0866b3b94e'
        'SKIP'
        '028808fa9eac85e66ad942fff07ca6595b578911b3f3f99ae7d67289bd6c27936bbce66fea160e8c3e2fcc6bb18f6429121685c550a815ed992f9d0c757391ae'
        'SKIP'
        'b46dde58525b727565efeca99cf4279fd2510382430b227ed233e7fc78c433b8d7eb2f1f7e4d31174118e9cc5bb8c43656e78583dc7fde15381aa63001b78277'
        'SKIP'
        '36a1a5be9166f436077aff8c8dc8e6b8745b6b07408e5abc3756846d199799cee22e825ae992f3db5f3885157fb37b64f1159b3bc8d0bd1d16c5980c9f74e092'
        'SKIP'
        '0c61991d38c95b25411e793a09855c18f536ddfae237b09d01ac7898d4638b8747fc58d2c2f35c651026bd6957cb04780382256417e0bbde288aa4e05cd80530'
        'SKIP'
        'e1b246634ee7b1bba7e4b140bc730fa6770f5988ed215ea1ba646eea630789b863333fec471e99c28b142b74539639f37239487b02b877ea360f519bdaee2894'
        'SKIP'
        'b7c4888a3af4e9ee37f3d83d15bad1360209eb412ba1e963c4be90b0b1d62e0c860f61f5cf7de3b7b1a34d341101069ffa5a65efc7dc5857dac296444321b9d2'
        'SKIP'
        'a8c5a2d526a049b36677a485d8e12a6ccbabc6118ba760e2e08785650b89ae13b155242c7c5f557fb229ffcdea6ff6d5b0de1d0c66b7f2a1711bee7d01a4b663'
        'SKIP'
        '990e6566c446ce030d1333a05de9027a994054e983bf414e9aa09505c94d0615f1726494e139320b0d1c923c680565b2cf4249bd062e9e8aa98b226386c03c26'
        'SKIP'
        '038f03bc543297a3f2e7612afdee7b27eb5d65d7f81c22976936211f4a80acd9f0faf1ba6c56e20fc653b877a448ab7872b5488da3684952682d80c752227ab2'
        'SKIP'
        '675b70e1df1083021fb6336e50d10012dc02e1a80865a64579256319ca98c8282af20e7210ef9d993f97718c7bfed2315f23edac04e6f3af65a1e08cd5f7ef2e'
        'SKIP'
        '461f2f6543501306faa5decd98211699f0ce84eea5a1225145dc401ec0ca893c9d8021359c04af4dec265e7d247f2fbb70cfe8d5382e3c38fd2774e017de4aed'
        'SKIP'
        '89f95c096f8e487e2a1a00541087d157321b125ae93dc656af0cf6ead9158401a028f5c838c4b81aeb95e7c4951a3b4dfb1a88e08297a03236c0ad36eb6710d2'
        'SKIP'
        'bcf683825da1e56692d7024748501cc582e623168fc1a8713ef3b4eb284222f6bf9144871d6357464a1c8c031f105ca6cac6cc591b5463d8b72eb139fcf044f0'
        'SKIP'
        'de3e38dbb2395c765767aed516ae3d143e3187a44964f90c587f41f93447c43515481e3c9bd562175d750d0dfb9e4e3eacb25c31f8bf54168fa544c938955eae'
        'SKIP'
        'cc2d886da8c51eb7bdbed694423eae29dc05dc2c7bd0cd41b9ee3acbc56ef135043bb48275c4162d33d2d4051a0a8b27f3aec097335b9d15e38fd841a6793f71'
        'SKIP'
        '2e0cc2255c0313ab85547363d7dd060d460db44131b698235275413c51e79cdc33b77064f84d56e75a0951fc62f947482c2f317a0d4f732822a4ffaed943a9cd'
        'SKIP'
        '9727ad8cf219ba906021f833cacbbccf6c5b9c94decf861a5f40627680ac3d19d65eaeafecd575545dc7eb538f27b0ecc55a7462b49d226751ad14fb2f40e825'
        'SKIP'
        'f9113fcb1b8ee8d96744e45f020fd8ec49546d6a29883544f4d4a4ef1087b764de6e7c37c760ac709370cdace9619aec84f03713be5e6bc9a9e90d97dd35caa0'
        'SKIP'
        '5d18e00cc44710f078037f25c61741a078bb0fc906d6d5555e581e093d9e99be71f7f06fc0d139f4f25d40f5f854378031aff6e63d26ead55fe6cca626df50bd'
        'SKIP'
        'ebe3bc47dadf5d689258c5ccf9883838d3383dc43bec68d2a6767b6348cf1515a98ec9e445c3110e8eb0d87e742c20a0d4ddb70649ec94217f55aad7d18552af'
        'SKIP'
        'b76ce03456e064f17db00e9026aa53656a063c195faa02c7d51da8d173f7525fe5411bf526f19ee9e717ee1ec957de7e73f5af851a68d5cb554f2c4492ab3844'
        'SKIP'
        '58fdeecf6dd685103c7dc0e7c200cae65206e5fb3360d798b9cec05fc935ebae139bdf142f6018c9837d1780eb7c5cecff0a945369c14fa575e6801c46a15a31'
        'SKIP'
        '01ddb0acc5b6067e729320692284d61735ace62eeede81a74b7628fe6899da61d921a11bd0d22d0e6f2e241e7b0cb64591654a34a33916739e35e23d5cc6f5bd'
        'SKIP'
        'd0cf114642393eb2e2d060eac339674c8ce10af4d54bbcee0f450854d27373ede9dd159caf6d05fc69429ad357d666b47f6781ef590287f33a535b2c26d8754d'
        'SKIP'
        'dac378115906e21fc754267c42e129e2374c9b63f879d1717d79930589618d4d8d17821b2f529d1851db7567d3efdfb0410c18e6869047e3d87443b29d507289'
        'SKIP'
        '55aab849da0fcc69ab3516d9d7ff2858b5f15cbeaddf66282f43f272b52d646c2c41c2ceef632a2ae8f13c25d92e85f49fbc6de989ed4f6ac4bb7bea7fc59a5d'
        'SKIP')

prepare() {
  cd "${pkgname}-${_basever}"
  for (( _p=1; _p<=$((10#${_patchlevel})); _p++ )); do
    local patch="bash${_basever//.}-$(printf "%03d" $_p)"
    patch -Np0 -i ../"${patch}"
  done
  # add patches from gentoo, fixing various upstream reported issues
  # https://gitweb.gentoo.org/repo/gentoo.git/tree/app-shells/bash/files
  patch -Np0 -i ../bash-5.2_p15-configure-clang16.patch
  patch -Np0 -i ../bash-5.2_p15-random-ub.patch
  patch -Np0 -i ../bash-5.2_p21-configure-strtold.patch
  patch -Np0 -i ../bash-5.2_p21-wpointer-to-int.patch
  patch -Np0 -i ../bash-5.2_p32-memory-leaks.patch
  patch -Np0 -i ../bash-5.2_p32-read-delimiter-in-invalid-mbchar.patch
}

build() {
  cd "${pkgname}-${_basever}"

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
  make -C "${pkgname}-${_basever}" check
}

package() {
  make -C "${pkgname}-${_basever}" DESTDIR="$pkgdir" install
  ln -s bash "${pkgdir}/usr/bin/sh"
  ln -s bash "${pkgdir}/usr/bin/rbash"

  # system-wide configuration files
  install -Dm644 system.bashrc "${pkgdir}/etc/bash.bashrc"
  install -Dm644 system.bash_logout "${pkgdir}/etc/bash.bash_logout"

  # user configuration file skeletons
  install -dm755 "${pkgdir}/etc/skel/"
  install -m644 dot.bashrc "${pkgdir}/etc/skel/.bashrc"
  install -m644 dot.bash_profile "${pkgdir}/etc/skel/.bash_profile"
  install -m644 dot.bash_logout "${pkgdir}/etc/skel/.bash_logout"
}


