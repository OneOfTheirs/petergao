Please store third party libraries source code here. 

# How to build libpng libraries
To build libpng (and zlib) for PC linux and AM5728, please ensure they are placed at 
/home/luba/libpng-1.6.34
/home/luba/zlib-1.2.8
and TI-SDK at
/home/luba/ti-processor-sdk-linux-am57xx-evm-04.03.00.05
If you prefer your own place, the following script need to be modified accordingly.

## Build for ubuntu linux
Please copy both of libpng-1.6.34 and zlib-1.2.8 to a local filesystem 
(not remote access to Windows, because you won't be able to create symlink in windows)

Terminal A:
```
cd zlib-1.2.8
rm -rf build
mkdir build
cd build
cmake ..
make
```
Terminal B:
```
cd libpng-1.6.34
rm -rf build
mkdir build
cd build
cmake .. -DZLIB_LIBRARY=/home/luba/zlib-1.2.8/build/libz.a -DZLIB_INCLUDE_DIR=/home/luba/zlib-1.2.8/build 
```
for debug:
```
cmake .. -DCMAKE_BUILD_TYPE=DEBUG -DPNG_DEBUG=1 
```
for release:
```
cmake .. -DCMAKE_BUILD_TYPE=RELEASE -DPNG_DEBUG=0
make 
```
## Build for AM5728
Terminal A:
```
source /home/luba/ti-processor-sdk-linux-am57xx-evm-04.03.00.05/linux-devkit/environment-step
cd zlib-1.2.8
rm -rf build
mkdir build
cd build
cmake ..
make
```
Terminal B:
```
source /home/luba/ti-processor-sdk-linux-am57xx-evm-04.03.00.05/linux-devkit/environment-step
cd libpng-1.6.34
rm -rf build
mkdir build
cd build
cmake .. -DZLIB_LIBRARY=/home/luba/zlib-1.2.8/build/libz.a -DZLIB_INCLUDE_DIR=/home/luba/zlib-1.2.8/build -DPNG_DEBUG=1
cmake .. -DM_LIBRARY=/home/luba/ti-processor-sdk-linux-am57xx-evm-04.03.00.05/linux-devkit/sysroots/armv7ahf-neon-linux-gnueabi/usr/lib/libm.so
```
for debug:
```
cmake .. -DCMAKE_BUILD_TYPE=DEBUG
```
for release:
```
cmake .. -DCMAKE_BUILD_TYPE=RELEASE
make 
```

## For windows

Open libpng-1.6.34\projects\vstudio\vstudio.sln in visual studio
compile as normal for debug and release
