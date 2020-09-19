# Maintainer: Timon Engelke <aur@timonengelke.de>
pkgdesc="ROS - The robot_localization package provides nonlinear state estimation through sensor fusion of an abritrary number of sensors."
url='https://wiki.ros.org/robot_localization'

pkgname='ros-melodic-robot-localization'
pkgver='2.6.7'
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
pkgrel=1
license=('BSD')

ros_makedepends=(ros-melodic-tf2-ros
  ros-melodic-geographic-msgs
  ros-melodic-diagnostic-updater
  ros-melodic-roscpp
  ros-melodic-geometry-msgs
  ros-melodic-std-msgs
  ros-melodic-diagnostic-msgs
  ros-melodic-message-filters
  ros-melodic-message-generation
  ros-melodic-nodelet
  ros-melodic-sensor-msgs
  ros-melodic-cmake-modules
  ros-melodic-catkin
  ros-melodic-tf2-geometry-msgs
  ros-melodic-nav-msgs
  ros-melodic-tf2
  ros-melodic-roslint
  ros-melodic-eigen-conversions)
makedepends=('ros-build-tools'
  ${ros_makedepends[@]}
  eigen
  cmake
  yaml-cpp)

ros_depends=(ros-melodic-tf2-ros
  ros-melodic-geographic-msgs
  ros-melodic-diagnostic-updater
  ros-melodic-roscpp
  ros-melodic-geometry-msgs
  ros-melodic-std-msgs
  ros-melodic-message-runtime
  ros-melodic-nodelet
  ros-melodic-diagnostic-msgs
  ros-melodic-message-filters
  ros-melodic-sensor-msgs
  ros-melodic-cmake-modules
  ros-melodic-tf2-geometry-msgs
  ros-melodic-nav-msgs
  ros-melodic-tf2
  ros-melodic-eigen-conversions)
depends=(${ros_depends[@]}
  eigen
  yaml-cpp)

_dir="robot_localization-${pkgver}"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/cra-ros-pkg/robot_localization/archive/${pkgver}.tar.gz")
sha256sums=('696487ac10c3d42f257bec7739010d1924ccea52da102b609e616f7d587a14d5')

build() {
  # Use ROS environment variables
  source /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/melodic/setup.bash ] && source /opt/ros/melodic/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Fix Python2/Python3 conflicts
  /usr/share/ros-build-tools/fix-python-scripts.sh -v 3 ${srcdir}/${_dir}

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/melodic \
        -DPYTHON_EXECUTABLE=/usr/bin/python3 \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
