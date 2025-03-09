# WebRTCBuildForAndroid

Android用WebRTCライブラリのビルド
OpenH264をバイナリファイルで組み込む

## バイナリファイル配置
DLしたバイナリファイル(libopenh264.so)をアーキテクチャ毎のディレクトリに配置

- arm64-v8aを対象にした例

    ~~~sh
    $HOME/work/webrtc/android/src/third_party/android_toolchain/ndk/toolchains/llvm/prebuilt/linux-x86_64/sysroot/usr/lib/aarch64-linux-android/21/pkgconfig
    ~~~



## pkg-config設定
アーキテクチャ毎のディレクトリにopenh264.pcファイル配置

- arm64-v8aを対象にした例

    ~~~sh
    $HOME/work/webrtc/android/src/third_party/android_toolchain/ndk/toolchains/llvm/prebuilt/linux-x86_64/sysroot/usr/lib/aarch64-linux-android/21/pkgconfig
    ~~~

- 反映の確認

    ~~~sh
    sudo ldconfig
    pkg-config --libs --cflags openh264
    ~~~

    出力結果例

    ~~~sh
    -I/home/name/work/webrtc/android/src/third_party/android_toolchain/ndk/include -L/home/hiro/work/webrtc/android/src/third_party/android_toolchain/ndk/toolchains/llvm/prebuilt/linux-x86_64/sysroot/usr/lib/aarch64-linux-android/21/ -lopenh264
    ~~~


## 環境変数
- env.txtの内容をセット

## ビルドツール実行

- arm64-v8aを対象にした例

    ~~~sh
    ./tools_webrtc/android/build_aar.py --arch arm64-v8a --extra-gn-args 'rtc_use_h264=true' 'rtc_system_openh264=true treat_warnings_as_errors=false'
    ~~~
