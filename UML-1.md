## 高階總覽圖
```mermaid
flowchart LR
    %% 參與者
    Fan(["🧑‍🎤 粉絲 (User)"])
    Admin(["🏢 官方管理者"])
    Blockchain(["⛓️ 區塊鏈基礎設施"])
    Pay(["💳 第三方金流 API"])

    %% 系統核心模組 (以用例形式呈現模組)
    subgraph SystemBoundary [Web2.5 粉絲互動生態系 App 總覽]
        direction TB
        M1([智慧票務與退讓票模組])
        M2([實體周邊 NFT 防偽模組])
        M3([粉絲價值長尾模組])
        M4([後台管理模組])
    end

    %% 主動連線 (實線)
    Fan --- M1 & M2 & M3
    Admin --- M1 & M3 & M4

    %% 被動依賴連線 (虛線)
    M1 -.- Pay & Blockchain
    M2 -.- Blockchain
    M3 -.- Blockchain
    
    %% 樣式
    classDef actor fill:#f9f9f9,stroke:#333,stroke-width:2px;
    classDef module fill:#e3f2fd,stroke:#1565c0,stroke-width:2px;
    class Fan,Admin,Blockchain,Pay actor;
    class M1,M2,M3,M4 module;
```
---

### A. 智慧票務與退讓票模組
這裡展示了粉絲與金流、區塊鏈的清晰互動，管理者僅介入 KYC 審核。
```mermaid
flowchart LR
    Fan(["🧑‍🎤 粉絲"])
    Admin(["🏢 官方管理者"])
    Blockchain(["⛓️ 區塊鏈基礎設施"])
    Pay(["💳 第三方金流"])

    subgraph TicketSystem [智慧票務與退讓票模組]
        direction TB
        UC1([實名身分驗證 KYC])
        UC2([購買門票與付款])
        UC3([分配同行者票券])
        UC4([申請官方退讓票])
    end

    Fan --- UC1 & UC2 & UC3 & UC4
    Admin --- UC1
    
    UC2 -.- Pay
    UC2 -.- Blockchain
    UC3 -.- Blockchain
    UC4 -.- Blockchain

    classDef actor fill:#f9f9f9,stroke:#333,stroke-width:2px;
    classDef usecase fill:#fad7d4,stroke:#d32f2f,stroke-width:1px;
    class Fan,Admin,Blockchain,Pay actor;
    class UC1,UC2,UC3,UC4 usecase;
```
---

### B. 實體周邊 NFT 防偽模組
極度單純的驗證與轉移流程。
```mermaid
flowchart LR
    Fan(["🧑‍🎤 粉絲"])
    Blockchain(["⛓️ 區塊鏈基礎設施"])

    subgraph MerchSystem [實體周邊 NFT 防偽模組]
        direction TB
        UC5([掃描 NFC 驗證 NFT 真偽])
        UC6([移轉 NFT 所有權])
    end

    Fan --- UC5 & UC6
    UC5 -.- Blockchain
    UC6 -.- Blockchain

    classDef actor fill:#f9f9f9,stroke:#333,stroke-width:2px;
    classDef usecase fill:#fad7d4,stroke:#d32f2f,stroke-width:1px;
    class Fan,Blockchain actor;
    class UC5,UC6 usecase;
```
---

### C. 粉絲價值長尾模組
明確區分出「官方設定規則」與「粉絲執行任務」的雙向互動。
```mermaid
flowchart LR
    Fan(["🧑‍🎤 粉絲"])
    Admin(["🏢 官方管理者"])
    Blockchain(["⛓️ 區塊鏈基礎設施"])

    subgraph LongTailSystem [粉絲價值長尾模組]
        direction TB
        UC7([任務打卡領取數位足跡])
        UC8([憑證兌換專屬長尾福利])
    end

    Fan --- UC7 & UC8
    Admin --- UC7 & UC8
    
    UC7 -.- Blockchain

    classDef actor fill:#f9f9f9,stroke:#333,stroke-width:2px;
    classDef usecase fill:#fad7d4,stroke:#d32f2f,stroke-width:1px;
    class Fan,Admin,Blockchain actor;
    class UC7,UC8 usecase;
```
---

### D. 後台管理模組
專屬於官方管理者的獨立作業區塊。
```mermaid
flowchart LR
    Admin(["🏢 官方管理者"])

    subgraph AdminSystem [後台管理模組]
        direction TB
        UC9([發布活動與設定任務])
        UC10([數據監控與退票池管理])
    end

    Admin --- UC9 & UC10

    classDef actor fill:#f9f9f9,stroke:#333,stroke-width:2px;
    classDef usecase fill:#fad7d4,stroke:#d32f2f,stroke-width:1px;
    class Admin actor;
    class UC9,UC10 usecase;
```
