# 併武 V18.78 dashboard FullMaster

台股量化技術分析儀表板（Streamlit）。

---

## 🚀 部署到免費的 Streamlit Community Cloud（拿到永久網址）

### 需要準備
- 一個 GitHub 帳號（免費）：https://github.com
- 一個 Streamlit Community Cloud 帳號（免費，用 GitHub 登入）：https://share.streamlit.io

### 步驟

#### 1. 把這個資料夾傳到 GitHub

**方法 A：用 GitHub 網頁（最簡單，不用裝 git）**
1. 到 https://github.com/new 建一個新的 repository，例如取名 `bw-dashboard`，設為 **Public**（免費版部署需要 Public，或 Private 也可但有限制），不要勾 "Add a README"。
2. 進到剛建好的空 repo 頁面，點 **「uploading an existing file」**。
3. 把以下檔案／資料夾整個拖進去上傳：
   - `bw_ultimate_dashboard_v18.78_dashboard_FullMaster.py`
   - `requirements.txt`
   - `.gitignore`
   - `.streamlit/config.toml`
   - `README.md`
   - （`latest_tdcc.csv` 有的話可一起上傳，沒有也沒關係）
   - ⚠️ **不要**上傳 `.streamlit/secrets.toml`（金鑰檔）
4. 按 **Commit changes**。

**方法 B：用 git 指令**
```bash
cd "C:\Users\user\Desktop\股票技術分析"
git init
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin https://github.com/你的帳號/bw-dashboard.git
git push -u origin main
```

#### 2. 在 Streamlit Cloud 開新 App
1. 到 https://share.streamlit.io ，用 GitHub 登入。
2. 點 **「Create app」→「Deploy a public app from GitHub」**。
3. 填寫：
   - **Repository**：`你的帳號/bw-dashboard`
   - **Branch**：`main`
   - **Main file path**：`bw_ultimate_dashboard_v18.78_dashboard_FullMaster.py`
   - **App URL**：自訂一個名稱，例如 `bw-dashboard` → 網址就是 `https://bw-dashboard.streamlit.app`
4. （可選）點 **「Advanced settings」**：
   - **Python version** 選 `3.11` 或 `3.12`
   - **Secrets**：如果要自動帶入永豐金 API 金鑰，貼上 `.streamlit/secrets.toml.example` 裡的格式並填真值。
     （不填也能跑，程式會走 Yahoo 資料模式。）
5. 按 **Deploy**，等 2–5 分鐘安裝套件。完成後就得到一個**永久有效的網址**。

之後每次你把新的 commit push 到 GitHub 的 `main` 分支，Streamlit Cloud 會自動重新部署。

---

## ⚠️ 部署注意事項

| 項目 | 說明 |
|---|---|
| **shioaji（永豐金 API）** | 預設**不安裝**。它在雲端常常編譯失敗，會讓整個 App 起不來。你的程式已用 `try/except ImportError` 包住，沒有它會自動改用 Yahoo Finance 抓資料。部署成功後若真的要用，再去 `requirements.txt` 取消註解 `shioaji>=1.2.0` 重新部署。 |
| **API 金鑰** | 絕對不要寫死在 `.py` 裡或上傳 GitHub。用側邊欄輸入，或用 Cloud 後台的 **Secrets**。 |
| **免費版限制** | 資源約 1 CPU / 2.7GB RAM；App 連續無人使用會「休眠」，有人開網址時會在幾十秒內自動喚醒（網址永久不變）。 |
| **檔案系統是暫時的** | `latest_tdcc.csv` 這類執行期間寫入的檔案不會永久保存，重啟就消失。要持久化請改用外部資料庫或 GitHub 內的檔案。 |
| **Yahoo 抓資料** | 雲端 IP 有時會被 Yahoo 限流，偶爾某些個股抓不到屬正常，程式有 fallback。 |

## 本機測試
```bash
pip install -r requirements.txt
streamlit run bw_ultimate_dashboard_v18.78_dashboard_FullMaster.py
```
