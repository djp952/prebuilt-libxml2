# LIBXML2 2.9.10
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
* android-28-armeabi-v7a (ndk-r20b/api-28)   
* android-28-arm64-v8a (ndk-r20b/api-28)   
* android-28-x86 (ndk-r20b/api-28)   
* rasbpian-armhf (gcc-4.8.3)   
* osx-x86_64 (apple-darwin15)   
   
**BUILD ENVIRONMENT**  
* Windows 10 x64 1809 (17763) "October 2018 Update"   
* Windows Subsystem for Linux   
* [Ubuntu on Windows 16.04 LTS](https://www.microsoft.com/store/productId/9PJN388HP8C9)   
* OSXCROSS Cross-Compiler (with Mac OSX 10.11 SDK)   

**CONFIGURE UBUNTU**   
Open "Ubuntu"   
```
sudo dpkg --add-architecture i386
sudo apt-get update
sudo apt-get install gcc-4.9 g++-4.9 libc6-dev:i386 libstdc++-4.9-dev:i386 lib32gcc-4.9-dev 
sudo apt-get install gcc-4.9-arm-linux-gnueabihf g++-4.9-arm-linux-gnueabihf gcc-4.9-arm-linux-gnueabi g++-4.9-arm-linux-gnueabi gcc-4.9-aarch64-linux-gnu g++-4.9-aarch64-linux-gnu
sudo apt-get install autoconf libtool make p7zip-full python
```

**CONFIGURE ANDROID TOOLCHAINS**   
Open "Ubuntu"   
```
wget https://dl.google.com/android/repository/android-ndk-r20b-linux-x86_64.zip
7z x android-ndk-r20b-linux-x86_64.zip
```
  
**CONFIGURE OSXCROSS CROSS-COMPILER**   
* Generate the MAC OSX 10.11 SDK Package for OSXCROSS by following the instructions provided at [PACKAGING THE SDK](https://github.com/tpoechtrager/osxcross#packaging-the-sdk).  The suggested version of Xcode to use when generating the SDK package is Xcode 7.3.1 (May 3, 2016).
* Open "Ubuntu"   
```
sudo apt-get install make clang zlib1g-dev libmpc-dev libmpfr-dev libgmp-dev
git clone https://github.com/tpoechtrager/osxcross --depth=1
cp {MacOSX10.11.sdk.tar.bz2} osxcross/tarballs/
UNATTENDED=1 osxcross/build.sh
GCC_VERSION=4.9.3 osxcross/build_gcc.sh
```
   
**BUILD LIBXML2 (linux-i686)**   
Open "Ubuntu"   
```
wget ftp://xmlsoft.org/libxml2/libxml2-sources-2.9.10.tar.gz
tar -xzf libxml2-sources-2.9.10.tar.gz
export CC=gcc-4.9
export AR=gcc-ar-4.9
export RANLIB=gcc-ranlib-4.9
export CFLAGS="-m32 -I/usr/include/i386-linux-gnu"
export LIBS=-ldl
cd libxml2-2.9.10
./configure --host=i686-pc-linux-gnu --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma
make
```
   
Get header files from include/libxml2   
Get libxml2.lib from .libs
   
**BUILD LIBXML2 (linux-x86_64)**   
Open "Ubuntu"   
```
wget ftp://xmlsoft.org/libxml2/libxml2-sources-2.9.10.tar.gz
tar -xzf libxml2-sources-2.9.10.tar.gz
export CC=gcc-4.9
export AR=gcc-ar-4.9
export RANLIB=gcc-ranlib-4.9
export CFLAGS="-I/usr/include/x86_64-linux-gnu"
export LIBS=-ldl
cd libxml2-2.9.10
./configure --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma
make
```
   
Get header files from include/libxml2   
Get libxml2.lib from .libs
   
**BUILD LIBXML2 (linux-armel)**   
Open "Ubuntu"   
```
wget ftp://xmlsoft.org/libxml2/libxml2-sources-2.9.10.tar.gz
tar -xzf libxml2-sources-2.9.10.tar.gz
export CC=arm-linux-gnueabi-gcc-4.9
export AR=arm-linux-gnueabi-gcc-ar-4.9
export RANLIB=arm-linux-gnueabi-gcc-ranlib-4.9
export LIBS=-ldl
cd libxml2-2.9.10
./configure --host=arm-linux-gnueabi --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma
make
```
   
Get header files from include/libxml2   
Get libxml2.lib from .libs
   
**BUILD LIBXML2 (linux-armhf)**   
Open "Ubuntu"   
```
wget ftp://xmlsoft.org/libxml2/libxml2-sources-2.9.10.tar.gz
tar -xzf libxml2-sources-2.9.10.tar.gz
export CC=arm-linux-gnueabihf-gcc-4.9
export AR=arm-linux-gnueabihf-gcc-ar-4.9
export RANLIB=arm-linux-gnueabihf-gcc-ranlib-4.9
export LIBS=-ldl
cd libxml2-2.9.10
./configure --host=arm-linux-gnueabihf --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma
make
```
   
Get header files from include/libxml2   
Get libxml2.lib from .libs
   
**BUILD LIBXML2 (linux-aarch64)**   
Open "Ubuntu"   
```
wget ftp://xmlsoft.org/libxml2/libxml2-sources-2.9.10.tar.gz
tar -xzf libxml2-sources-2.9.10.tar.gz
export CC=aarch64-linux-gnu-gcc-4.9
export AR=aarch64-linux-gnu-gcc-ar-4.9
export RANLIB=aarch64-linux-gnu-gcc-ranlib-4.9
export LIBS=-ldl
cd libxml2-2.9.10
./configure --host=aarch64-linux-gnu --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma
make
```
   
Get header files from include/libxml2   
Get libxml2.lib from .libs
   
**BUILD LIBXML2 (android-21-armeabi-v7a)**   
Open "Ubuntu"   
```
wget ftp://xmlsoft.org/libxml2/libxml2-sources-2.9.10.tar.gz
tar -xzf libxml2-sources-2.9.10.tar.gz
export TOOLCHAIN=$(pwd)/android-ndk-r20b/toolchains/llvm/prebuilt/linux-x86_64
export AR=$TOOLCHAIN/bin/arm-linux-androideabi-ar
export AS=$TOOLCHAIN/bin/arm-linux-androideabi-as
export CC=$TOOLCHAIN/bin/armv7a-linux-androideabi21-clang
export CXX=$TOOLCHAIN/bin/armv7a-linux-androideabi21-clang++
export LD=$TOOLCHAIN/bin/arm-linux-androideabi-ld
export RANLIB=$TOOLCHAIN/bin/arm-linux-androideabi-ranlib
export STRIP=$TOOLCHAIN/bin/arm-linux-androideabi-strip
export LIBS=-ldl
cd libxml2-2.9.10
./configure --host=arm-linux-androideabi --target=arm-linux-androideabi --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma
make
```
Get header files from include/libxml2   
Get libxml2.lib from .libs
   
**BUILD LIBXML2 (android-21-arm64-v8a)**   
Open "Ubuntu"   
```
wget ftp://xmlsoft.org/libxml2/libxml2-sources-2.9.10.tar.gz
tar -xzf libxml2-sources-2.9.10.tar.gz
export TOOLCHAIN=$(pwd)/android-ndk-r20b/toolchains/llvm/prebuilt/linux-x86_64
export AR=$TOOLCHAIN/bin/aarch64-linux-android-ar
export AS=$TOOLCHAIN/bin/aarch64-linux-android-as
export CC=$TOOLCHAIN/bin/aarch64-linux-android21-clang
export CXX=$TOOLCHAIN/bin/aarch64-linux-android21-clang++
export LD=$TOOLCHAIN/bin/aarch64-linux-android-ld
export RANLIB=$TOOLCHAIN/bin/aarch64-linux-android-ranlib
export STRIP=$TOOLCHAIN/bin/aarch64-linux-android-strip
export LIBS=-ldl
cd libxml2-2.9.10
./configure --host=aarch64-linux-android --target=aarch64-linux-android --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma
make
```
Get header files from include/libxml2   
Get libxml2.lib from .libs
   
**BUILD LIBXML2 (android-21-x86)**   
Open "Ubuntu"   
```
wget ftp://xmlsoft.org/libxml2/libxml2-sources-2.9.10.tar.gz
tar -xzf libxml2-sources-2.9.10.tar.gz
export TOOLCHAIN=$(pwd)/android-ndk-r20b/toolchains/llvm/prebuilt/linux-x86_64
export AR=$TOOLCHAIN/bin/i686-linux-android-ar
export AS=$TOOLCHAIN/bin/i686-linux-android-as
export CC=$TOOLCHAIN/bin/i686-linux-android21-clang
export CXX=$TOOLCHAIN/bin/i686-linux-android21-clang++
export LD=$TOOLCHAIN/bin/i686-linux-android-ld
export RANLIB=$TOOLCHAIN/bin/i686-linux-android-ranlib
export STRIP=$TOOLCHAIN/bin/i686-linux-android-strip
export LIBS=-ldl
cd libxml2-2.9.10
./configure --host=i686-linux-android --target=i686-linux-android --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma
make
```
Get header files from include/libxml2   
Get libxml2.lib from .libs
   
**BUILD LIBXML2 (android-28-armeabi-v7a)**   
Open "Ubuntu"   
```
wget ftp://xmlsoft.org/libxml2/libxml2-sources-2.9.10.tar.gz
tar -xzf libxml2-sources-2.9.10.tar.gz
export TOOLCHAIN=$(pwd)/android-ndk-r20b/toolchains/llvm/prebuilt/linux-x86_64
export AR=$TOOLCHAIN/bin/arm-linux-androideabi-ar
export AS=$TOOLCHAIN/bin/arm-linux-androideabi-as
export CC=$TOOLCHAIN/bin/armv7a-linux-androideabi28-clang
export CXX=$TOOLCHAIN/bin/armv7a-linux-androideabi28-clang++
export LD=$TOOLCHAIN/bin/arm-linux-androideabi-ld
export RANLIB=$TOOLCHAIN/bin/arm-linux-androideabi-ranlib
export STRIP=$TOOLCHAIN/bin/arm-linux-androideabi-strip
export LIBS=-ldl
cd libxml2-2.9.10
./configure --host=arm-linux-androideabi --target=arm-linux-androideabi --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma
make
```
Get header files from include/libxml2   
Get libxml2.lib from .libs
   
**BUILD LIBXML2 (android-28-arm64-v8a)**   
Open "Ubuntu"   
```
wget ftp://xmlsoft.org/libxml2/libxml2-sources-2.9.10.tar.gz
tar -xzf libxml2-sources-2.9.10.tar.gz
export TOOLCHAIN=$(pwd)/android-ndk-r20b/toolchains/llvm/prebuilt/linux-x86_64
export AR=$TOOLCHAIN/bin/aarch64-linux-android-ar
export AS=$TOOLCHAIN/bin/aarch64-linux-android-as
export CC=$TOOLCHAIN/bin/aarch64-linux-android28-clang
export CXX=$TOOLCHAIN/bin/aarch64-linux-android28-clang++
export LD=$TOOLCHAIN/bin/aarch64-linux-android-ld
export RANLIB=$TOOLCHAIN/bin/aarch64-linux-android-ranlib
export STRIP=$TOOLCHAIN/bin/aarch64-linux-android-strip
export LIBS=-ldl
cd libxml2-2.9.10
./configure --host=aarch64-linux-android --target=aarch64-linux-android --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma
make
```
Get header files from include/libxml2   
Get libxml2.lib from .libs
   
**BUILD LIBXML2 (android-28-x86)**   
Open "Ubuntu"   
```
wget ftp://xmlsoft.org/libxml2/libxml2-sources-2.9.10.tar.gz
tar -xzf libxml2-sources-2.9.10.tar.gz
export TOOLCHAIN=$(pwd)/android-ndk-r20b/toolchains/llvm/prebuilt/linux-x86_64
export AR=$TOOLCHAIN/bin/i686-linux-android-ar
export AS=$TOOLCHAIN/bin/i686-linux-android-as
export CC=$TOOLCHAIN/bin/i686-linux-android28-clang
export CXX=$TOOLCHAIN/bin/i686-linux-android28-clang++
export LD=$TOOLCHAIN/bin/i686-linux-android-ld
export RANLIB=$TOOLCHAIN/bin/i686-linux-android-ranlib
export STRIP=$TOOLCHAIN/bin/i686-linux-android-strip
export LIBS=-ldl
cd libxml2-2.9.10
./configure --host=aarch64-linux-android --target=aarch64-linux-android --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma
make
```
Get header files from include/libxml2   
Get libxml2.lib from .libs
   
**BUILD LIBXML2 (raspbian-armhf)**   
Open "Ubuntu"   
```
git clone https://github.com/raspberrypi/tools.git raspberrypi --depth=1
wget ftp://xmlsoft.org/libxml2/libxml2-sources-2.9.10.tar.gz
tar -xzf libxml2-sources-2.9.10.tar.gz
export PATH=$(pwd)/raspberrypi/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin:$PATH
export CC=arm-linux-gnueabihf-gcc
export AR=arm-linux-gnueabihf-gcc-ar
export RANLIB=arm-linux-gnueabihf-gcc-ranlib
export LIBS=-ldl
cd libxml2-2.9.10
./configure --host=arm-linux-gnueabihf --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma
make
```
   
Get header files from include/libxml2   
Get libxml2.lib from .libs
   
**BUILD LIBXML2 (osx-x86_64)**   
Open "Ubuntu"   
```
wget ftp://xmlsoft.org/libxml2/libxml2-sources-2.9.10.tar.gz
tar -xzf libxml2-sources-2.9.10.tar.gz
export PATH=$(pwd)/osxcross/target/bin:$PATH
export CROSS_COMPILE=x86_64-apple-darwin15-
export CFLAGS="-mmacosx-version-min=10.7 -stdlib=libc++"
export LIBS=-ldl
cd libxml2-2.9.10
./configure --host=x86_64-apple-darwin15 --with-pic --disable-shared --without-iconv --without-http --without-ftp --without-legacy --without-c14n --without-catalog --without-html --without-writer --without-schematron --without-docbook --without-output --without-push --without-modules --without-tree --without-xptr --without-xinclude --without-xpath --without-schemas --without-sax1 --without-iso8859x --without-python --without-zlib --without-lzma
OSXCROSS_NO_EXTENSION_WARNINGS=1 make
```
Get header files from include/libxml2   
Get libxml2.lib from .libs
   
## ADDITIONAL LICENSE INFORMATION
   
**XCODE AND APPLE SDKS AGREEMENT**   
The instructions provided above indirectly reference the use of intellectual material that is the property of Apple, Inc.  This intellectual material is not FOSS (Free and Open Source Software) and by using it you agree to be bound by the terms and conditions set forth by Apple, Inc. in the [Xcode and Apple SDKs Agreement](https://www.apple.com/legal/sla/docs/xcode.pdf).
