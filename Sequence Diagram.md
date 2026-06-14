
sequenceDiagram
    participant User as 粉絲使用者
    participant Frontend as Vue.js 前端
    participant Backend as Express API
    participant DB as Supabase
    participant Wallet as Xaman Wallet
    participant XRPL as XRPL Ledger

    User->>Frontend: 瀏覽活動與票券資訊
    Frontend->>Backend: 請求票券資料
    Backend->>DB: 查詢 global_tickets
    DB-->>Backend: 回傳票券資訊
    Backend-->>Frontend: 顯示票券資訊

    User->>Frontend: 選擇票券並確認購買
    Frontend->>Wallet: 發起付款簽署請求
    Wallet->>User: 顯示交易確認畫面
    User->>Wallet: 確認付款

    Wallet->>XRPL: 提交 PTS Token 交易
    XRPL-->>Wallet: 回傳交易結果

    Wallet-->>Frontend: 回傳交易成功資訊
    Frontend->>Backend: 建立購票紀錄

    Backend->>DB: 更新 global_tickets 庫存
    Backend->>DB: 新增 user_tickets 紀錄

    DB-->>Backend: 更新完成
    Backend-->>Frontend: 回傳購票成功訊息

    Frontend-->>User: 顯示購票結果與我的票券
