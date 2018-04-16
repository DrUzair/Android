[Android Studio Project Config with OpenCV For Android](https://sriraghu.com/2017/03/11/opencv-in-android-an-introduction-part-1/)

1. Create New Android Project
2. Download [Opencv SDK for Android](https://sourceforge.net/projects/opencvlibrary/files/opencv-android/)

2.1 Decompress the downloaded file and note the path. i.e. C:\\OpenCV-android-sdk\

2.2 

## CMakeLists
Make following changes to External Build Files --> CMakeLists

set(pathToProject C:/Dev/OpenCV_Test)
set(pathToOpenCV C:/OpenCV-android-sdk/sdk/native)


add_library( lib_opencv SHARED IMPORTED)
set_target_properties(lib_opencv PROPERTIES IMPORTED_LOCATION ${pathToProject}/app/src/main/jniLibs/${ANDROID_ABI}/libopencv_java3.so)

target_link_libraries( native-lib lib_opencv ${log-lib} )
