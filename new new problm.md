```mermaid
%%{init: {"flowchart": {"nodeSpacing": 40, "rankSpacing": 160, "padding": 40}}}%%
flowchart LR
    %% 定義顏色與樣式
    classDef uiNode fill:#ffffff,stroke:#007acc,stroke-width:2px,color:#333333,rx:8,ry:8
    classDef midNode fill:#ffffff,stroke:#db7093,stroke-width:2px,color:#333333,rx:8,ry:8
    classDef blockNode fill:#ffffff,stroke:#2e8b57,stroke-width:2px,color:#333333,rx:8,ry:8
    classDef storageNode fill:#ffffff,stroke:#888888,stroke-width:2px,color:#333333,rx:8,ry:8

    %% 第一層：前端展示層 (Frontend Layer)
    subgraph Layer1 ["【 第一層：前端展示層 】(React Native / Web)"]
        direction TB
        
        subgraph FanEnd ["📱 粉絲端 (React Native App)"]
            direction TB
            F1("👤 無密碼登入\n(Email/社群)"):::uiNode
            F2("💳 法幣支付模組\n(信用卡/行動支付)"):::uiNode
            F3("🎟️ 數位票夾 &\n任務足跡面板"):::uiNode
            F4("📡 NFC周邊感應"):::uiNode
        end

        subgraph AdminEnd ["💻 主辦方後台 (Web 管理端)"]
            direction TB
            A1("🆕 票券與實體\n周邊發行管理"):::uiNode
            A2("🎯 任務設定\n(線上/線下足跡)"):::uiNode
            A3("📊 二手市場與\n大數據監控面板"):::uiNode
            A4("🎁 長尾福利空投\n(優先購票權/折扣)"):::uiNode
        end
    end

    %% 第二層：後端邏輯與資料層 (Backend & Data Layer)
    subgraph Layer2 ["【 第二層：後端邏輯層 】(Node.js Express / Web 2.5)"]
        direction TB
        M1("🔐 託管錢包服務\n(Cloud KMS 技術)"):::midNode
        M2("💸 法幣入金閘道\n(Fiat Gateway)"):::midNode
        M3("⚙️ 任務與足跡引擎\n(Business Logic)"):::midNode
        DB[("🗄️ 系統資料庫\n(PostgreSQL)")]:::storageNode
    end

    %% 第三層：區塊鏈協議層 (Blockchain Layer)
    subgraph Layer3 ["【 第三層：區塊鏈協議層 】(Polygon Layer 2)"]
        direction TB
        SC1{{"📝 票務智慧合約\n(Solidity / NFT 鑄造)"}}:::blockNode
        SC2{{"🏆 粉絲足跡合約\n(S-NFT / POAP 憑證)"}}:::blockNode
        IPFS[("📦 IPFS 儲存\n(去中心化存儲)")]:::storageNode
    end

    %% 互動關係線
    
    F1 -.-> |"API"| M1
    F2 ====> |"API"| M2
    F3 -.-> |"API"| M3
    F4 -.-> |"NFC Verify"| SC2

    %% 後端與資料庫連線
    M3 ====> |"寫入帳務/行為"| DB
    A3 -.-> |"撈取大數據分析"| DB

    %% 區塊鏈連線
    M1 -.-> |"RPC: 錢包互動"| SC1
    M2 ====> |"RPC: 觸發鑄造"| SC1
    M3 ====> |"RPC: 發放憑證"| SC2

    A1 ====> |"合約部署"| SC1
    A2 ====> |"設定任務"| SC2
    A4 -.-> |"憑證快照"| SC2

    %% 儲存連線
    SC1 <--> |"Metadata"| IPFS
    SC2 <--> |"Metadata"| IPFS
```
