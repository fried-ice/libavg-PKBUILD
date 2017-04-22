_pkgname=libavg
pkgname=$_pkgname-git
pkgver=20170117
pkgrel=1
pkgdesc='High-level multimedia platform with a focus on interactive art installations.'
arch=('i686' 'x86_64')
url='http://www.libavg.de'
depends=('libtool' 'librsvg' 'libxi' 'gdk-pixbuf2' 'libxml2' 'ffmpeg2.8' 'boost' 'boost-libs' 'python2' 'pango' 'sdl2')
install=$_pkgname.install
backup=('etc/profile.d/libavg.sh')
optdepends=('libvdpau' 'libdc1394' )
makedepends=('python2' 'git' 'cmake')
license=('LGPL')
source=(
	"${_pkgname}::git+https://github.com/libavg/libavg.git#branch=master"
	$_pkgname.sh
	)

sha256sums=(
	"SKIP"
	"fad7e27c496d2e22e0ed81529f80077362640057d3ccb17d18bd8ac6fb98a357"
	)


pkgver() {
	cd ${srcdir}/${_pkgname}
	git log -1 --format="%cd" --date=short | sed "s|-||g"
}

prepare() {
	cd ${srcdir}/${_pkgname}

	# fix python shebang to use python2
	from="#!/usr/bin/env python"
	to="#!/usr/bin/env python2"
	find . -name "*.py" -print | xargs sed -i "s|$from|$to|g"

	mkdir -p build
	cd build

	cmake \
	-D FFMPEG_INCLUDE_DIRS="/usr/include/ffmpeg2.8" \
	-D FFMPEG_LIBRARIES="/usr/lib/ffmpeg2.8" \
	-D CMAKE_INSTALL_PREFIX=/usr \
	-D PYTHON_INTERPRETER=/usr/bin/python2 \
	-D CMAKE_EXE_LINKER_FLAGS="-lpython2.7" \
	 ../

}

build() {

	cd ${srcdir}/${_pkgname}/build

	make ${MAKEFLAGS}
}

package() {
	cd ${srcdir}/${_pkgname}/build
	# make DESTDIR=${pkgdir} install
	mkdir -p ${pkgdir}/usr/lib/python2.7/site-packages/libavg/plugin
	cp -r python/build/lib/libavg ${pkgdir}/usr/lib/python2.7/site-packages
	cp src/test/plugin/colorplugin.so ${pkgdir}/usr/lib/python2.7/site-packages/libavg/plugin
	cd ${pkgdir}/usr/lib/python2.7/site-packages/
	chmod -R 755 libavg/

	install -D -m644 ${srcdir}/${_pkgname}/src/avgrc ${pkgdir}/etc/avgrc

	install -Dm755 "${srcdir}/$_pkgname.sh" ${pkgdir}/etc/profile.d/$_pkgname.sh
}
