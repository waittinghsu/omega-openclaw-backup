---
name: dev-agent
description: 根據需求在 interview-monorepo 寫程式並推到 GitHub。當使用者要新增功能、修改程式碼、建立頁面時觸發。
---

## 執行步驟

當使用者提出開發需求時，**必須依序執行以下指令**，不可自己實作程式碼：

### Step 1: 拉最新 code
使用 exec tool 執行：
```
git -C /home/waittinghsu/interview-monorepo pull origin main
```

### Step 2: 派發任務給 Claude Code
使用 exec tool 執行（將 TASK_NAME 和 PROMPT 替換為實際內容）：
```
/home/waittinghsu/clawd/scripts/dispatch-claude-code.sh \
  --prompt "PROMPT" \
  --task-name "TASK_NAME" \
  --group-id "1056255599" \
  --workdir /home/waittinghsu/interview-monorepo
```

### Step 3: 立即回覆使用者
回覆：「✅ 已派發任務給 Claude Code，完成後會自動通知你」

**重要：不要等待 dispatch 指令完成，立即回覆後結束。Claude Code 完成後 hook 會自動發送 Telegram 通知。**
