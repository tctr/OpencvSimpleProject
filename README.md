## This is a simple project to show how to create an OpenCV project using cmake

- create a directory for the project 
```
$ mkdir simple_demo && cd simple demo
```
- create a `main.cpp` file with the following code :
```
// main.cpp

#include <iostream>
#include <opencv2/opencv.hpp>
#include <opencv2/highgui.hpp>

using std::cout;
using std::endl;

int main(int argc, char** argv) {

    if (argc != 2) {
        cout << "Expecting a image file to be passed to program" << endl;
        return -1;
    }
    
    cv::Mat img = cv::imread(argv[1]);
    
    if (img.empty()) {
        cout << "Not a valid image file" << endl;
        return -1;
    }
    
    cv::namedWindow("Simple Demo", cv::WINDOW_AUTOSIZE);
    cv::imshow("Simple Demo", img);
    
    cv::waitKey(0);
    cv::destroyAllWindows();

    return 0;
}
```

- in the same directory, create a `CMakeLists.txt` file with the following code :
```
# CMakeLists.txt

# Older versions of CMake are likely to work just fine but, since
# I don't know where to cut off I just use the version I'm using
cmake_minimum_required(VERSION "3.17")

# name of this example project
project(simple-demo)

# set OpenCV_DIR variable equal to the path to the cmake
# files within the previously installed opencv program with
# an environment variable that is set to [PATH_TO_OPENCV_INSTALL]/lib/cmake/opencv4
set(OpenCV_DIR $ENV{OPENCV_MAC})

# Tell compiler to use C++ 17 features which is needed because
# Clang version is often behind in the XCode installation
set(CMAKE_CXX_STANDARD 17)

# configure the necessary common CMake environment variables
# needed to include and link the OpenCV program into this
# demo project, namely OpenCV_INCLUDE_DIRS and OpenCV_LIBS
find_package( OpenCV REQUIRED )

# tell the build to include the headers from OpenCV
include_directories( ${OpenCV_INCLUDE_DIRS} )

# specify the executable target to be built
add_executable(simple-demo main.cpp)

# tell it to link the executable target against OpenCV
target_link_libraries(simple-demo ${OpenCV_LIBS} )
```
- create and cd to a build directory
- launch the following commands to generate the executable : 
```
$ cmake ..`
$ make
```



