# zmq 安装与部署

# 1.安裝依賴

```
sudo apt-get install libtool pkg-config build-essential autoconf automake
```

# 2.編譯安裝ZMQ使用的加密庫

```
git clone git://github.com/jedisct1/libsodium.git
cd libsodium
./autogen.sh -s linux
./configure && make check
sudo make install
sudo ldconfig
cd ..
```

如果是從windows中的github應用下載的源碼，拷貝到linux虛擬機中運行autogen.sh時出現文件結尾錯誤

```
/bin/sh^M: bad interpreter: No such file or directory
```

可以通過vim打開該文件(autogen.sh)然後另存文件格式為unix

```
// [ESC]
:set fileformat=unix
// [ESC]
:wq!
```


# 3.編譯安裝ZMQ核心庫

```
git clone git://github.com/zeromq/libzmq.git
cd libzmq
./autogen.sh
./configure && make check
sudo make install
sudo ldconfig
cd ..
```

#4.編譯安裝ZMQ的C綁定

```
git clone git://github.com/zeromq/czmq.git
cd czmq
./autogen.sh
./configure && make check
sudo make install
sudo ldconfig
cd ..
```

#5.添加ZMQC++綁定

```
git clone https://github.com/zeromq/cppzmq.git
cd cppzmq
sudo cp zmq.hpp /usr/local/include/
cd ..
```

#6.添加庫編譯命令行

```
g++ test.cpp -o test -lzmq
```

vs中 鏈接器>所有選項>庫依賴項>添加zmq

#7.注意事項
zmq.hpp適合單綫程zmq服務，因爲實現上用了全局裏的同一個handle
所以不建議用zmq的c++11接口。采用c接口適應多綫程編程。
zhelper.h在 zguide項目中
