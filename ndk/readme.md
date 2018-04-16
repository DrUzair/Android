# [Getting Started with Native Development Kit](https://developer.android.com/ndk/guides/index.html)

# Issues
1. Unable to resolve dependency for 'app@debugAndroidTest/compileClasspath': could not download junit.jar'

Disable / Comment 
- build.gradle 
-- dependencies{
      testImplementation 'junit:junit:4.12'
      androidTestImplementation 'com.android.support.test:runner:1.0.1'
      androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.1'
    }

If behind proxy- set id/password for proxy in gradle.properties
- gradle.properties
-- systemProp.http.proxyPassword
-- systemProp.http.proxyHost
-- systemProp.https.proxyPassword
-- systemProp.https.proxyHost

