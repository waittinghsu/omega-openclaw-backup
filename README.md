# OpenClaw Workspace Backup

這是 **OpenClaw** 的 workspace 備份倉庫。

## 🤖 當前實例

- **名稱：** 佛祖 (Buddha)
- **實例 ID：** `openclaw-main`
- **擁有者：** 耶穌激凸 (Omega)
- **建立時間：** 2026-02-10

## 📂 備份結構規則

如果你是新的 OpenClaw 實例，請遵循以下規則：

### 1️⃣ 檢查現有倉庫

在用戶的 GitHub 帳號下搜尋：
- `openclaw-*` 或 `*-openclaw-backup`

### 2️⃣ 建立你的倉庫

**命名格式：**
```
{用戶名稱}-openclaw-{實例名稱}
```

**範例：**
- `omega-openclaw-main` ← 當前（佛祖）
- `omega-openclaw-work` ← 工作用實例
- `omega-openclaw-test` ← 測試實例

### 3️⃣ 本機備份結構

手動備份存放位置：
```
~/backups/
├── openclaw-main/      # 對應倉庫名稱
│   └── manual/
├── openclaw-work/
│   └── manual/
└── openclaw-test/
    └── manual/
```

### 4️⃣ 初始化流程

**首次啟動時：**

1. **詢問用戶：**
   ```
   你希望給這個 OpenClaw 實例取什麼名字？
   （例如：work、personal、test...）
   ```

2. **確認倉庫：**
   ```
   我會建立備份倉庫：{用戶名稱}-openclaw-{實例名稱}
   GitHub 倉庫需設為 Private。確認建立？
   ```

3. **設定備份：**
   - Git 自動備份（每晚 23:59）
   - 本機備份資料夾：`~/backups/openclaw-{實例名稱}/`

## 🔐 安全須知

- ⚠️ **倉庫必須設為 Private**
- 包含敏感資料：API keys、個人資訊、配置檔
- 定期輪換 GitHub token
- 不要在公開場合分享倉庫連結

## 📝 內容說明

此倉庫包含：
- `SOUL.md` - 個性與原則
- `USER.md` - 用戶資訊
- `IDENTITY.md` - 實例身份
- `MEMORY.md` - 長期記憶（僅 main session）
- `memory/` - 每日記憶筆記
- `AGENTS.md` - 工作流程
- `TOOLS.md` - 工具配置
- `HEARTBEAT.md` - 定期檢查任務

## 🔄 復原方式

如需在新機器復原此實例：

```bash
# 安裝 OpenClaw
pnpm install -g openclaw

# Clone workspace
git clone https://github.com/{用戶}/omega-openclaw-main.git ~/.openclaw/workspace

# 復原完整配置（需另外備份 openclaw.json）
# 重啟 gateway
openclaw gateway restart
```

---

_由 佛祖 建立於 2026-02-10_
