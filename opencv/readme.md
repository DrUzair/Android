# Android Studio Project Config with OpenCV For Android

1. Create New Android Project (Include C++ Suppoprt) 
   
   Choose appropriate C++ standard i.e. C++ 11, C++ 14
   
   If behind proxy: 
   1. update gradle.properties (Project properties)
   ..* systemProp.http.proxyUser
   ..* systemProp.https.proxyUser
   ..* systemProp.http.proxyPassword
   ..* systemProp.https.proxyPassword
   ..* systemProp.http.proxyPort
   ..* systemProp.https.proxyPort=8080
   2. update builg.gradle (Module:app)
   disable/comment 
    ```gradle
        //testImplementation 'junit:junit:4.12'
        //androidTestImplementation 'com.android.support.test:runner:1.0.1'
        //androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.1'
    ```
2. Download [Opencv SDK for Android](https://sourceforge.net/projects/opencvlibrary/files/opencv-android/)

- Decompress the downloaded file and note the path. i.e. C:\\OpenCV-android-sdk\

## Import openCV Module
Android Studio: File-->New-->Import Module-->Browse to C:\\OpenCV-android-sdk\sdk\java-->Ok-->Finish

## build.gradle (Module:app)
- Important Elements: 
-- sourceSets
-- defaultConfig --> externalNativeBuild
-- dependencies --> compile project(':openCVLibrary341')  
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
    sourceSets {
            main {
                jniLibs.srcDirs = ['C:/Dev/OpenCV_Test/app/src/main/jniLibs']
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
    compile project(':openCVLibrary341')     
}
```
## build.gradle (Module:openCVLibrary341)
```json
apply plugin: 'com.android.library'

android {
    compileSdkVersion 26
    buildToolsVersion "26.0.2"

    defaultConfig {
        minSdkVersion 21
        targetSdkVersion 26
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.txt'
        }
    }
}
```
Make sure that compileSdkVersion, minSdkVersion and targetSdkVersion have same values in both build.gradle files.
## CMakeLists
Make following changes to External Build Files --> CMakeLists

- set(pathToProject C:/Dev/OpenCV_Test)
- set(pathToOpenCV C:/OpenCV-android-sdk/sdk/native)

- include_directories(${pathToOpenCV}/jni/include)

- add_library( lib_opencv SHARED IMPORTED)
- set_target_properties(lib_opencv PROPERTIES IMPORTED_LOCATION ${pathToProject}/app/src/main/jniLibs/${ANDROID_ABI}/libopencv_java3.so)

- target_link_libraries( native-lib lib_opencv ${log-lib} )
