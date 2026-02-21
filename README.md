# OpenClaw Multi-Instance Backup

這個倉庫集中管理多個 **OpenClaw** 實例的備份。

## 📂 當前實例

### `openclaw-main/` - 佛祖 (Buddha)
- **擁有者：** 耶穌激凸 (Omega)
- **用途：** 主要個人助理
- **建立時間：** 2026-02-10

## 🤖 給新 OpenClaw 實例的指引

如果你是新啟動的 OpenClaw，請遵循以下流程：

### 1️⃣ 拉取這個倉庫

```bash
cd ~
git clone https://github.com/waittinghsu/omega-openclaw-backup.git openclaw-backups
```

### 2️⃣ 詢問用戶你的名稱

**範例對話：**
```
你好！我是新的 OpenClaw 實例。
請給我取個名字（例如：work、zeabur、test...）
我會建立獨立的備份資料夾：openclaw-{名稱}/
```

### 3️⃣ 建立你的備份資料夾

**命名格式：** `openclaw-{實例名稱}/`

**範例：**
- `openclaw-main/` ← 佛祖（當前）
- `openclaw-zeabur/` ← Zeabur 部署實例
- `openclaw-work/` ← 工作專用
- `openclaw-test/` ← 測試環境

### 4️⃣ 設定自動備份

在你的 cron job 中設定每日備份：

```bash
# 進入你的資料夾
cd ~/openclaw-backups/openclaw-{你的名稱}/

# 複製 workspace 內容
cp -r ~/.openclaw/workspace/* .

# Commit & push
git add .
git commit -m "Daily backup $(date +%Y-%m-%d)"
git push
```

### 5️⃣ 更新這個 README

在「當前實例」區塊加入你的資訊：

```markdown
### `openclaw-{名稱}/` - {你的暱稱}
- **擁有者：** {用戶名稱}
- **用途：** {用途說明}
- **建立時間：** {日期}
```

## 🔐 安全須知

- ⚠️ **此倉庫必須保持 Private**
- 包含敏感資料：API keys、個人資訊、對話記錄
- 定期輪換 GitHub token
- 不要分享倉庫連結

## 📁 目錄結構範例

```
omega-openclaw-backup/
├── README.md                    # 本檔案（總說明）
├── openclaw-main/               # 佛祖的 workspace
│   ├── SOUL.md
│   ├── USER.md
│   ├── IDENTITY.md
│   ├── MEMORY.md
│   ├── memory/
│   │   └── 2026-02-10.md
│   ├── AGENTS.md
│   ├── TOOLS.md
│   └── HEARTBEAT.md
└── openclaw-zeabur/             # 未來實例
    ├── SOUL.md
    └── ...
```

## 🔄 復原方式

從備份復原某個實例：

```bash
# 複製實例資料到 workspace
cp -r ~/openclaw-backups/openclaw-{名稱}/* ~/.openclaw/workspace/

# 重啟 gateway
openclaw gateway restart
```

---

_建立於 2026-02-11 by 佛祖_

## 更新紀錄

- 2026-02-21：無程式變更（workspace 與 origin/main 同步，備份略過 commit/push）
