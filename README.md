# Zero Degree: Agentic e-Procurement Infrastructure

Zero Degree is a high-signal bridge designed to settle **Digital Goods e-Procurement** workflows between institutional ERP systems (SAP S/4HANA) and the Avalanche C-Chain. By utilizing Agentic AI workers and secure Vyper-based smart contracts, Zero Degree automates the procurement lifecycle for digital assets like API licenses, software keys, and specialized data sets.

## 🏗️ System Architecture

The infrastructure operates as a closed-loop settlement engine:

1. **Outbound Trigger (ERP):** SAP triggers a Purchase Requisition (PR) via OData structures to the Zero Degree FastAPI middleware.
2. **On-Chain Settlement:** The system executes a high-precision purchase via the `SnowGate` vault and `VendorShop` contracts, locking USDC for digital delivery.
3. **Agentic Fulfillment:** An autonomous off-chain worker monitors the Avalanche C-Chain for `OrderCreated` events. Upon detection, it generates and encrypts the digital asset (e.g., a 256-bit API key).
4. **ERP Reconciliation:** The fulfillment is detected by a block-scanner, which triggers a secure callback to the ERP listener, delivering the decrypted asset and closing the PR in the ERP system.

## 🚀 Technical Stack

* **Smart Contracts:** Vyper 0.4.0 (Leveraging security-first architecture and gas efficiency).
* **Framework:** ApeWorx (Advanced Python-based Ethereum development).
* **Middleware:** FastAPI / Uvicorn (OData-compliant bridge).
* **Blockchain:** Avalanche C-Chain (Subnet-ready deployment).
* **Agentic Logic:** Custom Python-based block-scanning cursors with persistent state synchronization.

## 🔐 Security & Reliability

* **Atomic Delivery:** On-chain fulfillment ensures that payment is only settled upon successful encryption of the digital payload.
* **Persistent Cursor Management:** The Agent worker maintains a persistent block-height cursor with a 3-block safety buffer to ensure data availability and prevent RPC indexing collisions.
* **OData Compliance:** Middleware adheres to standard SAP S/4HANA OData payloads for seamless enterprise integration.


## 📍 Core Infrastructure (Avalanche Testnet)
* **SnowGate Registry:** `0x48f1CeBF46122a6f7Db6328CFf884bDAFb38c8e9`
* **Digital Vendor Shop:** `0x87254613A0AFa45A78eEF2aF294ba6b50EDb783b`

## 🛠️ Installation & Setup

1. **Clone & Install Dependencies:**
   ```bash
   git clone [https://github.com/neonmercenary/zero-degree-infra](https://github.com/neonmercenary/zero-degree-infra)
   pip install -r requirements.txt
   ape plugins install vyper avalanche

    Configure Environment:
    Create a .env file with your AGENT_PASS and RPC details. Ensure your alt_user account is loaded in Ape. See .env.example for details
    ```

## 🚀 Execution Walkthrough (The Demo)

### Step 1: Start the SAP Emulator (Inbound Listener)

This mimics the ERP system waiting for a delivery receipt.
Bash
```python
python simulate_sap.py
```
### Step 2: Launch the Agentic Monitor

The worker automatically starts scanning blocks for new orders on the VendorShop.
Bash


### Step 3: Trigger the Procurement Cycle

Simulate an outbound PR from SAP. This hits the SnowGate contract, checks session validity, and executes the on-chain purchase.
Bash



**Lead Architect:** Polemarch  
**Repository:** [github.com/neonmercenary/zero-degree-infra](https://github.com/neonmercenary/zero-degree-infra)