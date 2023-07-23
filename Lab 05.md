### **安裝 Apache 網頁伺服器以及其應用的步驟** - 學習筆記

**Step 1：更新套件列表**
在開始安裝之前，首先要確保系統套件列表是最新的。打開終端機（Terminal）並執行以下指令：

```
sudo apt update
```

**Step 2：安裝 Apache 網頁伺服器**
更新套件列表後，安裝 Apache 。在終端機中執行以下指令：

```
sudo apt install apache2
```

當系統提示時，輸入管理員密碼（sudo 密碼）。安裝過程中會詢問是否確定要安裝，輸入 `Y` 然後按下 Enter 繼續。

**Step 3：啟動 Apache 服務**
安裝完成後，Apache 會自動啟動。可以再次確認一下它是否正在運行：

```
sudo systemctl status apache2
```

如果一切正常，看到以下的輸出：

```
● apache2.service - The Apache HTTP Server
   Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
   Active: active (running) since ... ; ...
```

**Step 4：測試 Apache**
完成安裝後，可以在瀏覽器中輸入伺服器 IP 地址或主機名稱來測試 Apache 是否正常運行。如果一切正常，會看到 Apache 的預設歡迎頁面。

**應用及順序：**
安裝完成後， Ubuntu 系統上現在就有了一個運行中的 Apache 網頁伺服器。這使我能夠在伺服器上托管靜態網站、動態網站、API 或其他 web 應用程式。

要開始使用 Apache 開發網站或應用，以下步驟進行：

1. **建立網站目錄：** 將網站檔案放在適當的目錄中，預設情況下，Apache 預設的網站根目錄位於 `/var/www/html`。

2. **設定虛擬主機：** 如果打算在同一台伺服器上運行多個網站，可以設定虛擬主機，使每個網站有自己的獨立設定。

3. **設定伺服器：** 根據需求，需要調整 Apache 的設定檔。主要的設定檔位於 `/etc/apache2/apache2.conf` 或 `/etc/apache2/sites-available` 目錄中。

4. **重啟 Apache 服務：** 對設定進行更改後，需要重新啟動 Apache 服務，使更改生效：

   ```
   sudo systemctl restart apache2
   ```

5. **開發與測試：** 在網站目錄中進行網站開發，然後在瀏覽器中測試你的網站。

6. **防火牆設定：** 如果伺服器上有防火牆（例如 UFW），需要確保防火牆允許外部訪問 Apache 的相應端口（預設為 80）。

**虛擬主機設定：**
虛擬主機允許在同一個伺服器上運行多個網站，每個網站有自己獨立的域名或主機名。這是非常有用的，尤其是想要在同一個伺服器上托管多個不同的網站或應用時。

在Apache中，可以通過以下步驟設定虛擬主機：

1. **創建虛擬主機設定檔：** 在`/etc/apache2/sites-available/`目錄中創建一個新的虛擬主機設定檔，例如`my_website.conf`。

2. **設定虛擬主機：** 在該設定檔中，指定網站的域名或主機名、網站目錄、日誌文件位置等等。

   ```
   <VirtualHost *:80>
       ServerName mydomain.com
       DocumentRoot /var/www/my_website
       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>
   ```

   需要將 `mydomain.com` 替換為我要的網站域名，並將 `/var/www/my_website` 替換為想要的網站檔案所在的路徑。

3. **啟用虛擬主機：** 使用 `a2ensite` 命令啟用虛擬主機設定檔。

   ```
   sudo a2ensite my_website
   ```

4. **重啟 Apache 服務：** 確保重新啟動 Apache 服務以應用變更。

   ```
   sudo systemctl restart apache2
   ```

現在，虛擬主機已經設定完成，並可以在瀏覽器中通過該虛擬主機的域名訪問網站。

**其他 Apache 設定：**
Apache 提供了豐富的設定選項，根據需求來進行自定義設定。以下是一些常見的設定選項：

1. **安全性設定：** 可以設定伺服器的安全性，例如禁止目錄瀏覽、限制特定目錄的訪問權限等。

2. **模組啟用：** Apache 支援許多模組，這些模組可以增強伺服器的功能，例如開啟 URL 重寫、啟用 SSL 加密等。

3. **日誌設定：** 可以設定伺服器的存取日誌和錯誤日誌的位置和格式。

4. **性能優化：** 調整 Apache 的設定以提高伺服器的性能，例如處理連線數、併發連線等。

在 `/etc/apache2/` 目錄下找到主要的設定檔，包括 `apache2.conf` 和 `ports.conf`，以及虛擬主機設定檔所在的 `sites-available` 和 `sites-enabled` 目錄。

在修改這些設定檔之前，建議先備份它們，以防止出現意外的錯誤。

**SSL/TLS 加密：** 對於許多網站來說，安全性是至關重要的。
如果打算在網站上處理用戶的敏感資訊，例如登錄帳號、密碼、信用卡號等，建議使用 SSL/TLS 加密來保護數據傳輸。這可以防止數據在網路上被截取或竊聽。

在 Apache 中，可以使用 `mod_ssl` 模組來啟用 SSL/TLS 加密。啟用 SSL/TLS 加密的基本步驟：

1. **安裝 mod_ssl：** 確保 `mod_ssl` 模組已經安裝在系統上。

   ```
   sudo apt install libapache2-mod-ssl
   ```

2. **產生 SSL/TLS 憑證：** SSL/TLS 加密需要有效的數位憑證。可以自己產生自簽名憑證，或者購買來自受信任的證書授權機構（CA）的憑證。

   以下是自簽名憑證的範例產生方式：

   ```
   sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt
   ```

   這將在 `/etc/ssl/private/` 目錄下產生一個私鑰檔案 `apache-selfsigned.key` 和在 `/etc/ssl/certs/` 目錄下產生一個憑證檔案 `apache-selfsigned.crt`。

3. **設定 SSL/TLS 設定檔：** 在 Apache 的虛擬主機設定檔中，新增以下指令來啟用 SSL/TLS 加密。

   ```
   <VirtualHost *:443>
       ServerName mydomain.com
       DocumentRoot /var/www/my_website

       SSLEngine on
       SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt
       SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key

       # 可選：如果有中介憑證 (Intermediate Certificate) 的話，可以加上以下指令
       # SSLCertificateChainFile /path/to/intermediate_certificate.crt

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>
   ```

   將 `mydomain.com` 替換為你的網站域名，並確保 `SSLCertificateFile` 和 `SSLCertificateKeyFile` 指向正確的憑證檔案位置。

4. **重啟 Apache 服務：** 重新啟動 Apache 服務以應用變更。

   ```
   sudo systemctl restart apache2
   ```

現在，這個網站就已經啟用了 SSL/TLS 加密，用戶在瀏覽器中輸入網址後 將透過加密連線進行傳輸。

請注意，自簽名憑證在瀏覽器中可能會顯示安全性警告，因為它沒有受到受信任的證書授權機構簽署。如果你需要真正受信任的 SSL/TLS 憑證，可以購買來自證書授權機構的憑證，這樣瀏覽器就不會顯示警告。
