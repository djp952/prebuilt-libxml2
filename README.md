# LIBXML2 2.9.13
[http://www.xmlsoft.org/](http://www.xmlsoft.org/)   
  
**TARGETS**   
* linux-i686 (gcc-4.9)   
* linux-x86_64 (gcc-4.9)   
* linux-armel (gcc-4.9)   
* linux-armhf (gcc-4.9)   
* linux-aarch64 (gcc-4.9)   
* android-21-armeabi-v7a (ndk-r20b/api-21)   
* android-21-arm64-v8a (ndk-r20b/api-21)   
* android-21-x86 (ndk-r20b/api-21)   
* android-21-x86_64 (ndk-r20b/api-21)   
* rasbpian-armhf (gcc-4.8.3)   
* osx-x86_64 (apple-darwin19)   
   
**BUILD ENVIRONMENT**  
* Windows 10 x64 20H2 (19042)   
* [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) (WSL v1 recommended)   
* [WSL Ubuntu 18.04 LTS Distro](https://www.microsoft.com/store/productId/9N9TNGVNDL3Q)   

**REQUIRED: CONFIGURE UBUNTU ON WINDOWS**   
* Open "Ubuntu 18.04 LTS"   
```
sudo dpkg --add-architecture i386
sudo add-apt-repository 'deb http://archive.ubuntu.com/ubuntu/ xenial main universe'
sudo apt-get update
sudo apt-get install gcc-4.9 g++-4.9 libc6-dev:i386 libstdc++-4.9-dev:i386 lib32gcc-4.9-dev
sudo apt-get install gcc-4.9-arm-linux-gnueabihf g++-4.9-arm-linux-gnueabihf gcc-4.9-arm-linux-gnueabi g++-4.9-arm-linux-gnueabi gcc-4.9-aarch64-linux-gnu g++-4.9-aarch64-linux-gnu
sudo apt-get install autoconf libtool make p7zip-full python
```

**CONFIGURE ANDROID TOOLCHAINS**   
* Open "Ubuntu 18.04 LTS"   
```
wget https://dl.google.com/android/repository/android-ndk-r20b-linux-x86_64.zip
7z x android-ndk-r20b-linux-x86_64.zip
```
  
**BUILD OSXCROSS CROSS-COMPILER**   
* Download [Xcode 11.3.1](https://download.developer.apple.com/Developer_Tools/Xcode_11.3.1/Xcode_11.3.1.xip) __(Account required)__ to a location accessible to the WSL Ubuntu 18.04 LTS Distro
* Open "Ubuntu 18.04 LTS"   
```
sudo apt-get install cmake clang llvm-dev liblzma-dev libxml2-dev uuid-dev libssl-dev libbz2-dev zlib1g-dev
cp {Xcode_11.3.1.xip} ~/
git clone https://github.com/tpoechtrager/osxcross --depth=1
osxcross/tools/gen_sdk_package_pbzx.sh ~/Xcode_11.3.1.xip
mv osxcross/MacOSX10.15.sdk.tar.xz osxcross/tarballs/
UNATTENDED=1 osxcross/build.sh
osxcross/build_compiler_rt.sh
sudo mkdir -p /usr/lib/llvm-6.0/lib/clang/6.0.0/include
sudo mkdir -p /usr/lib/llvm-6.0/lib/clang/6.0.0/lib/darwin
sudo cp -rv $(pwd)/osxcross/build/compiler-rt/compiler-rt/include/sanitizer /usr/lib/llvm-6.0/lib/clang/6.0.0/include
sudo cp -v $(pwd)/osxcross/build/compiler-rt/compiler-rt/build/lib/darwin/*.a /usr/lib/llvm-6.0/lib/clang/6.0.0/lib/darwin
sudo cp -v $(pwd)/osxcross/build/compiler-rt/compiler-rt/build/lib/darwin/*.dylib /usr/lib/llvm-6.0/lib/clang/6.0.0/lib/darwin
```
   
**BUILD LIBXML2 (linux-i686)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://gitlab.gnome.org/GNOME/libxml2 -b v2.9.13 --depth=1
export CC=gcc-4.9
export AR=gcc-ar-4.9
export RANLIB=gcc-ranlib-4.9
export CFLAGS="-m32 -I/usr/include/i386-linux-gnu"
export LIBS=-ldl
cd libxml2
./autogen.sh --host=i686-pc-linux-gnu --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma --prefix=$(pwd)/out
make && make install
```
Get files from libxml2/out   
   
**BUILD LIBXML2 (linux-x86_64)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://gitlab.gnome.org/GNOME/libxml2 -b v2.9.13 --depth=1
export CC=gcc-4.9
export AR=gcc-ar-4.9
export RANLIB=gcc-ranlib-4.9
export CFLAGS="-I/usr/include/x86_64-linux-gnu"
export LIBS=-ldl
cd libxml2
./autogen.sh --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma --prefix=$(pwd)/out --prefix=$(pwd)/out
make && make install
```
Get files from libxml2/out   
   
**BUILD LIBXML2 (linux-armel)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://gitlab.gnome.org/GNOME/libxml2 -b v2.9.13 --depth=1
export CC=arm-linux-gnueabi-gcc-4.9
export AR=arm-linux-gnueabi-gcc-ar-4.9
export RANLIB=arm-linux-gnueabi-gcc-ranlib-4.9
export LIBS=-ldl
cd libxml2
./autogen.sh --host=arm-linux-gnueabi --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma --prefix=$(pwd)/out
make && make install
```
Get files from libxml2/out   
   
**BUILD LIBXML2 (linux-armhf)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://gitlab.gnome.org/GNOME/libxml2 -b v2.9.13 --depth=1
export CC=arm-linux-gnueabihf-gcc-4.9
export AR=arm-linux-gnueabihf-gcc-ar-4.9
export RANLIB=arm-linux-gnueabihf-gcc-ranlib-4.9
export LIBS=-ldl
cd libxml2
./autogen.sh --host=arm-linux-gnueabihf --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma --prefix=$(pwd)/out
make && make install
```
Get files from libxml2/out   
   
**BUILD LIBXML2 (linux-aarch64)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://gitlab.gnome.org/GNOME/libxml2 -b v2.9.13 --depth=1
export CC=aarch64-linux-gnu-gcc-4.9
export AR=aarch64-linux-gnu-gcc-ar-4.9
export RANLIB=aarch64-linux-gnu-gcc-ranlib-4.9
export LIBS=-ldl
cd libxml2
./autogen.sh --host=aarch64-linux-gnu --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma --prefix=$(pwd)/out
make && make install
```
Get files from libxml2/out   
   
**BUILD LIBXML2 (android-21-armeabi-v7a)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://gitlab.gnome.org/GNOME/libxml2 -b v2.9.13 --depth=1
export TOOLCHAIN=$(pwd)/android-ndk-r20b/toolchains/llvm/prebuilt/linux-x86_64
export AR=$TOOLCHAIN/bin/arm-linux-androideabi-ar
export AS=$TOOLCHAIN/bin/arm-linux-androideabi-as
export CC=$TOOLCHAIN/bin/armv7a-linux-androideabi21-clang
export CXX=$TOOLCHAIN/bin/armv7a-linux-androideabi21-clang++
export LD=$TOOLCHAIN/bin/arm-linux-androideabi-ld
export RANLIB=$TOOLCHAIN/bin/arm-linux-androideabi-ranlib
export STRIP=$TOOLCHAIN/bin/arm-linux-androideabi-strip
export LIBS=-ldl
cd libxml2
./autogen.sh --host=arm-linux-androideabi --target=arm-linux-androideabi --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma --prefix=$(pwd)/out
make && make install
```
Get files from libxml2/out   
   
**BUILD LIBXML2 (android-21-arm64-v8a)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://gitlab.gnome.org/GNOME/libxml2 -b v2.9.13 --depth=1
export TOOLCHAIN=$(pwd)/android-ndk-r20b/toolchains/llvm/prebuilt/linux-x86_64
export AR=$TOOLCHAIN/bin/aarch64-linux-android-ar
export AS=$TOOLCHAIN/bin/aarch64-linux-android-as
export CC=$TOOLCHAIN/bin/aarch64-linux-android21-clang
export CXX=$TOOLCHAIN/bin/aarch64-linux-android21-clang++
export LD=$TOOLCHAIN/bin/aarch64-linux-android-ld
export RANLIB=$TOOLCHAIN/bin/aarch64-linux-android-ranlib
export STRIP=$TOOLCHAIN/bin/aarch64-linux-android-strip
export LIBS=-ldl
cd libxml2
./autogen.sh --host=aarch64-linux-android --target=aarch64-linux-android --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma --prefix=$(pwd)/out
make && make install
```
Get files from libxml2/out   
   
**BUILD LIBXML2 (android-21-x86)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://gitlab.gnome.org/GNOME/libxml2 -b v2.9.13 --depth=1
export TOOLCHAIN=$(pwd)/android-ndk-r20b/toolchains/llvm/prebuilt/linux-x86_64
export AR=$TOOLCHAIN/bin/i686-linux-android-ar
export AS=$TOOLCHAIN/bin/i686-linux-android-as
export CC=$TOOLCHAIN/bin/i686-linux-android21-clang
export CXX=$TOOLCHAIN/bin/i686-linux-android21-clang++
export LD=$TOOLCHAIN/bin/i686-linux-android-ld
export RANLIB=$TOOLCHAIN/bin/i686-linux-android-ranlib
export STRIP=$TOOLCHAIN/bin/i686-linux-android-strip
export LIBS=-ldl
cd libxml2
./autogen.sh --host=i686-linux-android --target=i686-linux-android --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma --prefix=$(pwd)/out
make && make install
```
Get files from libxml2/out   
   
**BUILD LIBXML2 (android-21-x86_64)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://gitlab.gnome.org/GNOME/libxml2 -b v2.9.13 --depth=1
export TOOLCHAIN=$(pwd)/android-ndk-r20b/toolchains/llvm/prebuilt/linux-x86_64
export AR=$TOOLCHAIN/bin/x86_64-linux-android-ar
export AS=$TOOLCHAIN/bin/x86_64-linux-android-as
export CC=$TOOLCHAIN/bin/x86_64-linux-android21-clang
export CXX=$TOOLCHAIN/bin/x86_64-linux-android21-clang++
export LD=$TOOLCHAIN/bin/x86_64-linux-android-ld
export RANLIB=$TOOLCHAIN/bin/x86_64-linux-android-ranlib
export STRIP=$TOOLCHAIN/bin/x86_64-linux-android-strip
export LIBS=-ldl
cd libxml2
./autogen.sh --host=x86_64-linux-android --target=x86_64-linux-android --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma --prefix=$(pwd)/out
make && make install
```
Get files from libxml2/out   
   
**BUILD LIBXML2 (raspbian-armhf)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://github.com/raspberrypi/tools.git raspberrypi --depth=1
git clone https://gitlab.gnome.org/GNOME/libxml2 -b v2.9.13 --depth=1
export PATH=$(pwd)/raspberrypi/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin:$PATH
export CC=arm-linux-gnueabihf-gcc
export AR=arm-linux-gnueabihf-gcc-ar
export RANLIB=arm-linux-gnueabihf-gcc-ranlib
export LIBS=-ldl
cd libxml2
./autogen.sh --host=arm-linux-gnueabihf --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma --prefix=$(pwd)/out
make && make install
```   
Get files from libxml2/out   
   
**BUILD LIBXML2 (osx-x86_64)**   
Open "Ubuntu 18.04 LTS"   
```
git clone https://gitlab.gnome.org/GNOME/libxml2 -b v2.9.13 --depth=1
export PATH=$(pwd)/osxcross/target/bin:$PATH
export CROSS_COMPILE=x86_64-apple-darwin19-
export CC=x86_64-apple-darwin19-clang
export AR=x86_64-apple-darwin19-ar
export RANLIB=x86_64-apple-darwin19-ranlib
export CFLAGS="-mmacosx-version-min=10.9 -stdlib=libc++"
export LIBS=-ldl
cd libxml2
./autogen.sh --host=x86_64-apple-darwin19 --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma --prefix=$(pwd)/out
OSXCROSS_NO_EXTENSION_WARNINGS=1 make
OSXCROSS_NO_EXTENSION_WARNINGS=1 make install
```
Get files from libxml2/out   
   
## ADDITIONAL LICENSE INFORMATION
   
**XCODE AND APPLE SDKS AGREEMENT**   
The instructions provided above indirectly reference the use of intellectual material that is the property of Apple, Inc.  This intellectual material is not FOSS (Free and Open Source Software) and by using it you agree to be bound by the terms and conditions set forth by Apple, Inc. in the [Xcode and Apple SDKs Agreement](https://www.apple.com/legal/sla/docs/xcode.pdf).
