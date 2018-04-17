## Android Debugging Tool [(ADB)](https://developer.android.com/studio/command-line/adb.html)
replace **User_Name** and 
cd to C:\Users\ **User_Name** \AppData\Local\Android\Sdk\platform-tools 
adb push 
## Emulator Device Monitor
cd to C:\Users\ **User_Name** \AppData\Local\Android\Sdk\tools

### Accessing file stored in project files
```java
        String file_path = "/data/data/com.company.project_name/files/file.extension";
        File dir = new File(file_path);
        if(dir.isFile()) {
            File file = new File(file_path);
            file_path = file.getAbsolutePath();
        }
        // Example of a call to a native method
        TextView tv = findViewById(R.id.sample_text);
        tv.setText(stringFromJNI(video_file_path));
```

### Accessing file stored in SDCard
```java
        File sdcard = Environment.getExternalStorageDirectory();
        if(sdcard.isDirectory()){            
            Log.d("TAG_DEBUG_APP", sdcard.getAbsolutePath());
        }
        File file = new File(sdcard + "/file.extenstion");
        if(file.isFile()){
            Log.d("TAG_DEBUG_APP", file.getAbsolutePath());
        }else{
            Log.d("TAG_DEBUG_APP", "NOPE>>>>>>>");
        }
```
