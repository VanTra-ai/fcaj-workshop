---
title: "Week 10 Worklog"
date: 2026-07-12
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

* Comprehensive business analysis for Supply Chain & Logistics Management Systems (WMS/TMS), translating requirements into Enterprise-grade software architecture.
* Design relational database model (ERD) on PostgreSQL, defining TypeORM Entities with complete foreign key constraints, indexes, and custom data transformers.
* Build core Backend using NestJS: Modular Monolith architecture, JWT Authentication integration, bcrypt password hashing, and Role-Based Access Control (RBAC Guard).
* Build core WMS (Warehouse Management System) module: Multi-tier storage location management (Zone/Aisle/Shelf/Bin), weight-based Put-away algorithm, packaging material management, and inventory audit flows.
* Develop core TMS (Transportation Management System) module: Fleet modeling (Bikes & Trucks), Auto-Dispatch algorithm with GPS Haversine distance grouping and vehicle capacity constraints.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date |
| --- | --- | --- | --- |
| Mon | - B2B Logistics business requirement analysis: Goods movement flow, RBAC permissions across 3 roles (`ADMIN`, `HUB_COORDINATOR`, `SHIPPER`).<br>- 3-Tier system architecture design: Backend Server (NestJS/TypeORM), Web Dashboard (Next.js/TailwindCSS), and Mobile App (Flutter/Riverpod).<br>- Design PostgreSQL Database ERD containing core tables: `users`, `hubs`, `orders`, `shipments`, `locations`, `vehicles`, `materials`, `wallets`, `incidents`, `tracking_history`. | 22/06/2026 | 22/06/2026 |
| Tue | - Initialize NestJS backend project, configure environment files (`.env`), and set up PostgreSQL connection via TypeORM (`AppModule`).<br>- Define `User` Entity (with auto-generated staff IDs, GPS coordinates, real-time heartbeat) and `Hub` Entity.<br>- Implement `AuthModule`: Build `/auth/login` and `/auth/refresh` APIs, Bcrypt hashing, Access Token / Refresh Token issuance, and `RolesGuard` security layer. | 23/06/2026 | 23/06/2026 |
| Wed | - Implement `Order` Entity and `OrdersService`: Build State Machine validation (`validateStatus`) protecting order lifecycles (`PENDING` $\rightarrow$ `AT_HUB` $\rightarrow$ `DELIVERING` $\rightarrow$ `FINISHED`).<br>- Integrate `EventEmitter2` triggering `order.status.changed` events to automatically append journey logs to `TrackingHistory`.<br>- Implement `OrdersExcelService` supporting bulk Excel order Import/Export via Buffer streams and Database Transactions. | 24/06/2026 | 24/06/2026 |
| Thu | - Develop WMS Module: Create `Location` Entity configuring shelf barcode format (`LOC-Zone-Aisle-Shelf-Bin`).<br>- Write `putaway()` method with pessimistic locking (`pessimistic_write`) to assign orders onto shelves and dynamically update warehouse capacity (`EMPTY` / `OCCUPIED` / `FULL`).<br>- Build `MaterialsModule` for packaging supply management and `AuditsModule` for inventory audit and shelf discrepancy reconciliation. | 25/06/2026 | 25/06/2026 |
| Fri | - Develop TMS Module: Initialize `Shipment` Entity categorizing Last-Mile Fleet (`BIKE`) and Line-Haul Fleet (`TRUCK`).<br>- Build `TmsService` and `RouteOptimizationService`: Program Auto-Dispatch algorithm scanning available shippers (online within 10 mins, no active `IN_TRANSIT` trip), calculate GPS distance using Haversine formula to suggest virtual shipments (`virtualShipments`). | 26/06/2026 | 26/06/2026 |

### Week 10 Achievements:

* **Robust Architecture & Database:**
  * Completed 100% ERD architecture diagram and successfully deployed 20+ TypeORM Entities synchronized to PostgreSQL Database.
  * Integrated secure password hashing, two-tier JWT Token issuance (Access/Refresh), and protected all Endpoints using AuthGuard & RolesGuard.
* **WMS & TMS Core Operation Engine:**
  * Successfully constructed closed Logistics State Machine, preventing non-sequential status updates from the Client.
  * Developed WMS Put-away algorithm auto-suggesting Zone A (<5kg) / Zone B ($\ge$5kg) and computing real-time warehouse occupancy rates.
  * Programmed TMS Auto-Dispatch algorithm optimizing delivery routes using Nearest Neighbor algorithm combined with vehicle weight locks.
