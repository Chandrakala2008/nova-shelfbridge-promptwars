# NOVA ShelfBridge — Zero-Friction Merchant Inventory Sync & Smart-Substitution

**Product Focus:** Active Stockout Prevention & Local Network Continuity Bridge  
**Challenge Track:** PROMPTWARS BUSINESS RESCUE CHALLENGE for NOVA CART  
**Status:** Functional Hackathon MVP (100% Ready to Demo)

---

## 1. Executive Problem & Solution

* **The Problem:** 35% of NOVA CART cancellations are caused by product unavailability because 39% of partner stores find manual inventory maintenance too burdensome and update catalogs only once every 1–3 days.
* **The Solution:** A zero-friction voice/text catalog synchronizer for local merchants that targets the inventory-effort problem reported by 39% of stores and provides an availability bridge across local partner stores.

---

## 2. Files Created

| File | Description |
|---|---|
| `index.html` | Complete standalone single-page application with side-by-side Merchant Console, Customer Storefront, Smart-Bridge substitution cards, and Business Impact Telemetry. |
| `server.py` | Lightweight Python standard-library HTTP server that serves the prototype at `http://localhost:8000` with clean logging and auto-browser launch. |
| `run.bat` | One-click Windows launch script. |
| `README.md` | Comprehensive system documentation, demo runbook, and verification report. |

---

## 3. How to Run the Application

### Option A: Using the 1-Click Batch Script (Windows)
Double-click `run.bat` in this folder. It launches the local server and opens your default browser at:
```
http://localhost:8000
```

### Option B: Using Python via Terminal
Run the following command from this directory:
```bash
python server.py
```
Or use Python's built-in module directly:
```bash
python -m http.server 8000
```
Then visit `http://localhost:8000` in Google Chrome, Microsoft Edge, or Firefox.

### Option C: Direct File Opening
You can also directly double-click `index.html` in File Explorer. (Note: For Web Speech API microphone access, modern browsers prefer `http://localhost:8000`).

---

## 4. Functional vs. Simulated Matrix

### FUNCTIONAL (Real working code in the MVP)
* ✅ **Merchant Natural Language Input:** Free-text typing in English/Hinglish or browser voice recognition (Web Speech API).
* ✅ **AI Entity & Intent Extraction:** Real-time extraction of canonical SKU IDs, stock actions (`OUT_OF_STOCK`, `IN_STOCK`, `LOW_STOCK`), and quantity.
* ✅ **Dual AI Architecture:** Works with live Google Gemini Flash API if an API key is provided, or uses a deterministic, highly intelligent Local NLP Fallback with zero setup.
* ✅ **Ambiguity Detection & Disambiguation UI:** If an ambiguous input like *"Amul doodh nahi hai"* is submitted, the system halts automatic mutation and presents a 1-tap choice between candidate variants (`Amul Gold` vs `Amul Taaza`).
* ✅ **Real-Time Customer Catalog Sync:** Deactivates depleted items in the customer app instantly without full-page reloads.
* ✅ **Smart Bridge Recommendations:**
  * Option 1: Recommends in-stock substitute variants from the *same* store (e.g., Amul Taaza for Amul Gold).
  * Option 2: Recommends identical in-stock items from a *nearby NOVA partner store — 350m* (e.g., Sharma Daily Mart).
* ✅ **Interactive Cart & Order Continuity:** Customer can add the substitute in 1 click; potential cancellation avoided in this simulation.
* ✅ **Business Impact HUD:** Live calculation separating verified case facts from demo session counters (simulated potential cancellation intercepted: 1, simulated GMV protected: ₹486 tied to case AOV).
* ✅ **Pilot KPIs to Validate:** Field trial targets for merchant updates/day, time per update, substitution acceptance rate, and availability cancellation rate.
* ✅ **1-Click Demo Reset:** Instantly resets all inventory states and counters back to baseline for repeated presentations.

### SIMULATED (Mocked / Modeled for the Hackathon)
* ⚠️ **620-Store Production Network:** Modeled using 2 realistic neighborhood partner stores (`Gupta Kirana` and `Sharma Daily Mart`).
* ⚠️ **Delivery Rider Dispatch Logistics:** Rider assignment and GPS route tracking are mocked.
* ⚠️ **Payment Gateway / Banking Settlement:** Order checkout and UPI payment are simulated via a 1-click confirmation modal.
* ⚠️ **WhatsApp Business API Webhook:** Simulated through the Merchant Web Console.

---

## 5. Is an API Key Required?

