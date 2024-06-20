**DBeaver 23的連線教學**

**設定MYSQL**
1. 在 WSL 2 中啟動 MySQL 服務
1-1. 啟動 MySQL 服務：
 開啟 WSL 終端，並執行以下命令以啟動 MySQL 服務：
 ```
 sudo service mysql start
 ```
 1-2. 檢查 MySQL 服務狀態：
 確保 MySQL 服務正在運作：
 ```
 sudo service mysql status
 ```
2. 尋找 WSL 2 的 IP 位址
 為了從 Windows 連線到 WSL 2 中的 MySQL，您需要找到 WSL 2 的 IP 位址。
 2-1. 在 WSL 終端機中取得 IP 位址：
 ```
 hostname -I
 ```
3. 設定 MySQL 允許外部連接
 3-1. 編輯 MySQL 設定檔設定檔(可跳過)：
 編輯 MySQL 設定檔 mysqld.cnf：
 ```
 sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
 ```
 3-2. 修改綁定位址：
 找到 bind-address 行，並將其改為 0.0.0.0，以允許來自所有位址的連接：
 > bind-address = 0.0.0.0
 3-3. 儲存並退出：
 按 Ctrl + X，然後按 Y，最後按 Enter 儲存並退出編輯器。
 3-4. 重啟 MySQL 服務：
 ```
 sudo service mysql restart
 ```
 3-5. 建立遠端存取使用者（可選）：
 確保 MySQL 使用者允許從外部連線。如果需要，可以建立一個允許從任何主機連接的使用者：
 ```
 CREATE USER 'your_username'@'%' IDENTIFIED BY 'your_password';
 GRANT ALL PRIVILEGES ON *.* TO 'your_username'@'%';
 FLUSH PRIVILEGES;
 ```

**在 DBeaver 中設定連接**

點選功能表列中的 "Database" -> "New Connection"。
選擇 MySQL，然後點選 "Next"。
設定連接參數：

在 "Connection Settings" 頁面中，填寫以下資訊：

主機名稱：輸入 WSL 2 的 IP 位址，例如 172.20.240.1。
連接埠：預設 MySQL 連接埠為 3306，如果有更改，請填寫相應連接埠。
資料庫：輸入您要連線的資料庫名稱。
使用者名稱：輸入 MySQL 使用者名，例如 root 或新建立的使用者。
密碼：輸入對應的使用者密碼。
測試連接：

點選 "Test Connection" 按鈕，確保 DBeaver 能成功連線到 MySQL 資料庫。

儲存連線：

如果測試連線成功，點選 "Finish" 儲存連線設定。
</details>
