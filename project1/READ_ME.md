This project displays the environment created in gazebo with a welcome message (written in welcome.cpp file in the script folder) on running
project1/world#gazebo myworld 

The content of welcome.cpp file is as follows 

#include <gazebo/gazebo.hh>

namespace gazebo
{
  class WorldPluginMyRobot : public WorldPlugin
  {
    public: WorldPluginMyRobot() : WorldPlugin()
            {
              printf("WELCOME MESSAGE!");
            }

    public: void Load(physics::WorldPtr _world, sdf::ElementPtr _sdf)
            {
            }
  };
  GZ_REGISTER_WORLD_PLUGIN(WorldPluginMyRobot)
}

Displaying the welcome message requires the following
CMakeLists.txt file and a build directory

CMakeLists.txt file should contain the following

cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

find_package(gazebo REQUIRED)
include_directories(${GAZEBO_INCLUDE_DIRS})
link_directories(${GAZEBO_LIBRARY_DIRS})
list(APPEND CMAKE_CXX_FLAGS "${GAZEBO_CXX_FLAGS}")

add_library(welcome SHARED script/welcome.cpp)
target_link_libraries(hello ${GAZEBO_LIBRARIES})

build directory is created within project1 directory  and compiled as below:
$ mkdir build
$ cd build/
$ cmake ../
$ make # You might get errors if your system is not up to date!
$ export GAZEBO_PLUGIN_PATH=${GAZEBO_PLUGIN_PATH}:"path on your system"/project1/build

The myworld file in the world directory within project1 directory should contain 
<plugin name="welcome" filename="libwelcome.so"/>
under the code: <world name="default">
