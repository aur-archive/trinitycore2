# Maintainer: inteliboy <inteliboy@gmail.com>

pkgname=trinitycore2
pkgver=20120529
pkgrel=1
pkgdesc="Trinity Core MMo Server Framework"
arch=('i686' 'x86_64')
url="http://www.trinitycore.org"
license=('GPL')
depends=('mysql' 'libmysqlclient' 'mysql-clients' 'zlib' 'openssl')
makedepends=('git' 'cmake' 'ace>=6.0.0' 'libtool' 'patch' 'gcc' 'make' 'autoconf' 'automake' 'bin86' 'bison' 'ed' 'fakeroot' 'flex' 'm4' 'pkgconfig')
options=('!libtool')
source=('GMutex.patch')
md5sums=('dce01e94214395c540fdab84b56c7ba5')

_gitroot=git://github.com/TrinityCore
_gitname=TrinityCore

build() 
{
	cd "$srcdir"
	msg "Conecting to GIT server..."

	if [ -d $_gitname ] ; then
		cd "$_gitname" $$ git pull origin || return 1
		msg "The local files are updated."
	else
		msg "No previous sources found. Cloning from GIT now."
		git clone "$_gitroot/$_gitname" "$_gitname" || return 1
	fi
	msg "GIT checkout done or server timeout."
	msg "Starting to build."

# some cleanup
	rm -rf "$srcdir/build" || return 1

# prepare build dir
  	mkdir "$srcdir/build" || return 1
	git clone -l "$srcdir/$_gitname" "$srcdir/build" || return 1
  	cd "$srcdir/build"	|| return 1

        msg "Applying compilation fixes..."
# for more info follow the link below.
# http://www.trinitycore.org/f/topic/6211-usleep-not-found/
	patch -Np1 -i "${srcdir}/GMutex.patch"	|| return 1

# configure
  	cmake -DPREFIX="$pkgdir/usr" -DCONF_DIR="$pkgdir/usr/etc" || return 1

# build
  	make || return 1
  	make install || return 1
} 