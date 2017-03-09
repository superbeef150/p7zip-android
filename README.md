# p7zip android jni lib

This fork exists because I wanted to compile 7z so I could extract ISO's from the android shell, but there were issues with the original repo causing it to not build.

### Now with HugeFiles (>2GB) on!



I also needed to be able to support files greater than 2GB (indicated by HugeFiles=on vs HugeFiles=off in the top of 7z's output). The reason that files >2GB don't work by default is that 7z uses `lseek` and `off_t` rather than their 64 bit equivalents `lseek64` and `off64_t`.

[This issue isn't specific to 7z](https://bugzilla.xamarin.com/show_bug.cgi?id=17128), and as stated in that link, this can typically be solved by using "-D_FILE_OFFSET_BITS=64" in the compiler flags (LOCAL_CFLAGS in ndk). Unfortunately the ndk does not seem to acknowledge that flag in it's current state (althought supposedly [it will soon](https://code.google.com/p/android/issues/detail?id=64613)), so I made the replacements manually.

#To build 7z:
```
cd  p7zip-android\p7zip_15.09\CPP\ANDROID\7z\jni
ndk-build
```
Tested with android-ndk-r14. Other executables (p7zip, 7za, etc) have not been tested.
