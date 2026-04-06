## Use Case Diagram
掃描周邊防偽驗證應該是NFT不是智能合約的工作  
打卡領取數位足跡是任務卡領取福利，跟智能合約也無關
```mermaid
flowchart LR
    %% Actors
    Fan(["🧑‍🎤 粉絲"])
    Admin(["🏢 官方管理者"])
    Pay(["💳 金流服務"])
    Blockchain(["⛓️ 區塊鏈服務"])

    %% System Boundary
    subgraph System [Web2.5 粉絲互動生態系]
        direction LR

        %% 主流程
        UC0([參與演唱會完整流程])

        subgraph Ticket [票務系統]
            UC1([完成身份驗證（防黃牛）])
            UC2([購買門票（信用卡支付）])
            UC3([轉讓門票給朋友])
            UC4([透過官方退票池轉售])
        end

        subgraph Merch [周邊系統]
            UC5([驗證周邊真偽])
            UC6([轉讓周邊所有權])
        end

        subgraph FanSystem [粉絲長尾系統]
            UC7([完成任務取得數位足跡])
            UC8([兌換粉絲專屬福利])
        end

        subgraph AdminSystem [後台管理]
            UC9([設定任務與活動])
            UC10([管理票務與退票池])
        end
    end

    %% 主流程關聯
    Fan --- UC0
    UC0 --> UC2
    UC0 --> UC7
    UC0 --> UC8

    %% 粉絲互動
    Fan --- UC1
    Fan --- UC2
    Fan --- UC3
    Fan --- UC4
    Fan --- UC5
    Fan --- UC6
    Fan --- UC7
    Fan --- UC8

    %% 官方互動
    Admin --- UC9
    Admin --- UC10
    Admin --- UC7
    Admin --- UC8

    %% 外部系統（Web2.5 重點🔥）
    UC2 --- Pay
    UC2 --- Blockchain
    UC3 --- Blockchain
    UC4 --- Blockchain
    UC5 --- Blockchain
    UC6 --- Blockchain
    UC7 --- Blockchain
```
---
## 循環圖
