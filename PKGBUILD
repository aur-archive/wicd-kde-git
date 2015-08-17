
pkgname=wicd-kde-git
pkgver=20130301
pkgrel=1
pkgdesc="Wicd client build on the KDE Development Platform"
arch=("i686" "x86_64")
url="https://projects.kde.org/projects/extragear/network/wicd-kde/"
license=('GPL')
depends=('kdelibs' 'qt4' 'wicd')
makedepends=('cmake' 'git' 'automoc4')
conflicts=('wicd-kde')
options=(!strip)
source=(download_i18n.sh)
md5sums=('941d2a7e0fd59dafdfdb2bfddf6310d6')

_gitroot="git://anongit.kde.org/wicd-kde"
_gitname="wicd-kde"

build() {
	msg "Connecting to GIT server...."

	
	[ -d $_gitname ] && {
		cd $_gitname
		git pull origin
		cd ..

		msg "Local files have been updated."
	} || {
		git clone $_gitroot
	}

	msg "GIT checkout done or server timeout"

	rm -rf $_gitname-build
	git clone $_gitname $_gitname-build
        cp download_i18n.sh $_gitname-build
	cd $_gitname-build
	echo 'add_subdirectory( i18n )' >> CMakeLists.txt
	msg "Starting make..."
        ./download_i18n.sh
        cmake -DCMAKE_INSTALL_PREFIX=`kde4-config --prefix` \
              -DQT_QMAKE_EXECUTABLE=qmake-qt4 \
              -DPYTHONBIN=python2 \
              -DCMAKE_BUILD_TYPE=debugfull \
              . 
        make

	make DESTDIR=${pkgdir} install || return 1
}


