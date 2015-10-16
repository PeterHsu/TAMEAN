# 安裝
下載Windows 60-bit 2008 R2+版本
MongoDB版本為:3.0
安裝檔名稱為:mongodb-win32-x86_64-2008plus-ssl-3.0.7-signed.msi

# OS環境
```
>wmic os get caption
>wmic os get osarchitecture
```
預設安裝目錄:"%programfiles%\MongoDB\"
新增檔案用來設定WindowsService
"%programfiles%\MongoDB\mongod.cfg"
```
systemLog:
    destination: file
    path: c:\data\log\mongod.log
storage:
    dbPath: c:\data\db
```
建置C:\data\log及\data\db目錄
執行命令,安裝成WindowsService,要用管理者身份執行
按win鍵,輸入cmd.exe,按Ctrl+Shift+Enter執行
```
"%programfiles%\MongoDB\Server\3.0\bin\mongod.exe" --config "%programfiles%\MongoDB\mongod.cfg" --install
```
啟動服務: >net start MongoDB  
關閉服務: >net stop MongoDB
移除服務: >"%programfiles%\MongoDB\Server\3.0\bin\mongod.exe" --remove
# 執行命令
執行 >mongo
help (說明)
exit (離開)
```
show dbs (查databases)
db (顯示連到的資料庫)
use names (連到指定的資料庫,即使不存在)
db.mynames.insert({name:'nathan',email:'nathan@10gen.com'}) (新增一筆document在mynames collection裡)
show dbs (已自動新增Database)
db.mynames.find() (查詢)
show collections (查collections)
db.mynames.remove() (移除會有錯誤)
```
