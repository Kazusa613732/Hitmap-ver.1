# Kioptrix_Level_1
  - https://www.vulnhub.com/entry/kioptrix-level-1-1,22/
## 掃描
  - 透過 netdiscover 對整個網段進行搜尋，找出靶機
    ```sh
    netdiscover -r 192.168.117.0
    ```
  - 掃描出 port -> nmap
    ```sh
    nmap -A -sV -T4 192.168.117.133
    # -A 執行進階掃描，包括操作系統偵測、服務版本偵測、腳本掃描以及路由追蹤
    # -sV 開啟服務版本偵測功能
    # -T4 指定掃描的時間模板。T4 表示快速模式，會加速掃描過程，但可能對網路造成更大的流量壓力
    ```
    - ports
      - 22,80,111,139,443,1024
    ![nmap掃描port](https://github.com/Kazusa613732/Hitmap-ver.1/blob/main/Vulnhub_Writeup/Vulnhub_img/kioptrix-level-1-1_nmap.png)

  - nikto 掃描（容易產生大量請求，實際環境容易被擋）
    ```sh
    nikto -h ip
    ```
## 利用版本資訊
  - 掃描後，發現使用 mod_ssl/2.8.4 ，去查一下有沒有漏洞或PoC（不只這個，其他像是 Samba 之類的也可以去查看看）
  - mod_ssl/2.8.4 PoC
  - Github :　https://github.com/heltonWernik/OpenLuck
  - 依照步驟進行獲取目標機器的root權限
