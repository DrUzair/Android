[Android Studio Project Config with OpenCV For Android](https://sriraghu.com/2017/03/11/opencv-in-android-an-introduction-part-1/)

1. Create New Android Project
2. Download [Opencv SDK for Android](https://sourceforge.net/projects/opencvlibrary/files/opencv-android/)

2.1 Decompress the downloaded file and note the path. i.e. C:\\OpenCV-android-sdk\

2.2 
## build.gradle (Module:app)
```json
android {
    compileSdkVersion 26
    defaultConfig {
        applicationId "com.company.opencv_project"
        minSdkVersion 21
        targetSdkVersion 26
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
        externalNativeBuild {
            cmake {
                cppFlags "-std=c++11 -frtti -fexceptions" //EDIT
                abiFilters 'x86', 'x86_64', 'armeabi', 'armeabi-v7a', 'arm64-v8a', 'mips', 'mips64' //EDIT
            }
        }
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
    externalNativeBuild {
        cmake {
            path "CMakeLists.txt"
        }
    }
}

dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'com.android.support:appcompat-v7:26.1.0'
    implementation 'com.android.support.constraint:constraint-layout:1.0.2'
    // ADD
    compile project(':openCVLibrary341')     
}
```
## build.gradle (Module:openCVLibrary341)


## CMakeLists
Make following changes to External Build Files --> CMakeLists

- set(pathToProject C:/Dev/OpenCV_Test)
- set(pathToOpenCV C:/OpenCV-android-sdk/sdk/native)

- include_directories(${pathToOpenCV}/jni/include)

- add_library( lib_opencv SHARED IMPORTED)
- set_target_properties(lib_opencv PROPERTIES IMPORTED_LOCATION ${pathToProject}/app/src/main/jniLibs/${ANDROID_ABI}/libopencv_java3.so)

- target_link_libraries( native-lib lib_opencv ${log-lib} )
