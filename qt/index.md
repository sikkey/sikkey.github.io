# QT Develop

# qt lose dll

[openssl dll setting of qt project](qt開發缺少庫的注意事項.md)

除了在項目裡導入dll以外， 還需要將lib和dll文件copy到debug/*.exe路徑下

# qt 打包

1. release 方式運行一次
2. 將release目錄下的exe文件copy到要打包的文件夾中
3. 此時還缺少許多dll
4. 在win10開始菜單搜索QT，打開QT5.12 FOR DESKTOP 選擇相應的打包編譯器
5. 運行 ```cd /d 打包文件路徑```
6. 運行 ```windeployqt 可執行文件名.exe```
