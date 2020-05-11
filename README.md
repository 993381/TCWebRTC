## TWebRTC, 腾讯云删减版WebRTC

### Android编译

1. 根据https://webrtc.googlesource.com/src/+/refs/heads/master/docs/native-code/android/index.md准备好编译环境, 并将src切换至本项目  
   fetch --nohooks webrtc_android   
   gclient sync -r bf053b6f3c7364c8e615b1f678339700be209cf7 --force  
   git remote add twebrtc https://github.com/tencentyun/TWebRTC.git  
   git fetch twebrtc  
   git checkout twebrtc/master  
2. 生成编译文件夹  
   gn gen out/Debug --args="`cat args/android_arm64.gn`"  或 gn gen out/Debug --args="`cat args/android_arm.gn`"  
3. 编译  
   ninja -C out/Debug  
4. 拷贝out/Debug/libjingle_peerconnection_so.so到[TWebRTC-Android-SDK](https://github.com/tencentyun/TWebRTC-Android-SDK)/twebrtcsdk/libs/arm64-v8a 或 armeabi-v7a文件夹下, 进行aar编译和publish到jcenter  

### IOS 编译  
  
1. 安装depot_tools并配置环境变量 类似android  
   fetch --nohooks webrtc_ios  
   gclient sync -r bf053b6f3c7364c8e615b1f678339700be209cf7 --force  
   git remote add twebrtc https://github.com/tencentyun/TWebRTC.git  
   git fetch twebrtc  
   git checkout twebrtc/master  
     
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
