# http下載示範項目中https無法下載問題

該示範項目用QProgressDialog作爲UI類，核心功能用QNetworkAccessManager和QUrl完成。

編譯運行時，如果輸入下載地址為https協議，會導致下載失敗錯誤如下

qt.network.ssl: QSslSocket::connectToHostEncrypted: TLS initialization failed

原因在於沒有安裝openssl庫，這裏openssl庫是可選的，需要用戶自己放到相應的bin目錄下

qt5官方的庫路徑在 `{Qt安裝目錄}\Qt5.12.0\Tools\mingw730_64\opt\bin\` 下

在此目錄下找到
ssleay32.dll 和 libeay32.dll


根據項目deply配置，將以上兩個文件複製到編譯輸出文件夾下即可。

QT默認編譯輸出文件夾與項目文件夾平級。

# 與上文同理可以解決許多DLL丟失問題