**NO.** The application is built with a resilient dual-mode architecture:
* **Default Mode (Local Intelligent NLP):** Runs 100% offline with zero dependencies, zero API keys, and zero network latency. It parses Hinglish intents (`"khatam"`, `"over"`, `"bacha hai"`, `"nahi hai"`) with deterministic confidence scoring.
* **Optional Live Gemini Mode:** You can click `⚙️ AI Config` in the top right, select `Gemini 1.5 / 2.5 Flash API`, paste your Gemini API key, and test live LLM extraction. If the API key is missing or fails, it automatically falls back to Local NLP without interrupting the demo.

---

## 6. Exact 2-Minute Demo Script (Guaranteed Flow)

Follow this exact sequence for a judge presentation:

1. **Step 1: Set the Baseline**
   * Keep the view on **Desktop Dual Split-View** (Default).
   * Point to the Right Pane (Customer Storefront): Show that `Amul Gold Full Cream Milk 500ml` is **IN STOCK (12 units)** at `Gupta Kirana Store`.
   * *"Judges, 35% of NOVA CART’s cancellations happen because this shelf goes empty in the real world, but the app doesn't know it."*

2. **Step 2: Merchant Action (5 Seconds)**
   * Look at the Left Pane (Merchant Console).
   * Point to the hypothesis: *"Hypothesis: one spoken/text update is lower effort than manual catalog editing. Pilot metric: updates per store per day."*
   * Click the preset chip: **`"Amul Gold doodh khatam ho gaya"`** (or speak it into the mic).
   * Click **`Sync To Customer Catalog Now`**.

3. **Step 3: AI Processing Trace**
   * Point to the black debug drawer below the merchant input:
   * Show the structured JSON payload:
     * `sku_id: "DAI-01"`
     * `product_name: "Amul Gold Full Cream Milk 500ml"`
     * `action: "OUT_OF_STOCK"`
     * `confidence: 0.96`
     * `ambiguous: false`

4. **Step 4: Real-Time Catalog Reaction**
   * Look at the Right Pane (Customer Storefront) without refreshing:
   * `Amul Gold Milk` has immediately flipped to grey with an **`OUT OF STOCK`** badge. The customer is blocked from placing an impossible order.

5. **Step 5: Smart Bridge Alternative**
   * Directly below the out-of-stock item, point out the **Availability bridge across local stores**:
     * *Same Store Alternative:* `Amul Taaza Milk 500ml (₹27)` with a green **`+ Add Alternative`** button.
     * *Nearby NOVA partner store — 350m:* `Available at Sharma Daily Mart (350m away)` with a blue **`Switch Store`** button.

6. **Step 6: The Order Rescue**
   * Click **`+ Add Alternative`**.
   * Amul Taaza is added to the customer's cart. A green banner confirms: *"Smart Bridge Active: Substitution applied. Potential cancellation avoided in this simulation."*

7. **Step 7: The Business Value Proof**
   * Scroll down to the **Business Impact HUD**:
   * Point to **Demo Session Telemetry (SIMULATED DEMO DATA)**:
     * **Simulated potential cancellation intercepted:** `1`
     * **Simulated GMV protected:** `₹486` (Tied to ₹486 case AOV)
     * **Simulated support ticket avoided:** `1`
   * Point to **Pilot KPIs to Validate**: highlight updates/day, update speed, substitution conversion, and cancellation rate targets.
   * *"In 5 seconds of merchant input, this prototype targets a major cancellation driver identified in the case, simulates ₹486 in GMV protected tied to case AOV, and demonstrates an availability bridge across local stores."*

---

## 7. Known Limitations

1. **Microphone Permissions in Non-Chromium Browsers:** Voice recognition relies on the Web Speech API (`webkitSpeechRecognition`), which requires microphone permission and works best in Google Chrome, Brave, and Edge. If a user denies mic permission, typing and one-click preset buttons are fully functional.
2. **Mock Catalog Scope:** The mock dataset contains 12 essential grocery SKUs across Dairy, Bakery, and Staples. This is intentionally sized for a high-clarity 3-hour hackathon demo rather than testing 50,000 enterprise SKUs.
3. **Multi-Store Route Optimization:** In the current prototype, switching to Sharma Daily Mart redirects the customer's order to that store. Real-world multi-store split-delivery routing is modeled conceptually.

---

## 8. Final Submission Checklist

* [x] Python HTTP server verified (`server.py` and `run.bat` tested).
* [x] Standalone zero-dependency HTML/JS/CSS verified.
* [x] Tested the exact core scenario: `Amul Gold doodh khatam ho gaya` $\rightarrow$ OOS $\rightarrow$ Smart Bridge $\rightarrow$ Alternative added $\rightarrow$ GMV protected.
* [x] Ambiguity handling tested: `Amul doodh nahi hai` prompts user with variant choice before mutating catalog.
* [x] Verified that all challenge data is accurately cited (38,500 orders, 11% cancels, 35% unavailability, 29% mismatch, 39% merchant burden, ₹486 AOV).
* [x] Verified that session simulation metrics are explicitly distinguished from case baseline facts.
