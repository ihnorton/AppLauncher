FROM thewtex/opengl:v0.1.0
MAINTAINER CommonTK Community <ctk-developers@commontk.org>
# Test the CTK App Launcher
# Graphic rendering support is required, so we use a base image that support
# rendering.

# Build the same version of CMake that is in thewtex/centos-build
WORKDIR /usr/src
RUN git clone git://cmake.org/cmake.git CMake && \
  cd CMake && \
  git checkout v3.4.1 && \
  mkdir /usr/src/CMake-build && \
  cd /usr/src/CMake-build && \
  /usr/src/CMake/bootstrap \
    --parallel=$(grep -c processor /proc/cpuinfo) \
    --prefix=/usr && \
  make -j$(grep -c processor /proc/cpuinfo) && \
  ./bin/cmake \
    -DCMAKE_BUILD_TYPE:STRING=Release \
    -DCMAKE_USE_OPENSSL:BOOL=ON . && \
  make install && \
  cd .. && rm -rf CMake*

ENV APP "sudo chown -R user.user /usr/src/AppLauncher-build && cd /usr/src/AppLauncher-build && ctest -V"
