# RocketMQ-Client-CPP x64 build on VS2019#
I don't think anyone needs this anymore because it's significantly behind the latest release - too many things have changed. The current latest version can be found at:
https://github.com/apache/rocketmq-clients/tree/cpp-5.0.2/cpp , this version build with bazel.

However, I did invest considerable time figuring out how to build this specific version with VS2019 (in case it might help someone).

# Building Step
## 1. build boost <br>
* Enter thirdparty\boost_1_58_0 and run bootstrap.bat
* Modify the file thirdparty\boost_1_58_0\project-config.jam with your cl.exe path as below
  ```
  using msvc : 14.2 :
  "C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Tools\MSVC\14.29.30133\bin\Hostx64\x64\cl.exe"; 
  ```
* Run b2.exe with your zlib path

  ```
  b2.exe install --prefix=..\boost-vc142 -- 
  build-type=complete --toolset=msvc-14.2 -s 
  ZLIB_SOURCE="C:\hufeng\rocketmq-client-cpp-windows- 
   vs2019\thirdparty\zlib-1.2.3-src\src\zlib\1.2.3\zlib- 
    1.2.3" threading=multi address-model=64 debug release
  ```
## 2 Build Solution
* Open the Solution File
Locate and open rocketmq-client-cpp.sln in Visual Studio.

* Configure for x64
In the toolbar, select:
x64 (Platform) → Debug (Configuration)
(Release configuration follows the same steps if needed later.)