#Maintainer: Benjamin Chretien <chretien at lirmm dot fr>
pkgdesc="ROS - PR2 specific tutorials for MoveIt!"
url='http://www.ros.org/'

pkgname=ros-groovy-pr2-moveit-tutorials
pkgver=0.4.3
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools' 'cmake')
depends=('ros-groovy-interactive-markers'
         'ros-groovy-pluginlib'
         'ros-groovy-moveit-core'
         'ros-groovy-moveit-ros-planning-interface'
         'ros-groovy-moveit-ros-perception')
_dir=moveit_pr2
_subdir=pr2_moveit_tutorials
source=("$_dir"::'git://github.com/ros-planning/moveit_pr2.git'#branch=groovy-devel)
md5sums=('SKIP')


build() {
    [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
    [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
    cd ${srcdir}/build
    /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/${_dir}/${_subdir}
    cmake ${srcdir}/${_dir}/${_subdir} \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy \
        -DPYTHON_EXECUTABLE=/usr/bin/python2 \
        -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 \
        -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
    make
}

package() {
    cd "${srcdir}/build"
    make DESTDIR="${pkgdir}/" install
}
