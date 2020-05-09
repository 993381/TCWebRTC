## 删减版WebRTC

### Android编译

1. 根据https://webrtc.googlesource.com/src/+/refs/heads/master/docs/native-code/android/index.md准备好编译环境, 并将src切本项目
   git remote add webrtc-client-native https://github.com/tencentyun/webrtc-client-native.git
   git fetch webrtc-client-native
   git checkout webrtc-client-native/master
   gclient sync -r bf053b6f3c7364c8e615b1f678339700be209cf7 --force
2. 生成编译文件夹
   gn gen out/Debug --args='target_os="android" target_cpu="arm"'
3. 替换编译配置文件
   cp args/android_arm.gn out/Debug/args.gn 或 cp args/android_arm64.gn out/Debug/args.gn
4. 编译
   ninja -C out/Debug
5. 拷贝out/Debug/libjingle_peerconnection_so.so到leb-android-sdk/lebwebrtcsdk/src/libs/arm64-v8a 或armeabi-v7a文件夹下
6. 拷贝out/Debug/lib.java/sdk/android/libwebrtc.jar到leb-android-sdk/lebwebrtcsdk/src/libs文件夹下 

### IOS 编译
1. 安装depot_tools并配置环境变量 类似android
   fetch --nohooks webrtc_ios
   gclient sync -r bf053b6f3c7364c8e615b1f678339700be209cf7 --force
   git remote add webrtc-client-native https://github.com/tencentyun/webrtc-client-native.git
   git fetch webrtc-client-native
   git checkout webrtc-client-native/master
   
 2. 使用优化参数打包编译生成 webrtc framework.
    sh tools_webrtc/ios/build_ios_libs.sh --extra-gn-args="`cat args/ios.gn`"
    
 3. 编译app和调试
    gn gen out/ios_64 --args='target_os="ios" target_cpu="arm64"' --xcode
    ninja -C out/ios_64 AppRTCMobile
    编译的时候可能会有账号问题。需要将examples/objc/AppRTCMobile/ios/info.plist文件的Bundle identifier改成自己的账号。
    
    
### More info

 * Official web site: http://www.webrtc.org
 * Master source code repo: https://webrtc.googlesource.com/src
 * Samples and reference apps: https://github.com/webrtc
 * Mailing list: http://groups.google.com/group/discuss-webrtc
 * Continuous build: http://build.chromium.org/p/client.webrtc
 * [Coding style guide](style-guide.md)
 * [Code of conduct](CODE_OF_CONDUCT.md)
