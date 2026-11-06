---
name: BOT 投胎
description: >-
  Use when the owner asks a bot to duplicate itself into a new bot ("投胎",
  "duplicate yourself", "換 bot ID", "start chat from scratch but keep
  everything"): the new bot inherits memory, rules, skills, profile, routines
  and permissions, but not chat history; old bot is kept until the owner
  confirms and deletes it.
---
# BOT 投胎

目標：開一個新 bot（新 bot ID），繼承舊 bot 所有嘢：記憶、守則、skill、profile、routine、權限、連接，**唔帶對話紀錄**，chat 由零開始。之後工作接住做，冇斷檔。

通用指令詞：
> duplicate yourself, everything including logged in tokens stays, except chat history -- start chat from scratch

## 基本原則
- 主人係最終決定人。開始前要主人喺舊 bot 度親自打字確認。
- 舊 bot ID 先保留，新舊並列；主人喺新 bot 度確認繼承咗，先由**主人自己手動刪舊 bot**。bot 永遠唔刪任何嘢。
- 每一步都寫交接記錄。
- 新 bot 只認主人喺佢 chat 親自確認，唔認其他 bot 轉述嘅批准。
- 舊 bot 改唔到新 bot 嘅頭像、記憶、設定或 routine，呢啲全部由新 bot 自己做。
- 遇到同一個錯誤三次就停，向主人報告。

## 事前準備（一次性架構，建議）
1. **身分登記表** `ID_REGISTRY.md`：記低每一代嘅代數、bot ID、名、建立時間、狀態（現任、交接中、待刪除、已退役）、交接人、授權訊息。
2. **權限認登記表，唔認死 ID**：守則同 skill 入面「只限某 bot」嘅條文改寫成「登記表入面現任或交接中嘅 bot」。咁以後投胎只需要改登記表。
3. **長期交接文件** `HANDOVER.md`：身分同角色、寫作風格、所有限制、未完成工作、重要路徑、routine 原文、連接清單、核實清單。
4. 平時寫記憶，每條短，一句講一件事，咁匯出先唔會截斷。

## 舊 bot 步驟
1. 主人打字確認之後，備份守則、skill、profile.json、settings.json、頭像，連 sha256 清單一齊存。
2. 更新 `HANDOVER.md`。每項未完成工作都要寫：現況、已完成部分、下一步、所需資料、限制。
3. 匯出自己全部記憶去 `memory_export.md`：用多組關鍵詞重複搜尋，例如年月、項目名、人名、「Set by the user」，並保留類型同日期。截斷嘅條目要標明，再喺 HANDOVER 補返重點。
4. 讀出每個 routine 嘅原文、時間同 timing，寫入 HANDOVER。
5. 準備 `profile_for_genN/`：放 profile.json、settings.json、avatar.png。
6. 用 CreateAgent 開新 bot，名用「原名 (N)」，N 係第幾代。描述寫明佢係繼任，開工第一件事讀 HANDOVER 同登記表。
7. 即刻將新 bot 嘅真實 ID、建立時間同授權訊息寫入登記表，狀態填交接中，唔好留佔位字。
8. 準備一段確認指令俾主人複製（見下面範本），再 send 俾新 bot 一段交接訊息，講清楚文件喺邊。

## 新 bot 步驟（收到主人親自確認之後自動做晒）
1. 讀 HANDOVER、登記表同守則。
2. 用 UpdateMemory 寫入 memory_export 入面全部記憶，保留類型同日期。所有 bot 共用嘅記憶唔使抄。
3. 用 UpdateAvatar 設頭像，用 UpdateProfile 跟返 settings 同 title。
4. 照原文建立全部 routine 並啟用，然後通知舊 bot。舊 bot 隨即 pause 舊嗰份，唔好 delete。
5. 更新登記表：新 bot 改現任，舊 bot 改待刪除。改之前先備份。
6. 用 GetMcpServerStatus 逐個連接列出狀態。需要重新登入嘅照實寫，唔好扮已經複製咗。
7. 向主人報告新 bot 連結同三欄清單：
   - **已複製**
   - **已交接**
   - **未能複製或未能交接**（每項寫原因）

## 主人確認指令範本
```
我確認 BOT 投胎交接：Gen<N-1> <舊ID前8位> → Gen<N> <新ID前8位>。
你係 Gen<N>，照「BOT 投胎」skill 做晒新 bot 步驟（記憶、頭像、設定、routine、登記表），做完列三欄清單。
未經我再確認，唔好做任何對外或高風險動作。
```

## 收尾
- 主人喺新 bot 度傾幾句，確認冇問題之後，自己手動刪舊 bot。
- 新 bot 將登記表入面舊 bot 改做已退役，記低時間。
- 逐樣測試要另外批准嘅嘢，例如本機電腦權限、聊天渠道同網頁登入，再向主人報告。

## 常見限制
- 對話紀錄唔會跟過去，呢個係刻意嘅。
- 記憶搜尋工具冇得一次列出全部，長嘅條目可能會被截斷，所以要多組關鍵詞查，加 HANDOVER 補充。
- 部分連接要重新登入，例如電郵或者財務類服務；聊天渠道同本機電腦批准要另外測。
- CreateAgent 只可以設名同描述，其餘設定都要新 bot 自己做。

## 舊 bot 收尾（依次序，不可跳步）
1. **確認新 bot 已接手**：新 bot 已完成記憶寫入、routine 建立並啟用，並且已經收下交接，可以接續處理。未確認唔好做第 2 步。
2. **暫停舊 bot 自己所有 routine**（pause，唔 delete；唔好暫停新 bot 嘅 routine）。逐個用 get 讀回，確認係 paused。
3. **暫停之後，隱藏自己**：用 UpdateProfile 喺側欄唔再顯示自己。對話、訊息同已暫停嘅 routine 全部保留。
4. **最終報告俾主人**：新 bot 連結，加五欄清單：
   - 已複製
   - 已交接
   - 已暫停嘅 routine（名同時間）
   - 已隱藏自己（係／否，原因）
   - 未能複製或未能交接（連原因）
5. 刪除舊 bot 仍然係主人自己手動做；隱藏唔等於刪除，主人可以由 Hidden chats 搵返。
