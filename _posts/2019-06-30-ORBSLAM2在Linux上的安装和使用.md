
安装相关依赖
make -j1
修改./.bashrc后一定要source
运行./build_ros.sh出现/usr/lib/x86_64-linux-gnu/libboost_system.so: error adding symbols: DSO missing from command line，按照https://github.com/raulmur/ORB_SLAM2/pull/507 修改CMakeLists.txt即可
