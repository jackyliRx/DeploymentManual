# DBeaver 23的連線教學

## 設定MYSQL
1. 在 WSL 2 中啟動 MySQL 服務，執行以下命令以啟動啟動：  
 ```
 sudo service mysql start
 ```
2. 檢查 MySQL 服務狀態：  
 ```
 sudo service mysql status
 ```
3. 尋找 WSL 2 的 IP 位址，為了從 Windows 連線到 WSL 2 中的 MySQL，需要找到 WSL 2 的 IP 位址。   
 ```
 hostname -I
 ```
4. 設定 MySQL 允許外部連接，設定檔 mysqld.cnf(可跳過)：  
 ```
 sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
 ```
5. 找到 bind-address 行，並將其改為 0.0.0.0，以允許來自所有位址的連接：
   > 按 Ctrl + X，然後按 Y，最後按 Enter 儲存並退出編輯器。
 ```
 bind-address = 0.0.0.0
```
6. 重啟 MySQL 服務：  
 ```
 sudo service mysql restart
 ```
7. 建立遠端存取使用者（可選），確保 MySQL 使用者允許從外部連線。  
 如果需要，可以建立一個允許從任何主機連接的使用者：  
 ```
 CREATE USER 'your_username'@'%' IDENTIFIED BY 'your_password';
 GRANT ALL PRIVILEGES ON *.* TO 'your_username'@'%';
 FLUSH PRIVILEGES;
 ```

## DBeaver 設定連接
在 "Connection Settings" 頁面中，填寫以下資訊：  
主機名稱：輸入 WSL 2 的 IP 位址，例如 172.20.240.1。  
連接埠：預設 MySQL 連接埠為 3306，如果有更改，請填寫相應連接埠。  
資料庫：輸入您要連線的資料庫名稱。  
使用者名稱：輸入 MySQL 使用者名，例如 root 或新建立的使用者。  
密碼：輸入對應的使用者密碼。  
測試連接：  
    點選 "Test Connection" 按鈕，確保 DBeaver 能成功連線到 MySQL 資料庫。  
