---
title: "Week 11 Worklog"
date: 2026-07-12
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:

* Build Advanced Finance & Tariff Module: Dynamic pricing configuration per Franchise Hub, automatic fallback to default system pricing grid, integrated e-wallet settlement and driver COD debt management.
* Build Web App Interface (Next.js 15, TailwindCSS): UI/UX optimization for Coordinators & Admins, resolve Leaflet Map memory leaks, integrate 2-in-1 Processing Station and Hub Data Isolation.
* Build Mobile App (Flutter & Riverpod): Camera Barcode/QR Code scanner flow integration, background GPS tracking & periodic Heartbeat, proof-of-delivery (POD) photo capture.
* Finalize Advanced Features: A6 shipping label PDF generation (PDFKit), Exception/Incident Management (`OrderIncident`), Support Ticket Chat (`TicketComment`), and Audit Log Subscriber tracing.
* Execute End-to-End (E2E Golden Flow 6-step) integration testing and code optimization ready for production deployment.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date |
| --- | --- | --- | --- |
| Mon | - Develop `FinanceModule`: Create `FinanceTariff` Entity (dynamic volumetric pricing formula $L \times W \times H / \text{volumetric\_divisor}$ and base/overage rates) & `FinanceTariffAudit` for pricing revision history.<br>- Develop `WalletsModule`: Build e-wallet transaction logic for Shippers (`cod_debt`, `income_balance`), schedule full COD debt settlement (`remitAllShipperCod`) wrapped inside Database Transactions with Pessimistic Lock (`pessimistic_write`). | 29/06/2026 | 29/06/2026 |
| Tue | - Web Dashboard Development (Next.js): Configure RBAC Sidebar according to roles, purge all mock data, normalize Pagination `{ data, meta }`.<br>- Optimize `TmsMap.tsx`: Use `useRef` and Cleanup function to eliminate "Map container is already initialized" crash.<br>- Build Station Page: Integrate quick Put-away input, view suggested Zone, edit weight with auto-recalculated tariffs and forced red blinking label reprint. | 30/06/2026 | 30/06/2026 |
| Wed | - Mobile App Development (Flutter): Configure Riverpod State Management, Dio HTTP Client with Auth Interceptor for automatic Token refresh.<br>- Build `ShipperScanScreen` (Mobile QR/Barcode Scanner), Order Status Update screen (`completeOrder`) attaching proof-of-delivery photo.<br>- Integrate background `LocationTrackerService` broadcasting GPS Heartbeats (`PATCH /users/heartbeat`) maintaining Online status for TMS algorithms. | 01/07/2026 | 01/07/2026 |
| Thu | - Implement `LabelService`: Use PDFKit and QRCode to render A6 shipping label PDF stream in Vietnamese (Roboto font) returned as Buffer Stream (`GET /orders/:id/label`).<br>- Upgrade Shipment Cancellation flow (`cancelShipment`): Auto-rollback internal order statuses back to `AT_HUB`, release `Vehicle` assignments, and record immutable Audit Logs (`AuditLogSubscriber`). | 02/07/2026 | 02/07/2026 |
| Fri | - Execute 6-Step Automated E2E Test Script (`e2e_test.js`): Admin Login $\rightarrow$ Create Order $\rightarrow$ Scan-In Warehouse Shelving $\rightarrow$ TMS Auto-Dispatch $\rightarrow$ Scan-Out Handover to Shipper $\rightarrow$ Mobile completeOrder double wallet reconciliation.<br>- Fix TypeScript compilation issues, verify `npm run build` succeeds on both Backend and Web App, commit code following Conventional Commits. | 03/07/2026 | 03/07/2026 |

### Week 11 Achievements:

* **Complete Financial & E-Wallet System:**
  * Successfully constructed dynamic volumetric pricing formula $V = (L \times W \times H) / 5000$, supporting Franchise Hub pricing with automatic system fallback.
  * Completely handled COD debt settlement and driver commission payouts via ACID transactions with absolute security, preventing Race Conditions.
* **Complete Multi-Platform Operational Interfaces:**
  * **Web App (Next.js):** Intuitive Dashboard connected 100% to real APIs, smooth Leaflet GIS map integration, All-in-One Station Page allowing scanning, re-labeling, weight modification, and continuous shelving.
  * **Mobile App (Flutter):** Smooth pickup/delivery execution flow, high-speed barcode scanning, automatic real-time GPS synchronization to Backend.
* **Completed E2E Golden Flow Testing:**
  * Successfully executed automated 6-step E2E test script covering order ingestion, WMS warehousing, TMS dispatching, delivery completion, and financial ledger closing.
  * Standardized source code, purged all mock data, compiled without TypeScript errors, ready for Docker containerization and AWS Cloud deployment.
