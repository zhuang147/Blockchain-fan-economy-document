```mermaid
graph TD

U[使用者]

subgraph Frontend[前端 Vue.js]
A1[LoginBox]
A2[TicketsTab]
A3[MyTicketsTab]
A4[SecondHandTab]
A5[LiveFeed]
A6[store.js]
end

subgraph Backend[Backend API]
B1[Express Server]
B2[profiles API]
B3[user-tickets API]
B4[global-tickets API]
B5[feed API]
B6[second-hand API]
end

subgraph Database[Supabase]
C1[profiles]
C2[user_tickets]
C3[global_tickets]
C4[feed_messages]
C5[second_hand_products]
C6[second_hand_orders]
end

subgraph XRPL[XRPL 生態]
D1[Xaman Wallet]
D2[XRPL Ledger]
D3[PTS Token]
D4[NFT Ticket]
end

U --> A1
U --> A2
U --> A3
U --> A4

A6 --> B1

B1 --> B2
B1 --> B3
B1 --> B4
B1 --> B5
B1 --> B6

B2 --> C1
B3 --> C2
B4 --> C3
B5 --> C4
B6 --> C5
B6 --> C6

A2 --> D1
A3 --> D1
A4 --> D1

D1 --> D2
D2 --> D3
D2 --> D4
```
