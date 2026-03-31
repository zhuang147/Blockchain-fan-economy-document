## 系統架構圖

```mermaid
flowchart LR
    %% 定義顏色與樣式 (安全色碼與圓角)
    classDef uiNode fill:#ffffff,stroke:#007acc,stroke-width:2px,color:#333333,rx:8,ry:8
    classDef midNode fill:#ffffff,stroke:#db7093,stroke-width:2px,color:#333333,rx:8,ry:8
    classDef blockNode fill:#ffffff,stroke:#2e8b57,stroke-width:2px,color:#333333,rx:8,ry:8
    classDef storageNode fill:#ffffff,stroke:#888888,stroke-width:2px,color:#333333,rx:8,ry:8

    %% 第一層：使用者互動層
    subgraph Layer1 ["【 第一層：使用者互動層 User Interface Layer 】(純 Web2 UX)"]
        direction TB
        
        subgraph FanEnd ["📱 粉絲端 App / Web 介面"]
            direction TB
            F1("👤 無密碼登入\n(Email/社群)"):::uiNode
            F2("💳 法幣支付模組\n(信用卡/行動支付)"):::uiNode
            F3("🎟️ 數位票夾 &\n任務足跡面板"):::uiNode
            F4("📡 NFC周邊感應"):::uiNode
        end

        subgraph AdminEnd ["💻 經紀公司 / 主辦方後台"]
            direction TB
            A1("🆕 票券與實體\n周邊發行管理"):::uiNode
            A2("🎯 任務設定\n(線上/線下足跡)"):::uiNode
            A3("📊 二手市場與\n大數據監控面板"):::uiNode
            A4("🎁 長尾福利空投\n(優先購票權/折扣)"):::uiNode
        end
    end

    %% 第二層：中介與業務邏輯層
    subgraph Layer2 ["【 第二層：中介與業務邏輯層 Middleware Layer 】(Web2.5 橋樑)"]
        direction TB
        M1("🔐 託管錢包服務\n(Custodial Wallet)"):::midNode
        M2("💸 法幣入金閘道\n(Fiat Gateway)"):::midNode
        M3("⚙️ 任務與足跡引擎\n(Mission Engine)"):::midNode
        M4("🛡️ 動態防偽驗證模組\n(動態QR / NFC)"):::midNode
    end

    %% 第三層：區塊鏈與合約層
    subgraph Layer3 ["【 第三層：區塊鏈與合約層 Blockchain Layer 】(去中心化信任基礎)"]
        direction TB
        SC1{{"📝 票務智慧合約\n(唯一鑄造 / 受控轉讓限制)"}}:::blockNode
        SC2{{"🏆 粉絲足跡合約\n(實體綁定 / POAP 憑證)"}}:::blockNode
        IPFS[("📦 IPFS 儲存\n(視覺/元數據)")]:::storageNode
    end

    %% 互動關係線
    
    F1 -.-> |"API: 自動生成/授權\n(Custodial Wallet)"| M1
    F2 ====> |"API: 刷卡支付\n(Gateway / 代付 Gas)"| M2
    F3 -.-> |"API: 驗證足跡(Gamefication)"| M3
    F4 -.-> |"API: 硬體加密驗證\n(NFC Verify)"| M4

    M1 -.-> |"Web3.js: 錢包互動\n(RPC通訊)"| SC1
    M2 ====> |"Web3.js: 觸發鑄造 Mint\n(Smart Contract)"| SC1
    M3 ====> |"RPC: 發放/升級憑證\n(NFT/POAP)"| SC2
    M4 ====> |"RPC: 驗證鏈上真偽\n(NFC S-NFT)"| SC2

    A1 ====> |"合約部署\n與發行"| SC1
    A2 ====> |"寫入任務規則\n(Smart Contract)"| SC2
    A4 -.-> |"依據身分憑證\n快照空投"| SC2

    SC1 <--> |"讀取/寫入\n(IPFS API)"| IPFS
    SC2 <--> |"讀取/寫入\n(IPFS API)"| IPFS
```
