# RO Survivors 排隊提醒

全服上限 20000 人同時在線，超過就要排隊。這個小工具**不用開網頁**就能一直盯你的名次：
名次進到門檻（預設 100 名）會響三聲＋彈出提醒，按「進入遊戲」才幫你開遊戲視窗準備進入。

[**下載 ro-queue.exe**](https://github.com/lono2023/ro-queue-reminder/releases/latest/download/ro-queue.exe)
（單檔、免安裝、不需要 Python）

**第一次用請看圖文手冊：[MANUAL.md](MANUAL.md)**（含截圖、SmartScreen 提示處理與常見問題）

## 快速開始

1. 雙擊 `ro-queue.exe`（第一次若跳「Windows 已保護你的電腦」→「其他資訊」→「仍要執行」）。
2. 按「**登入／重新登入**」→ 在自動開出的專屬遊戲視窗裡登入一次；
   程式會**自動偵測**登入憑證，開始盯名次（瀏覽器裡本來就登過的話這步可跳）。
3. 名次進到門檻會響聲＋彈提醒 → 按「**進入遊戲**」，隊位保留、直接開視窗。
4. 玩完按「**結束**」關閉程式（會自動讓位）。

## 要注意的

- **遊戲要在程式開的專屬視窗裡玩**：同一帳號在別處登入會被線上踢掉，
  踢掉時程式會彈窗通知，按「登入／重新登入」重登即可。
- **關掉視窗不等於結束排隊**，請按「結束」（會自動讓位）。
- 同一台電腦只能跑一份，重複開啟不會排兩個隊（會彈出「已經在跑了」）。
- 工作管理員看到**兩個** `ro-queue.exe` 是正常的：單檔版有一個啟動程序加一個真正跑的程序。
- **訪客帳號不排隊**：訪客是直接進，沒有名次；要用登入帳號的同一個 token，排到的隊才接得上。
- 憑證讀不到時：先在專屬視窗登入一次再重開；或 F12 Console 輸入
  `localStorage.getItem("ro-survivors-session")`，把整串貼進視窗的 token 欄位。

## 指令模式

```
ro-queue.exe --check             # 查一次網路、憑證、各頻道狀態
ro-queue.exe --no-gui            # 無視窗純文字輪詢
ro-queue.exe --update            # 檢查有沒有新版
ro-queue.exe --install-update    # 自動下載替換，下次啟動生效
ro-queue.exe --token XXX         # 手動指定憑證
ro-queue.exe --threshold 50      # 改提醒門檻
```

設定與記錄檔在 `%APPDATA%\ro-queue\`。

## 給自己要改的人

主程式是單一檔案 `ro_queue.py`，只用 Python 3.8+ 標準函式庫（tkinter／urllib／ctypes／winsound）。
API 協定、登入偵測（CDP）與 TLS 的細節都寫在 `ro_queue.py` 的註解裡。

打包：

```
pip install pyinstaller
python build_exe.py        # 產 dist\ro-queue.exe 與 dist\latest.json
```

## 版本

看 [Releases](../../releases)。啟動時會自動檢查新版，可一鍵更新。
