# Maintainer: Eric Coleman <eric@colemando.com>

pkgname=mod_cloudflare-git
_pkgname=mod_cloudflare
pkgver=20150324
pkgrel=1
pkgdesc="Replaces CloudFlares ip with the actual client ip address."
arch=('i686' 'x86_64')
url='https://github.com/cloudflare/mod_cloudflare'
license=('Apache')
depends=('apache>=2.0.0')
makedepends=('apr>=1.4.0')
install=${_pkgname}.install
md5sums=('13ed7f7934b8bd636b06b525be28bb9f')
source=('mod_cloudflare.conf')

_gitroot=https://github.com/cloudflare/mod_cloudflare.git
_gitname=${_pkgname}

package() {
  _MODDIR='usr/lib/httpd/modules'

  msg "Connecting to GIT server..."
  cd $srcdir
  if [ -d "${_gitname}/.git" ] ; then
      cd $srcdir/${_gitname}
      git pull --rebase
  else
      git clone --depth 1 ${_gitroot}
      test -d ${_gitname} && cd ${_gitname} || return $?
  fi
  msg "GIT checkout done or server timeout"


  # make the module
  cd $srcdir/$_gitname

  /usr/sbin/apxs -c -o $_pkgname.so $_pkgname.c
  install -Dm644 .libs/$_pkgname.so $pkgdir/$_MODDIR/$_pkgname.so
  install -Dm644 $srcdir/mod_cloudflare.conf $pkgdir/etc/httpd/conf/extra/mod_cloudflare.conf
}

