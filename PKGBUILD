#Maintainer:Kwrazi<kwrazi@gmail.com>

# 2014-03-19
#  - changed repo from https://github.com/cyrillos/crtools.git to
#    offical repo from https://github.com/xemul/criu.git
# too bad AUR does provide easy way of renaming package using PKGBUILD

_pkgname="crtools"
_newname='criu'

pkgname=${_pkgname}-git
pkgver=20150129
pkgrel=1
pkgdesc="Utility to do checkpoint and restore tasks/processes (aka criu)"
arch=('i686' 'x86_64')
url='http://criu.org/Main_Page'
license=('GPL2')
depends=(protobuf-c)
makedepends=('git' 'xmlto' 'asciidoc')
backup=()
install="${_newname}.install"
provides=(${_pkgname})
conflicts=('criu')
# source=('git+https://github.com/cyrillos/crtools.git')
source=('git+https://github.com/xemul/criu.git')
md5sums=('SKIP')

pkgver() {
    cd ${srcdir}/${_newname}
    git log -1 --format='%cd' --date=short | tr -d -- '-'
}

build() {
    cd ${srcdir}/${_newname}
    unset CFLAGS LDFLAGS
    make all -j $(cat /proc/cpuinfo | grep processor | wc -l)
}

package() {
    cd ${srcdir}/${_newname}
    cp Makefile.inc Makefile.inc.orig
    cat Makefile.inc.orig | sed -e "s|/usr/local|/usr|" | sed -e "s|\$(PREFIX)/etc/logrotate.d/|/etc/logrotate.d/|" > Makefile.inc
    mkdir -p ${pkgdir}/etc/logrotate.d
    make install DESTDIR=${pkgdir}
    ln -s criu ${pkgdir}/usr/sbin/crtools
}
