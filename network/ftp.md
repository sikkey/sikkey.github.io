# FTP命令及響應碼

## FTP命令

命令字符串結尾要加'\n'
ABOR：中斷數據連接程序
ACCT <account>：系統特權帳號
ALLO <bytes>：為服務器上的文件存儲器分配字節
APPE <filename>：添加文件到服務器同名文件
CDUP <dir path>：改變服務器上的父目錄
CWD <dir path>：改變服務器上的工作目錄
DELE <filename>：刪除服務器上的指定文件
HELP <command>：返回指定命令信息
LIST <name>：如果是文件名列出文件信息，如果是目錄則列出文件列表
MODE <mode>：傳輸模式（S=流模式，B=塊模式，C=壓縮模式）
MKD <directory>：在服務器上建立指定目錄
NLST <directory>：列出指定目錄內容
NOOP：無動作，除了來自服務器上的承認
PASS <password>：系統登錄密碼
PASV：請求服務器等待數據連接
PORT <address>：IP 地址和兩字節的端口 ID
PWD：顯示當前工作目錄
QUIT：從 FTP 服務器上退出登錄
REIN：重新初始化登錄狀態連接
REST <offset>：由特定偏移量重啟文件傳遞
RETR <filename>：從服務器上找回（複製）文件
RMD <directory>：在服務器上刪除指定目錄
RNFR <old path>：對舊路徑重命名
RNTO <new path>：對新路徑重命名
SITE <params>：由服務器提供的站點特殊參數
SMNT <pathname>：掛載指定文件結構
STAT <directory>：在當前程序或目錄上返回信息
STOR <filename>：儲存（複製）文件到服務器上
STOU <filename>：儲存文件到服務器名稱上
STRU <type>：數據結構（F=文件，R=記錄，P=頁面）
SYST：返回服務器使用的操作系統
TYPE <data type>：數據類型（A=ASCII，E=EBCDIC，I=binary）
USER <username>：系統登錄的用戶名

## FTP響應碼

110：新文件指示器上的重啟標記
120：服務器準備就緒的時間（分鐘數）
125：打開數據連接，開始傳輸
150：打開連接
200：成功
202：命令沒有執行
211：系統狀態回复
212：目錄狀態回复
213：文件狀態回复
214：幫助信息回复
215：系統類型回复
220：服務就緒
221：退出網絡
225：打開數據連接
226：結束數據連接
227：進入被動模式（IP 地址、ID 端口）
230：登錄因特網
250：文件行為完成
257：路徑名建立
331：要求密碼
332：要求帳號
350：文件行為暫停
421：服務關閉
425：無法打開數據連接
426：結束連接
450：文件不可用
451：遇到本地錯誤
452：​​磁盤空間不足
500：無效命令
501：錯誤參數
502：命令沒有執行
503：錯誤指令序列
504：無效命令參數
530：未登錄網絡
532：存儲文件需要帳號
550：文件不可用
551：不知道的頁類型
552：超過存儲分配
553：文件名不允許
