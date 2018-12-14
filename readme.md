# 3DS Max模型浏览工具

# 1. 环境准备
1. VMware Ubuntu 16.04.5 x64
2. qt-everywhere-enterprise-src-4.8.7.tar.gz
3. assimp-4.1.0.tar.gz

## 1.1 安装OpenGL ES v2开发包
`sudo apt-get install libgles2-mesa-dev -y`

## 1.2 安装OpenGL utility开发包
`sudo apt-get install libglu1-mesa-dev -y`

tips：确定包安装后都安装了哪些文件可以通过如下命令查看<br>
`dpkg -L libglu1-mesa-dev`


# 2. AssImp编译与安装
## 2.1 AssImp-3.0.1270版本 构建方法
`unzip assimp--3.0.1270-source-only.zip`<br>
`mv assimp--3.0.1270-source-only assimp-3.0.1270`<br>
`mkdir assimp-3.0.1270_build`<br>
`cd assimp-3.0.1270_build`<br>
`cmake -DENABLE_BOOST_WORKAROUND=ON -DCMAKE_INSTALL_PREFIX=~/share/install/assimp-3.0.1270 ../assimp-3.0.1270`<br>
`make`<br>
`make install`<br>
	

## 2.2 AssImp-4.1.0 git版本 构建方法
```
unzip assimp-4.1.0.zip
mkdir assimp-4.1.0_build
cd assimp-4.1.0_build
cmake -DCMAKE_INSTALL_PREFIX=~/share/install/assimp-4.1.0 ../assimp-4.1.0
make
make install
```

注意：当前主要选取git仓库(https://github.com/assimp/assimp/)中的特定版本(git hash:f29af1abc08b2e3d08efa3808f6458bed39e4150)，因为从更新记录看，近期的某个修改开始已经废除了Qt 4的支持，仅支持Qt 5

# 3. Qt 4.8.7源码编译并安装
## 3.1 序列号
```
FGKX-FML-F4M-4CX-D6YWX-98X87-11DF
```

## 3.2 desktop版本
```
./configure -fast -shared -release -confirm-license -exceptions -qt-freetype -qt-zlib -qt-libpng -qt-libtiff -qt-libjpeg -qt-libmng -no-largefile -no-accessibility -no-qt3support -no-openssl -opengl desktop -nomake demos -nomake docs -nomake examples -nomake tools -prefix ~/share/install/qt-4.8.7-desktop
make
make install
```

## 3.3 es2版本
```
./configure -fast -shared -release -confirm-license -exceptions -qt-freetype -qt-zlib -qt-libpng -qt-libtiff -qt-libjpeg -qt-libmng -no-largefile -no-accessibility -no-qt3support -no-openssl -opengl es2 -nomake demos -nomake docs -nomake examples -nomake tools -prefix ~/share/install/qt-4.8.7-es2
make
make install
```

# 4. AssimpQtViewer

## 4.1 AssimpQtViewer
注意：这个工具来自assimp-4.1.0 git版本自身的tools\assimp_qt_viewer，为顺利编译，增补pro项目文件，该代码有C++11的需求，暂时以手动修改Makefile，添加-std=c++11的方式

## 4.2 AssimpLoadingBlogCode
注意：这个工具只支持Qt 5，但是能同时支持OpenGL和OpenGL ES，目前暂时作为参考
