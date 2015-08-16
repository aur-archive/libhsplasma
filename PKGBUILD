# Maintainer: Nicolas Boulanger <nicolas.boulanger_aur at gadz dot org>
pkgname=libhsplasma
_commit=2c1d4014c77f7541683ede61cc085b6a45d6beef
pkgver=20121203
pkgrel=1
pkgdesc="Cross-platform Plasma data and network library"
provides=('libhsplasma')
arch=(any)
url="http://code.google.com/p/libhsplasma/"
license=('GPL')
depends=('zlib' 'libjpeg6' 'openssl' 'python2')

_gitroot="git://github.com/H-uru/libhsplasma.git"
_gitname="libhsplasma"


build() {
    cd "${srcdir}"
    msg "Connecting to GIT server...."

    if [ -d "${_gitname}" ] ; then
        cd "${_gitname}" && git checkout master && git pull origin 
        [[ "${_commit}" ]] && git checkout "${_commit}"
        msg "The local files are updated."
        msg "Running make distclean"
        make distclean || :
    else
        git clone "${_gitroot}" "${_gitname}"
        cd "${_gitname}"
        [[ "${_commit}" ]] && git checkout "${_commit}"
    fi

    cd "${srcdir}/${_gitname}"

    msg "Running cmake"
    cmake -DCMAKE_INSTALL_PREFIX=/usr -DDISABLE_PYTHON=0 .
    msg "Running make"
    make
}

package() {
    msg "Running make install"
    cd "${srcdir}/${_gitname}"
    make DESTDIR=$pkgdir install
}
# vim:set ts=2 sw=2 et:
