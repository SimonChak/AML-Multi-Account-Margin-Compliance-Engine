# 金融反洗錢與多帳號保證金合規引擎
FinTech AML & Multi-Account Margin Compliance Engine 
 
## 專案背景與概述 Project Overview
在金融衍生品交易平台中，為了防止洗黑錢（AML）行為，通常會有一項合規規則：「當客戶的交易帳號入金後，必須達到一定的交易量或維持一定的保證金比例」。

In financial trading platforms, compliance rules often require clients to achieve a certain trading volume or margin usage after depositing funds to prevent Anti-Money Laundering (AML) risks. 

然而，當單一客戶擁有個多個交易帳號並進行內部轉帳（`Transfer`）時，計算有效入金與實際保證金合規性會變得極為複雜。

However, when a single client owns multiple trading accounts and performs internal transfers ('Transfer'), calculating effective deposits and actual margin compliance becomes extremely complex.

本專案提供了一個專為資料倉儲（Data Warehouse）設計的自動化 T-SQL 分析引擎，能夠聚合客戶的所有關聯帳號網絡、追蹤多渠道資金流入，並即時評估合規性。

This project provides an automated T-SQL analytics engine designed for Data Warehouses to aggregate a client's entire connected account network, track fund inflows across multiple channels, and evaluate regulatory compliance in real-time.

---

## 核心功能與技術亮點 Key Features & Technical Highlights

1. **Multi-Account Graph Traversal (Connected Group Mapping):**
   - Automatically traces and maps first-tier and extended connected accounts (`Connected_Group`) through internal transfer transaction patterns.
   - **多帳號圖論式關聯（關聯群組對應）：** 透過內部轉帳交易模式，自動追蹤並對應第一層與延伸關聯帳號（`Connected_Group`）。

2. **Dynamic Fund Reset & Withdrawal Tracking:**
   - Evaluates withdrawal reset points (`max_reset_deal_no`) and excludes reversed adjustments (`Adjustment`) to ensure accurate calculation windows.
   - **動態資金重置與出金追蹤：** 評估出金重置點（`max_reset_deal_no`）並排除被撤銷的調整記錄（`Adjustment`），以確保計算時間視窗的準確性。

3. **Multi-Channel Deposit Breakdown:**
   - Categorizes and reconciles funding sources across Fiat gateways, Wire transfers, Cryptocurrencies, Commission transfers, and previous day balances.
   - **多渠道入金細目拆解：** 分類並核對來自法幣支付閘道、電匯、加密貨幣、佣金轉入及昨日結餘的資金來源。

4. **Symbol-Level Margin Conversion:**
   - Normalizes trades across diverse asset classes (Forex, Precious Metals, Indices, Crypto, and US Stocks) into standardized USD margin values based on dynamic exchange rates and instrument specifications.
   - **商品級別保證金換算：** 根據動態匯率與合約規格，將涵蓋多種資產類別（外匯、貴金屬、指數、加密貨幣與美股）的交易標準化為統一的 USD 保證金價值。

5. **Automated Compliance Auditing:**
   - Compares total group effective deposits against actual combined margin usage (threshold) to output a definitive audit status (`Audit_Status`) and shortfall amount.
   - **自動化合規審計：** 比較總群組有效入金與實際綜合保證金使用量（門檻），輸出確切的審計狀態（`Audit_Status`）與資金缺口金額。

---

## Sample Output Preview (De-identified) 範例輸出預覽（已去識別化）
<img width="1501" height="808" alt="image" src="https://github.com/user-attachments/assets/77feeae4-2595-437d-ad38-c31302c60016" />

*(Note: Sensitive client codes and financial data have been blurred for privacy)*
*(註：為保護隱私，敏感的客戶代號與財務數據已進行模糊處理)*

- **Audit Overview:** Shows consolidated group deposit, margin threshold, actual margin usage percentage, and compliance status.
  - **審計總覽：** 顯示群組合併入金、保證金門檻、實際保證金使用百分比以及合規狀態。
- **Channel Analysis:** Breaks down fiat, crypto, and wire flows per sub-account.
  - **渠道分析：** 細分各子帳號的法幣、加密貨幣與電匯金流。
- **Trade Details:** Maps individual ticket numbers and calculated margin requirements.
  - **交易明細：** 對應個別交易單號（Ticket No）與計算出的保證金需求。

---

## Tech Stack 技術堆疊
- **Database:** Microsoft SQL Server (T-SQL)
  - **資料庫：** Microsoft SQL Server (T-SQL)
- **Concepts:** Data Warehousing, Anti-Money Laundering (AML), Risk Analytics, Complex Joins & CTEs, Financial Data Engineering.
  - **核心概念：** 資料倉儲、反洗錢（AML）、風險分析、複雜關聯與 CTEs、金融資料工程。
