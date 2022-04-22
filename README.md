# ros_debug

1.CMakeLists配置：
catkin_make -DCMAKE_BUILD_TYPE=Debug 或者 
SET(CMAKE_BUILD_TYPE "Debug")
SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")
2. 
launch形式：
launch文件，在Node标签中添加
launch-prefix="xterm -e gdb -ex run --args "
命令形式：
rosrun --prefix 'gdb -ex run --args' [package_name] [node_name] 
可执行文件路径
you_catkin_workspace/devel/lib/your_package_name
gdb node_name



内存泄漏Valgrind
安装valgrind
tar jxvf valgrind-3.14.0.tar.bz2
cd valgrind-3.14.0/
./autogen.sh
./configure --prefix=/home/pony/valgrind
make
make install
sudo gedit ~/.bashrc
    export PATH=$PATH:~/valgrind/bin/
source ~/.bashrc

node配置
<node name ="node_name" pkg ="pkg_name" type="node_name" output="screen" launch-prefix="valgrind --log-file=node_name_report.log --tool=memcheck --leak-check=full --show-leak-kinds=all"/>
