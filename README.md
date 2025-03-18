# Hitmap-ver.1

## 掃描

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
  - etc..
  - 感覺奇怪的都去看

## Injection
### CRLF injection
  - [筆記](https://www.notion.so/CRLF-Injection-1b9997876c1380e4bc7cccad27ecd62f?pvs=4)

