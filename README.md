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

## 目錄爆破

### 工具
  - dirsearch
  - Gobuster
### 不該出現的頁面
  - .env
  - phpinfo
  - .git
  - upload.php（進去看有沒有可以try的點）
  - login.php（進去看有沒有可以try的點）
  - etc..
