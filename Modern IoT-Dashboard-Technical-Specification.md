# IoT Dashboard Self-Service System
## Complete Technical Specification Document

**Version:** 1.0  
**Date:** January 10, 2026  
**Status:** Ready for Implementation

---

# 1. Executive Summary

## 1.1 Project Goal

Build a modern, AI-powered IoT Dashboard Self-Service System that replaces the complexity of ThingsBoard with a simpler, more maintainable architecture while providing superior user experience through AI-assisted features.

## 1.2 Key Differentiators

| Aspect | ThingsBoard | Our System |
|--------|-------------|------------|
| Framework | Angular 18 + NgRx | React 19 + Next.js 15 + Zustand |
| Widget System | Complex lifecycle, subscription management | Simple React components + hooks |
| Dashboard Builder | Configuration-heavy, JSON editing | Drag-drop + AI natural language |
| AI Integration | None | First-class citizen throughout |
| Learning Curve | Steep | Moderate |
| Multi-tenancy | Shared database | Database-per-tenant |

## 1.3 Scale Requirements

| Metric | Target |
|--------|--------|
| Devices | 2,000 - 10,000 |
| Data Throughput | 10-20 MB/second (constant) |
| Concurrent Users | 50+ dashboard users |
| Widgets per Dashboard | ~20 |
| Data Points per Chart | Maximum 50 |
| Region | Asia-Pacific (primary) |

---

# 2. Confirmed Requirements

## 2.1 Core Platform

| Requirement | Decision |
|-------------|----------|
| Users | Internal team + Customers, all technical levels |
| Registration | Self-service signup (basic), Admin-only (advanced features) |
| Tenant Model | Self-service with hierarchy: Organization → Site → Building → Floor → Area |
| Cross-tenant Sharing | No |
| Pricing Tiers | No (single tier for now) |

## 2.2 Device & Data Model

| Requirement | Decision |
|-------------|----------|
| Device Organization | Hierarchical (Site → Building → Floor → Area → Device) |
| Device Profiles/Types | Yes (templates with predefined telemetry keys) |
| Gateway Support | Yes (parent-child device relationships) |
| Telemetry Keys | Predefined per device type |
| Unit Management | Yes (automatic conversion) |
| Attributes | Server-side + Client-side + Shared (push to device) |

## 2.3 Dashboard & Widgets

| Requirement | Decision |
|-------------|----------|
| Dashboard Sharing | Yes (within tenant) |
| Public Dashboards | Yes (view-only, real-time data, no branding) |
| Dashboard Templates | Yes (cloneable) |
| Widget Cross-interaction | No |
| Time Sync Across Widgets | No |
| Dashboard States/Filters | Yes |
| User-specific Customization | Yes |

## 2.4 Alerting & Notifications

| Requirement | Decision |
|-------------|----------|
| Channels | Email, Webhook, In-app, Push (web + mobile future) |
| Alert Complexity | Simple threshold (value > X) |
| Acknowledgment Workflow | Yes |

## 2.5 Device Control (RPC)

| Requirement | Decision |
|-------------|----------|
| Bidirectional | Yes |
| Command Types | All (on/off, parameters, firmware) |
| Execution Mode | Asynchronous |
| Authorization | Role-based |
| Audit Logging | Yes, all commands |

## 2.6 Rule Engine

| Requirement | Decision |
|-------------|----------|
| Complexity | Simple (condition → action) |
| Actions | Create alert, Send notification |

## 2.7 AI Features (All Must Have)

| Feature | Priority |
|---------|----------|
| Natural language dashboard builder | Must Have |
| Natural language data queries | Must Have |
| Anomaly detection with explanations | Must Have |
| Alert summarization (daily digest) | Must Have |
| Predictive maintenance suggestions | Must Have |
| Auto-configuration recommendations | Must Have |
| Smart widget suggestions | Must Have |
| AI Autonomy | Suggest → User Approves |

## 2.8 Data Retention & Storage

| Requirement | Decision |
|-------------|----------|
| Raw Data Retention | 30 days |
| Cold Storage Archival | Yes |
| Cold Storage Retention | 1 year |
| Aggregation Intervals | 1 minute (automatic) |

## 2.9 Integration & Export

| Requirement | Decision |
|-------------|----------|
| External Integrations v1 | None required |
| Export Formats | CSV, JSON, Excel, PDF |
| Bulk Export | Yes |
| Tenant API Access | Yes (REST) |
| API Key Management | Yes, per tenant |

## 2.10 Security & Audit

| Requirement | Decision |
|-------------|----------|
| Security Features | Skip for now (future phase) |
| Audit Logging | Full audit of all user actions |
| Audit Retention | 30 days |

## 2.11 Deployment

| Requirement | Decision |
|-------------|----------|
| Geographic | Multi-region (Asia-Pacific primary) |
| Deployment Model | Self-hosted + Managed cloud (AWS, Azure) |
| Team Experience | Yes (React/Next.js) |
# 3. Technology Stack

## 3.1 Frontend Stack

| Component | Technology | Version | Rationale |
|-----------|------------|---------|-----------|
| Framework | Next.js (App Router) | 15.x | Server components, streaming, excellent DX |
| Language | TypeScript | 5.x | Type safety, better tooling |
| Styling | Tailwind CSS | 4.x | Utility-first, excellent performance |
| UI Components | shadcn/ui + Radix UI | Latest | Accessible, customizable, no lock-in |
| State (Client) | Zustand | 5.x | Simple, minimal boilerplate |
| State (Server) | TanStack Query | 5.x | Caching, real-time sync |
| Charts | Recharts | 2.x | React-native, good performance |
| Tables | TanStack Table | 8.x | Headless, highly customizable |
| Maps | Mapbox GL JS | 3.x | Best performance for large datasets |
| Drag & Drop | dnd-kit | 6.x | Modern, accessible, performant |
| Forms | React Hook Form + Zod | 7.x + 3.x | Type-safe validation |
| Real-time | Socket.io Client | 4.x | Reliable WebSocket abstraction |
| Icons | Lucide React | Latest | Consistent, tree-shakeable |
| Date/Time | date-fns | 3.x | Modular, lightweight |
| Notifications | Sonner | Latest | Modern toast notifications |

## 3.2 Backend Stack

| Component | Technology | Version | Rationale |
|-----------|------------|---------|-----------|
| Runtime | Node.js | 22 LTS | Latest features, excellent ecosystem |
| Framework | Next.js API Routes | 15.x | Unified frontend/backend |
| Type-safe API | tRPC | 11.x | End-to-end type safety |
| Authentication | Auth.js (NextAuth) | 5.x | OAuth providers, session management |
| Real-time | Socket.io Server | 4.x | Room-based pub/sub |
| Background Jobs | BullMQ | 5.x | Reliable job processing |
| Message Broker | Redpanda | Latest | Kafka-compatible, lower resources |
| Stream Processing | Benthos | 4.x | Lightweight, declarative pipelines |
| Email | Resend | Latest | Modern email API |
| Push Notifications | Web Push + Firebase | Latest | Browser + mobile push |

## 3.3 IoT Gateway Stack

| Component | Technology | Version | Rationale |
|-----------|------------|---------|-----------|
| MQTT Broker | EMQX | 5.x | High performance, clustering |
| HTTP Ingestion | Custom (Node.js) | - | Webhook support, validation |
| CoAP Gateway | node-coap | Latest | Constrained device support |
| LwM2M Server | Leshan | 2.x | Device management protocol |
| Modbus Gateway | modbus-serial | Latest | Industrial protocol support |
| OPC-UA | node-opcua | Latest | Industrial automation |

## 3.4 Data Layer Stack

| Component | Technology | Version | Rationale |
|-----------|------------|---------|-----------|
| Primary Database | PostgreSQL | 16.x | Reliable, feature-rich |
| Time-Series | TimescaleDB | 2.x | Native PostgreSQL extension |
| ORM | Prisma | 5.x | Type-safe queries, migrations |
| Cache | Redis | 7.x | Session, cache, pub/sub |
| Object Storage | MinIO | Latest | S3-compatible, self-hosted |
| Cold Storage | S3 Glacier | - | Long-term archival |

## 3.5 AI/ML Stack

| Component | Technology | Rationale |
|-----------|------------|-----------|
| LLM | Claude API (Anthropic) | Best reasoning, function calling |
| Vector Search | pgvector | PostgreSQL native |
| Statistical Analysis | simple-statistics | Lightweight anomaly detection |
| Forecasting | Prophet (Python microservice) | Time-series forecasting |

## 3.6 DevOps Stack

| Component | Technology | Rationale |
|-----------|------------|-----------|
| Containerization | Docker | Development parity |
| Orchestration | Kubernetes | Scaling, self-healing |
| API Gateway | Traefik | Auto-discovery, SSL |
| Monitoring | Prometheus + Grafana | Industry standard |
| Logging | Loki | Grafana integration |
| CI/CD | GitHub Actions | Repository integration |

## 3.7 Protocol Support Matrix

| Protocol | Port | Use Case | Implementation |
|----------|------|----------|----------------|
| MQTT | 1883/8883 | Primary IoT protocol | EMQX Broker |
| MQTT-WS | 8083/8084 | Browser-based devices | EMQX WebSocket |
| HTTP | 80/443 | Webhooks, simple devices | Next.js API Routes |
| CoAP | 5683/5684 | Constrained devices | node-coap |
| LwM2M | 5683 | Device management | Eclipse Leshan |
| Modbus TCP | 502 | Industrial devices | modbus-serial |
| OPC-UA | 4840 | Industrial automation | node-opcua |
# 3. System Architecture

## 3.1 High-Level Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                                    CLIENTS                                           │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐                 │
│  │   Web App   │  │ Mobile Web  │  │  Admin UI   │  │  REST API   │                 │
│  │  (Next.js)  │  │ (Responsive)│  │             │  │  Consumers  │                 │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘                 │
└─────────┴────────────────┴────────────────┴────────────────┴────────────────────────┘
                                    │
          ┌─────────────────────────┴─────────────────────────┐
          │              LOAD BALANCER (Traefik)               │
          └─────────────────────────┬─────────────────────────┘
                                    │
┌───────────────────────────────────┴─────────────────────────────────────────────────┐
│                              APPLICATION LAYER                                       │
│  ┌───────────────────────────────────────────────────────────────────────────────┐  │
│  │                     Next.js Application (App Router)                           │  │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐              │  │
│  │  │  Dashboard  │ │   Device    │ │    User     │ │     AI      │              │  │
│  │  │   Module    │ │   Module    │ │   Module    │ │   Module    │              │  │
│  │  ├─────────────┤ ├─────────────┤ ├─────────────┤ ├─────────────┤              │  │
│  │  │   Alert     │ │    Rule     │ │   Tenant    │ │   Export    │              │  │
│  │  │   Module    │ │   Engine    │ │   Module    │ │   Module    │              │  │
│  │  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘              │  │
│  └───────────────────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────────────────┐  │
│  │                    Real-Time Service (Socket.io Server)                        │  │
│  └───────────────────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                    │
┌───────────────────────────────────┴─────────────────────────────────────────────────┐
│                              MESSAGE BROKER (Kafka/Redpanda)                         │
│  Topics: telemetry.{tenant}.raw | telemetry.{tenant}.processed | alerts.{tenant}    │
│          device.{tenant}.status | device.{tenant}.commands | ai.{tenant}.insights   │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                    │
┌───────────────────────────────────┴─────────────────────────────────────────────────┐
│                              IoT PROTOCOL GATEWAY                                    │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐     │
│  │   MQTT   │ │   HTTP   │ │   CoAP   │ │  LwM2M   │ │  Modbus  │ │  OPC-UA  │     │
│  │  (EMQX)  │ │ Endpoint │ │ Gateway  │ │ (Leshan) │ │ Gateway  │ │ Adapter  │     │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘     │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                    │
┌───────────────────────────────────┴─────────────────────────────────────────────────┐
│                              DATA PROCESSING (Benthos)                               │
│  Pipelines: Validation → Normalization → Aggregation → Anomaly Detection → Routing  │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                    │
┌───────────────────────────────────┴─────────────────────────────────────────────────┐
│                              DATA STORAGE LAYER                                      │
│  ┌─────────────────────────┐  ┌─────────────────────────┐  ┌─────────────────────┐  │
│  │   PostgreSQL            │  │   TimescaleDB           │  │   Redis Cluster     │  │
│  │   (Per-Tenant DBs)      │  │   (Time-Series)         │  │   (Cache/Pub-Sub)   │  │
│  │   - Users, Roles        │  │   - Telemetry data      │  │   - Session cache   │  │
│  │   - Devices, Assets     │  │   - 1-min aggregates    │  │   - Real-time cache │  │
│  │   - Dashboards          │  │   - Continuous aggs     │  │   - Rate limiting   │  │
│  │   - Rules, Alerts       │  │   - 30-day retention    │  │   - Pub/Sub         │  │
│  └─────────────────────────┘  └─────────────────────────┘  └─────────────────────┘  │
│  ┌─────────────────────────┐  ┌─────────────────────────┐                           │
│  │   S3/MinIO              │  │   S3 Glacier            │                           │
│  │   (Object Storage)      │  │   (Cold Storage)        │                           │
│  │   - Exports, Reports    │  │   - 1-year retention    │                           │
│  └─────────────────────────┘  └─────────────────────────┘                           │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                    │
┌───────────────────────────────────┴─────────────────────────────────────────────────┐
│                              AI / ML SERVICES                                        │
│  ┌─────────────────────────┐  ┌─────────────────────────┐                           │
│  │   Claude API (LLM)      │  │   Local Analysis        │                           │
│  │   - NL Dashboard Build  │  │   - Anomaly detection   │                           │
│  │   - NL Data Queries     │  │   - Forecasting         │                           │
│  │   - Alert Summaries     │  │   - Pattern matching    │                           │
│  └─────────────────────────┘  └─────────────────────────┘                           │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

## 3.2 Real-Time Data Flow

```
Device → Protocol Gateway → Kafka Topic → Benthos Pipeline → TimescaleDB
                                                         → Redis (cache)
                                                         → Rule Engine (alerts)
                                                         → Socket.io → Browser
```

## 3.3 Device Command Flow (RPC)

```
User Dashboard → API → Validate Permissions → Create Command Record → Audit Log
                                                         ↓
                                              Kafka: device.commands
                                                         ↓
                                              MQTT: devices/{id}/commands
                                                         ↓
                                                      Device
                                                         ↓
                                              MQTT: devices/{id}/response
                                                         ↓
                                              Update Command Status
                                                         ↓
                                              Socket.io → Dashboard (result)
```

## 3.4 API Architecture

```
/api/
├── auth/              (Auth.js handlers)
│   └── [...nextauth]  (OAuth callbacks)
├── trpc/[trpc]        (tRPC router - internal API)
├── v1/                (REST API - external/tenant API)
│   ├── devices        (CRUD + telemetry)
│   ├── telemetry      (Query + export)
│   ├── dashboards     (CRUD)
│   ├── alerts         (CRUD + acknowledge)
│   └── export         (Bulk export)
├── realtime/          (Socket.io upgrade)
├── ai/                (AI endpoints)
│   ├── query          (Natural language query)
│   ├── dashboard      (Generate dashboard)
│   └── insights       (Get insights)
└── webhook/           (External webhooks)
    └── telemetry      (HTTP device ingestion)
```
# 5. Data Model

## 5.1 Multi-Tenant Database Architecture

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                           MULTI-TENANT DATA MODEL                                    │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                         MASTER DATABASE (Shared)                             │    │
│  │                                                                              │    │
│  │   tenants              tenant_databases         global_users                │    │
│  │   ┌────────────────┐   ┌────────────────────┐   ┌────────────────┐          │    │
│  │   │ id (UUID)      │──▶│ tenant_id (FK)     │   │ id             │          │    │
│  │   │ name           │   │ database_host      │   │ email          │          │    │
│  │   │ slug           │   │ database_name      │   │ role           │          │    │
│  │   │ status         │   │ database_user      │   │ created_at     │          │    │
│  │   │ plan           │   │ database_pass (enc)│   └────────────────┘          │    │
│  │   │ created_at     │   │ pool_size          │                               │    │
│  │   │ settings (JSON)│   │ status             │                               │    │
│  │   └────────────────┘   └────────────────────┘                               │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
│                          Connection Pool Manager (Dynamic tenant routing)            │
│                                         │                                            │
│           ┌─────────────────────────────┼─────────────────────────────┐              │
│           ▼                             ▼                             ▼              │
│  ┌─────────────────┐           ┌─────────────────┐           ┌─────────────────┐    │
│  │  Tenant A DB    │           │  Tenant B DB    │           │  Tenant C DB    │    │
│  │  (PostgreSQL)   │           │  (PostgreSQL)   │           │  (PostgreSQL)   │    │
│  └─────────────────┘           └─────────────────┘           └─────────────────┘    │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │               TimescaleDB (Shared - Tenant Isolation via tenant_id)          │    │
│  │                                                                              │    │
│  │   telemetry (Hypertable)                                                    │    │
│  │   ┌────────────────────────────────────────────────────────────────────┐    │    │
│  │   │ time (TIMESTAMPTZ) | tenant_id (UUID) | device_id | key | value   │    │    │
│  │   └────────────────────────────────────────────────────────────────────┘    │    │
│  │                                                                              │    │
│  │   Row-Level Security (RLS) enforces tenant_id isolation                     │    │
│  │   Continuous Aggregates: telemetry_1min, telemetry_1hour, telemetry_1day   │    │
│  │   Retention: 30 days raw → Archive to S3 Glacier                           │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

## 5.2 Master Database Schema

```sql
-- Master database for tenant management
-- Database: iot_master

-- Tenants table
CREATE TABLE tenants (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    slug VARCHAR(100) UNIQUE NOT NULL,
    status VARCHAR(20) DEFAULT 'active', -- active, suspended, deleted
    plan VARCHAR(50) DEFAULT 'standard',
    settings JSONB DEFAULT '{}',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Tenant database connections
CREATE TABLE tenant_databases (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID REFERENCES tenants(id) ON DELETE CASCADE,
    database_host VARCHAR(255) NOT NULL,
    database_port INTEGER DEFAULT 5432,
    database_name VARCHAR(100) NOT NULL,
    database_user VARCHAR(100) NOT NULL,
    database_password_encrypted TEXT NOT NULL,
    connection_pool_size INTEGER DEFAULT 10,
    status VARCHAR(20) DEFAULT 'active',
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Global super admins (platform owners)
CREATE TABLE global_users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    name VARCHAR(255),
    role VARCHAR(50) DEFAULT 'super_admin',
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Indexes
CREATE INDEX idx_tenants_slug ON tenants(slug);
CREATE INDEX idx_tenants_status ON tenants(status);
CREATE INDEX idx_tenant_databases_tenant ON tenant_databases(tenant_id);
```

## 5.3 Tenant Database Schema

```sql
-- ============================================
-- ORGANIZATION HIERARCHY
-- ============================================

-- Sites (top level)
CREATE TABLE sites (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    address TEXT,
    latitude DECIMAL(10, 8),
    longitude DECIMAL(11, 8),
    timezone VARCHAR(50) DEFAULT 'UTC',
    metadata JSONB DEFAULT '{}',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Buildings
CREATE TABLE buildings (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    site_id UUID REFERENCES sites(id) ON DELETE CASCADE,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    metadata JSONB DEFAULT '{}',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Floors
CREATE TABLE floors (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    building_id UUID REFERENCES buildings(id) ON DELETE CASCADE,
    name VARCHAR(100) NOT NULL,
    level INTEGER,
    floor_plan_url TEXT,
    metadata JSONB DEFAULT '{}',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Areas
CREATE TABLE areas (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    floor_id UUID REFERENCES floors(id) ON DELETE CASCADE,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    metadata JSONB DEFAULT '{}',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- ============================================
-- USER MANAGEMENT
-- ============================================

-- Roles
CREATE TABLE roles (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(100) NOT NULL,
    description TEXT,
    permissions JSONB NOT NULL DEFAULT '[]',
    is_system BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Default system roles
INSERT INTO roles (name, description, permissions, is_system) VALUES
('tenant_admin', 'Full access to all tenant resources', '["*"]', true),
('dashboard_manager', 'Can create and manage dashboards', 
 '["dashboard:*", "widget:*", "device:read", "telemetry:read", "alert:read,create,update"]', true),
('operator', 'Can view dashboards and control devices', 
 '["dashboard:read", "device:read,update", "telemetry:read", "alert:read,update"]', true),
('viewer', 'Read-only access to dashboards', 
 '["dashboard:read", "device:read", "telemetry:read", "alert:read"]', true);

-- Users
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    name VARCHAR(255),
    avatar_url TEXT,
    role_id UUID REFERENCES roles(id),
    email_verified BOOLEAN DEFAULT FALSE,
    status VARCHAR(20) DEFAULT 'active',
    last_login TIMESTAMPTZ,
    settings JSONB DEFAULT '{}',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- ============================================
-- DEVICE MANAGEMENT
-- ============================================

-- Device profiles/types
CREATE TABLE device_profiles (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    type VARCHAR(100) NOT NULL, -- sensor, actuator, gateway, controller
    telemetry_keys JSONB NOT NULL DEFAULT '[]',
    -- Example: [{"key": "temperature", "type": "number", "unit": "°C"}]
    attribute_keys JSONB NOT NULL DEFAULT '[]',
    command_types JSONB NOT NULL DEFAULT '[]',
    -- Example: [{"name": "reboot", "params": []}]
    default_alert_rules JSONB DEFAULT '[]',
    icon VARCHAR(100),
    metadata JSONB DEFAULT '{}',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Devices
CREATE TABLE devices (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    profile_id UUID REFERENCES device_profiles(id),
    area_id UUID REFERENCES areas(id),
    parent_device_id UUID REFERENCES devices(id), -- For gateway relationships
    
    name VARCHAR(255) NOT NULL,
    label VARCHAR(255),
    description TEXT,
    
    -- Credentials
    access_token VARCHAR(255) UNIQUE,
    credentials_type VARCHAR(50) DEFAULT 'access_token',
    credentials_data JSONB DEFAULT '{}',
    
    -- Status
    status VARCHAR(20) DEFAULT 'inactive', -- active, inactive, maintenance
    is_gateway BOOLEAN DEFAULT FALSE,
    last_activity TIMESTAMPTZ,
    last_connect TIMESTAMPTZ,
    last_disconnect TIMESTAMPTZ,
    
    -- Attributes
    server_attributes JSONB DEFAULT '{}',
    shared_attributes JSONB DEFAULT '{}',
    
    metadata JSONB DEFAULT '{}',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Device client attributes (reported by device)
CREATE TABLE device_client_attributes (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    device_id UUID REFERENCES devices(id) ON DELETE CASCADE,
    key VARCHAR(255) NOT NULL,
    value JSONB NOT NULL,
    updated_at TIMESTAMPTZ DEFAULT NOW(),
    UNIQUE(device_id, key)
);

-- ============================================
-- DASHBOARD & WIDGETS
-- ============================================

-- Dashboards
CREATE TABLE dashboards (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    
    -- Layout and configuration
    layout JSONB NOT NULL DEFAULT '{"columns": 12, "rowHeight": 80}',
    settings JSONB DEFAULT '{}',
    
    -- Sharing
    is_public BOOLEAN DEFAULT FALSE,
    public_token VARCHAR(255) UNIQUE,
    
    -- States/Filters
    states JSONB DEFAULT '[]',
    
    -- Ownership
    created_by UUID REFERENCES users(id),
    updated_by UUID REFERENCES users(id),
    
    -- Template
    is_template BOOLEAN DEFAULT FALSE,
    template_id UUID REFERENCES dashboards(id),
    
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Widgets
CREATE TABLE widgets (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    dashboard_id UUID REFERENCES dashboards(id) ON DELETE CASCADE,
    
    type VARCHAR(100) NOT NULL,
    title VARCHAR(255),
    
    -- Position (grid-based)
    position JSONB NOT NULL, -- {"x": 0, "y": 0, "w": 4, "h": 3}
    
    -- Data source configuration
    data_source JSONB NOT NULL DEFAULT '{}',
    
    -- Widget-specific configuration
    config JSONB DEFAULT '{}',
    
    -- Styling
    style JSONB DEFAULT '{}',
    
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- User dashboard customizations
CREATE TABLE user_dashboard_settings (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    dashboard_id UUID REFERENCES dashboards(id) ON DELETE CASCADE,
    widget_positions JSONB DEFAULT '{}',
    hidden_widgets UUID[] DEFAULT '{}',
    settings JSONB DEFAULT '{}',
    UNIQUE(user_id, dashboard_id)
);

-- Dashboard shares
CREATE TABLE dashboard_shares (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    dashboard_id UUID REFERENCES dashboards(id) ON DELETE CASCADE,
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    permission VARCHAR(20) DEFAULT 'view',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    UNIQUE(dashboard_id, user_id)
);

-- ============================================
-- ALERTING SYSTEM
-- ============================================

-- Alert rules
CREATE TABLE alert_rules (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    
    -- Condition
    device_profile_id UUID REFERENCES device_profiles(id),
    device_ids UUID[],
    telemetry_key VARCHAR(255) NOT NULL,
    condition_type VARCHAR(50) NOT NULL, -- gt, gte, lt, lte, eq, neq
    threshold DECIMAL NOT NULL,
    duration_seconds INTEGER DEFAULT 0,
    
    -- Alert settings
    severity VARCHAR(20) DEFAULT 'warning', -- info, warning, critical
    
    -- Notifications
    notification_channels JSONB DEFAULT '["in_app"]',
    notification_config JSONB DEFAULT '{}',
    
    is_active BOOLEAN DEFAULT TRUE,
    
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Alert instances
CREATE TABLE alerts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    rule_id UUID REFERENCES alert_rules(id),
    device_id UUID REFERENCES devices(id),
    
    severity VARCHAR(20) NOT NULL,
    status VARCHAR(20) DEFAULT 'active', -- active, acknowledged, resolved
    
    telemetry_key VARCHAR(255),
    trigger_value DECIMAL,
    threshold DECIMAL,
    message TEXT,
    
    triggered_at TIMESTAMPTZ DEFAULT NOW(),
    acknowledged_at TIMESTAMPTZ,
    acknowledged_by UUID REFERENCES users(id),
    resolved_at TIMESTAMPTZ,
    resolved_by UUID REFERENCES users(id),
    
    notes TEXT
);

-- ============================================
-- RULE ENGINE
-- ============================================

CREATE TABLE rules (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    
    trigger_type VARCHAR(50) NOT NULL, -- telemetry, device_status, schedule
    trigger_config JSONB NOT NULL,
    
    actions JSONB NOT NULL DEFAULT '[]',
    
    is_active BOOLEAN DEFAULT TRUE,
    
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- ============================================
-- DEVICE COMMANDS (RPC)
-- ============================================

CREATE TABLE device_commands (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    device_id UUID REFERENCES devices(id) ON DELETE CASCADE,
    
    command_type VARCHAR(100) NOT NULL,
    params JSONB DEFAULT '{}',
    
    status VARCHAR(20) DEFAULT 'pending', -- pending, sent, success, failed, timeout
    
    sent_at TIMESTAMPTZ,
    response JSONB,
    completed_at TIMESTAMPTZ,
    error_message TEXT,
    
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- ============================================
-- API KEYS
-- ============================================

CREATE TABLE api_keys (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    key_hash VARCHAR(255) UNIQUE NOT NULL,
    key_prefix VARCHAR(10) NOT NULL,
    
    permissions JSONB DEFAULT '["read"]',
    
    last_used_at TIMESTAMPTZ,
    expires_at TIMESTAMPTZ,
    
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMPTZ DEFAULT NOW(),
    revoked_at TIMESTAMPTZ
);

-- ============================================
-- AUDIT LOG
-- ============================================

CREATE TABLE audit_logs (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id),
    
    action VARCHAR(100) NOT NULL,
    resource_type VARCHAR(100) NOT NULL,
    resource_id UUID,
    
    details JSONB DEFAULT '{}',
    ip_address INET,
    user_agent TEXT,
    
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- ============================================
-- INDEXES
-- ============================================

CREATE INDEX idx_buildings_site ON buildings(site_id);
CREATE INDEX idx_floors_building ON floors(building_id);
CREATE INDEX idx_areas_floor ON areas(floor_id);
CREATE INDEX idx_devices_profile ON devices(profile_id);
CREATE INDEX idx_devices_area ON devices(area_id);
CREATE INDEX idx_devices_parent ON devices(parent_device_id);
CREATE INDEX idx_devices_status ON devices(status);
CREATE INDEX idx_devices_token ON devices(access_token);
CREATE INDEX idx_widgets_dashboard ON widgets(dashboard_id);
CREATE INDEX idx_alerts_status ON alerts(status);
CREATE INDEX idx_alerts_triggered ON alerts(triggered_at);
CREATE INDEX idx_commands_device ON device_commands(device_id);
CREATE INDEX idx_audit_user ON audit_logs(user_id);
CREATE INDEX idx_audit_created ON audit_logs(created_at);
```

## 5.4 TimescaleDB Schema

```sql
-- Enable TimescaleDB extension
CREATE EXTENSION IF NOT EXISTS timescaledb;

-- Main telemetry hypertable
CREATE TABLE telemetry (
    time TIMESTAMPTZ NOT NULL,
    tenant_id UUID NOT NULL,
    device_id UUID NOT NULL,
    key VARCHAR(255) NOT NULL,
    value_numeric DOUBLE PRECISION,
    value_string TEXT,
    value_boolean BOOLEAN,
    value_json JSONB
);

-- Convert to hypertable
SELECT create_hypertable('telemetry', 'time', 
    chunk_time_interval => INTERVAL '1 day',
    if_not_exists => TRUE
);

-- Indexes
CREATE INDEX idx_telemetry_tenant_device_key_time 
ON telemetry (tenant_id, device_id, key, time DESC);

-- Enable compression
ALTER TABLE telemetry SET (
    timescaledb.compress,
    timescaledb.compress_segmentby = 'tenant_id, device_id, key'
);

SELECT add_compression_policy('telemetry', INTERVAL '7 days');

-- Continuous aggregate for 1-minute averages
CREATE MATERIALIZED VIEW telemetry_1min
WITH (timescaledb.continuous) AS
SELECT
    time_bucket('1 minute', time) AS bucket,
    tenant_id,
    device_id,
    key,
    AVG(value_numeric) AS avg_value,
    MIN(value_numeric) AS min_value,
    MAX(value_numeric) AS max_value,
    COUNT(*) AS count
FROM telemetry
WHERE value_numeric IS NOT NULL
GROUP BY bucket, tenant_id, device_id, key
WITH NO DATA;

SELECT add_continuous_aggregate_policy('telemetry_1min',
    start_offset => INTERVAL '1 hour',
    end_offset => INTERVAL '1 minute',
    schedule_interval => INTERVAL '1 minute'
);

-- Retention policy: 30 days
SELECT add_retention_policy('telemetry', INTERVAL '30 days');

-- Row-Level Security
ALTER TABLE telemetry ENABLE ROW LEVEL SECURITY;

CREATE POLICY tenant_isolation ON telemetry
    USING (tenant_id = current_setting('app.current_tenant_id')::uuid);
```
# 6. Device Profiles (Industrial Standard Templates)

## 6.1 Profile Categories

| Category | Description | Example Devices |
|----------|-------------|-----------------|
| Industrial | Manufacturing and factory equipment | Motors, sensors, PLCs |
| Building | Building automation systems | HVAC, lighting, occupancy |
| Environmental | Weather and environmental monitoring | Weather stations, air quality |
| Fleet | Vehicle and transportation | GPS trackers, OBD readers |
| Energy | Power and energy management | Meters, inverters, batteries |
| Agriculture | Farming and agriculture | Soil sensors, irrigation |
| Infrastructure | Network and system devices | Gateways, edge devices |

## 6.2 Industrial Device Profiles

### Temperature Sensor
```json
{
  "name": "Temperature Sensor",
  "type": "sensor",
  "category": "industrial",
  "telemetryKeys": [
    { "key": "temperature", "type": "number", "unit": "°C", "min": -40, "max": 125 },
    { "key": "battery", "type": "number", "unit": "%", "min": 0, "max": 100 }
  ],
  "attributeKeys": [
    { "key": "firmware_version", "type": "string" },
    { "key": "calibration_date", "type": "date" },
    { "key": "accuracy", "type": "string" },
    { "key": "location", "type": "string" }
  ],
  "commandTypes": [
    { "name": "reboot", "params": [] },
    { "name": "set_interval", "params": [{ "name": "interval_ms", "type": "number" }] },
    { "name": "calibrate", "params": [] }
  ],
  "defaultAlertRules": [
    { "key": "temperature", "condition": "gt", "threshold": 40, "severity": "warning" },
    { "key": "temperature", "condition": "gt", "threshold": 50, "severity": "critical" },
    { "key": "battery", "condition": "lt", "threshold": 20, "severity": "warning" }
  ],
  "icon": "thermometer"
}
```

### Humidity Sensor
```json
{
  "name": "Humidity Sensor",
  "type": "sensor",
  "category": "industrial",
  "telemetryKeys": [
    { "key": "humidity", "type": "number", "unit": "%", "min": 0, "max": 100 },
    { "key": "temperature", "type": "number", "unit": "°C", "min": -40, "max": 85 },
    { "key": "battery", "type": "number", "unit": "%", "min": 0, "max": 100 }
  ],
  "attributeKeys": [
    { "key": "firmware_version", "type": "string" },
    { "key": "location", "type": "string" }
  ],
  "commandTypes": [
    { "name": "reboot", "params": [] },
    { "name": "set_interval", "params": [{ "name": "interval_ms", "type": "number" }] }
  ],
  "defaultAlertRules": [
    { "key": "humidity", "condition": "gt", "threshold": 80, "severity": "warning" },
    { "key": "humidity", "condition": "lt", "threshold": 20, "severity": "warning" }
  ],
  "icon": "droplets"
}
```

### Pressure Sensor
```json
{
  "name": "Pressure Sensor",
  "type": "sensor",
  "category": "industrial",
  "telemetryKeys": [
    { "key": "pressure", "type": "number", "unit": "bar", "min": 0, "max": 100 },
    { "key": "temperature", "type": "number", "unit": "°C" }
  ],
  "attributeKeys": [
    { "key": "firmware_version", "type": "string" },
    { "key": "max_pressure", "type": "number" },
    { "key": "location", "type": "string" }
  ],
  "commandTypes": [
    { "name": "calibrate", "params": [] },
    { "name": "reboot", "params": [] }
  ],
  "defaultAlertRules": [
    { "key": "pressure", "condition": "gt", "threshold": 80, "severity": "critical" }
  ],
  "icon": "gauge"
}
```

### Flow Meter
```json
{
  "name": "Flow Meter",
  "type": "sensor",
  "category": "industrial",
  "telemetryKeys": [
    { "key": "flow_rate", "type": "number", "unit": "L/min", "min": 0 },
    { "key": "total_volume", "type": "number", "unit": "L", "min": 0 },
    { "key": "temperature", "type": "number", "unit": "°C" }
  ],
  "attributeKeys": [
    { "key": "pipe_diameter", "type": "number" },
    { "key": "max_flow", "type": "number" },
    { "key": "location", "type": "string" }
  ],
  "commandTypes": [
    { "name": "reset_counter", "params": [] },
    { "name": "reboot", "params": [] }
  ],
  "icon": "waves"
}
```

### Industrial Motor
```json
{
  "name": "Industrial Motor",
  "type": "actuator",
  "category": "industrial",
  "telemetryKeys": [
    { "key": "rpm", "type": "number", "unit": "RPM", "min": 0, "max": 5000 },
    { "key": "current", "type": "number", "unit": "A", "min": 0 },
    { "key": "temperature", "type": "number", "unit": "°C" },
    { "key": "vibration", "type": "number", "unit": "mm/s" },
    { "key": "power", "type": "number", "unit": "kW" },
    { "key": "running", "type": "boolean" }
  ],
  "attributeKeys": [
    { "key": "model", "type": "string" },
    { "key": "power_rating", "type": "number" },
    { "key": "max_rpm", "type": "number" },
    { "key": "location", "type": "string" }
  ],
  "commandTypes": [
    { "name": "start", "params": [] },
    { "name": "stop", "params": [] },
    { "name": "set_speed", "params": [{ "name": "rpm", "type": "number" }] },
    { "name": "emergency_stop", "params": [] }
  ],
  "defaultAlertRules": [
    { "key": "temperature", "condition": "gt", "threshold": 80, "severity": "warning" },
    { "key": "temperature", "condition": "gt", "threshold": 95, "severity": "critical" },
    { "key": "vibration", "condition": "gt", "threshold": 10, "severity": "warning" }
  ],
  "icon": "cog"
}
```

### Power Meter
```json
{
  "name": "Power Meter",
  "type": "sensor",
  "category": "energy",
  "telemetryKeys": [
    { "key": "voltage", "type": "number", "unit": "V" },
    { "key": "current", "type": "number", "unit": "A" },
    { "key": "power", "type": "number", "unit": "kW" },
    { "key": "energy", "type": "number", "unit": "kWh" },
    { "key": "power_factor", "type": "number", "unit": "" },
    { "key": "frequency", "type": "number", "unit": "Hz" }
  ],
  "attributeKeys": [
    { "key": "phase", "type": "string" },
    { "key": "max_current", "type": "number" },
    { "key": "ct_ratio", "type": "string" },
    { "key": "location", "type": "string" }
  ],
  "commandTypes": [
    { "name": "reset_energy", "params": [] },
    { "name": "reboot", "params": [] }
  ],
  "icon": "zap"
}
```

## 6.3 Building Automation Profiles

### HVAC Unit
```json
{
  "name": "HVAC Unit",
  "type": "controller",
  "category": "building",
  "telemetryKeys": [
    { "key": "supply_temp", "type": "number", "unit": "°C" },
    { "key": "return_temp", "type": "number", "unit": "°C" },
    { "key": "setpoint", "type": "number", "unit": "°C" },
    { "key": "fan_speed", "type": "number", "unit": "%" },
    { "key": "mode", "type": "string" },
    { "key": "power", "type": "number", "unit": "kW" }
  ],
  "attributeKeys": [
    { "key": "zone", "type": "string" },
    { "key": "capacity", "type": "number" },
    { "key": "model", "type": "string" }
  ],
  "commandTypes": [
    { "name": "set_mode", "params": [{ "name": "mode", "type": "string", "enum": ["cooling", "heating", "auto", "off"] }] },
    { "name": "set_setpoint", "params": [{ "name": "temperature", "type": "number" }] },
    { "name": "set_fan_speed", "params": [{ "name": "speed", "type": "number" }] }
  ],
  "icon": "wind"
}
```

### Occupancy Sensor
```json
{
  "name": "Occupancy Sensor",
  "type": "sensor",
  "category": "building",
  "telemetryKeys": [
    { "key": "occupied", "type": "boolean" },
    { "key": "count", "type": "number", "unit": "people" },
    { "key": "battery", "type": "number", "unit": "%" }
  ],
  "attributeKeys": [
    { "key": "zone", "type": "string" },
    { "key": "max_capacity", "type": "number" },
    { "key": "detection_range", "type": "number" }
  ],
  "commandTypes": [
    { "name": "reset_count", "params": [] }
  ],
  "icon": "users"
}
```

### Air Quality Sensor
```json
{
  "name": "Air Quality Sensor",
  "type": "sensor",
  "category": "building",
  "telemetryKeys": [
    { "key": "co2", "type": "number", "unit": "ppm" },
    { "key": "pm25", "type": "number", "unit": "µg/m³" },
    { "key": "pm10", "type": "number", "unit": "µg/m³" },
    { "key": "voc", "type": "number", "unit": "ppb" },
    { "key": "temperature", "type": "number", "unit": "°C" },
    { "key": "humidity", "type": "number", "unit": "%" }
  ],
  "attributeKeys": [
    { "key": "location", "type": "string" },
    { "key": "firmware_version", "type": "string" }
  ],
  "commandTypes": [
    { "name": "calibrate", "params": [] }
  ],
  "defaultAlertRules": [
    { "key": "co2", "condition": "gt", "threshold": 1000, "severity": "warning" },
    { "key": "pm25", "condition": "gt", "threshold": 35, "severity": "warning" }
  ],
  "icon": "cloud"
}
```

### Lighting Controller
```json
{
  "name": "Lighting Controller",
  "type": "actuator",
  "category": "building",
  "telemetryKeys": [
    { "key": "brightness", "type": "number", "unit": "%" },
    { "key": "power", "type": "number", "unit": "W" },
    { "key": "on", "type": "boolean" },
    { "key": "color_temp", "type": "number", "unit": "K" }
  ],
  "attributeKeys": [
    { "key": "zone", "type": "string" },
    { "key": "fixture_count", "type": "number" },
    { "key": "max_power", "type": "number" }
  ],
  "commandTypes": [
    { "name": "turn_on", "params": [] },
    { "name": "turn_off", "params": [] },
    { "name": "set_brightness", "params": [{ "name": "level", "type": "number" }] },
    { "name": "set_color_temp", "params": [{ "name": "kelvin", "type": "number" }] }
  ],
  "icon": "lightbulb"
}
```

## 6.4 Fleet/Vehicle Profiles

### Vehicle GPS Tracker
```json
{
  "name": "Vehicle GPS Tracker",
  "type": "sensor",
  "category": "fleet",
  "telemetryKeys": [
    { "key": "latitude", "type": "number", "unit": "°" },
    { "key": "longitude", "type": "number", "unit": "°" },
    { "key": "speed", "type": "number", "unit": "km/h" },
    { "key": "heading", "type": "number", "unit": "°" },
    { "key": "altitude", "type": "number", "unit": "m" },
    { "key": "satellites", "type": "number" },
    { "key": "battery", "type": "number", "unit": "%" }
  ],
  "attributeKeys": [
    { "key": "vehicle_id", "type": "string" },
    { "key": "plate_number", "type": "string" },
    { "key": "driver", "type": "string" },
    { "key": "imei", "type": "string" }
  ],
  "commandTypes": [
    { "name": "get_location", "params": [] },
    { "name": "set_interval", "params": [{ "name": "seconds", "type": "number" }] }
  ],
  "icon": "map-pin"
}
```

### Vehicle Diagnostics (OBD)
```json
{
  "name": "Vehicle Diagnostics (OBD)",
  "type": "sensor",
  "category": "fleet",
  "telemetryKeys": [
    { "key": "engine_rpm", "type": "number", "unit": "RPM" },
    { "key": "vehicle_speed", "type": "number", "unit": "km/h" },
    { "key": "fuel_level", "type": "number", "unit": "%" },
    { "key": "engine_temp", "type": "number", "unit": "°C" },
    { "key": "battery_voltage", "type": "number", "unit": "V" },
    { "key": "odometer", "type": "number", "unit": "km" },
    { "key": "dtc_count", "type": "number" }
  ],
  "attributeKeys": [
    { "key": "vin", "type": "string" },
    { "key": "make", "type": "string" },
    { "key": "model", "type": "string" },
    { "key": "year", "type": "number" }
  ],
  "commandTypes": [
    { "name": "read_dtc", "params": [] },
    { "name": "clear_dtc", "params": [] }
  ],
  "defaultAlertRules": [
    { "key": "engine_temp", "condition": "gt", "threshold": 100, "severity": "warning" },
    { "key": "battery_voltage", "condition": "lt", "threshold": 11.5, "severity": "warning" }
  ],
  "icon": "car"
}
```

## 6.5 Environmental Profiles

### Weather Station
```json
{
  "name": "Weather Station",
  "type": "sensor",
  "category": "environmental",
  "telemetryKeys": [
    { "key": "temperature", "type": "number", "unit": "°C" },
    { "key": "humidity", "type": "number", "unit": "%" },
    { "key": "pressure", "type": "number", "unit": "hPa" },
    { "key": "wind_speed", "type": "number", "unit": "m/s" },
    { "key": "wind_direction", "type": "number", "unit": "°" },
    { "key": "rainfall", "type": "number", "unit": "mm" },
    { "key": "uv_index", "type": "number" },
    { "key": "solar_radiation", "type": "number", "unit": "W/m²" }
  ],
  "attributeKeys": [
    { "key": "location", "type": "string" },
    { "key": "altitude", "type": "number" },
    { "key": "station_id", "type": "string" }
  ],
  "commandTypes": [],
  "icon": "cloud-sun"
}
```

### Soil Sensor
```json
{
  "name": "Soil Sensor",
  "type": "sensor",
  "category": "agriculture",
  "telemetryKeys": [
    { "key": "soil_moisture", "type": "number", "unit": "%" },
    { "key": "soil_temp", "type": "number", "unit": "°C" },
    { "key": "ph", "type": "number" },
    { "key": "ec", "type": "number", "unit": "dS/m" },
    { "key": "nitrogen", "type": "number", "unit": "mg/kg" },
    { "key": "phosphorus", "type": "number", "unit": "mg/kg" },
    { "key": "potassium", "type": "number", "unit": "mg/kg" }
  ],
  "attributeKeys": [
    { "key": "plot", "type": "string" },
    { "key": "depth", "type": "number" },
    { "key": "crop_type", "type": "string" }
  ],
  "commandTypes": [],
  "defaultAlertRules": [
    { "key": "soil_moisture", "condition": "lt", "threshold": 20, "severity": "warning" }
  ],
  "icon": "sprout"
}
```

## 6.6 Infrastructure Profiles

### IoT Gateway
```json
{
  "name": "IoT Gateway",
  "type": "gateway",
  "category": "infrastructure",
  "isGateway": true,
  "telemetryKeys": [
    { "key": "cpu_usage", "type": "number", "unit": "%" },
    { "key": "memory_usage", "type": "number", "unit": "%" },
    { "key": "disk_usage", "type": "number", "unit": "%" },
    { "key": "connected_devices", "type": "number" },
    { "key": "uptime", "type": "number", "unit": "seconds" },
    { "key": "messages_sent", "type": "number" },
    { "key": "messages_received", "type": "number" }
  ],
  "attributeKeys": [
    { "key": "firmware_version", "type": "string" },
    { "key": "ip_address", "type": "string" },
    { "key": "mac_address", "type": "string" },
    { "key": "model", "type": "string" }
  ],
  "commandTypes": [
    { "name": "reboot", "params": [] },
    { "name": "update_firmware", "params": [{ "name": "url", "type": "string" }] },
    { "name": "scan_devices", "params": [] },
    { "name": "restart_service", "params": [{ "name": "service", "type": "string" }] }
  ],
  "defaultAlertRules": [
    { "key": "cpu_usage", "condition": "gt", "threshold": 90, "severity": "warning" },
    { "key": "memory_usage", "condition": "gt", "threshold": 90, "severity": "warning" },
    { "key": "disk_usage", "condition": "gt", "threshold": 85, "severity": "warning" }
  ],
  "icon": "router"
}
```

### Network Switch
```json
{
  "name": "Network Switch",
  "type": "sensor",
  "category": "infrastructure",
  "telemetryKeys": [
    { "key": "port_status", "type": "json" },
    { "key": "cpu_usage", "type": "number", "unit": "%" },
    { "key": "temperature", "type": "number", "unit": "°C" },
    { "key": "uptime", "type": "number", "unit": "seconds" },
    { "key": "throughput_in", "type": "number", "unit": "Mbps" },
    { "key": "throughput_out", "type": "number", "unit": "Mbps" }
  ],
  "attributeKeys": [
    { "key": "model", "type": "string" },
    { "key": "firmware", "type": "string" },
    { "key": "ip_address", "type": "string" },
    { "key": "port_count", "type": "number" }
  ],
  "commandTypes": [
    { "name": "reboot", "params": [] }
  ],
  "icon": "network"
}
```
# 7. Widget System

## 7.1 Widget Type Registry

| Category | Widget Type | Description | Data Source |
|----------|------------|-------------|-------------|
| **Charts** | `line_chart` | Time-series line chart | timeseries |
| | `area_chart` | Filled area chart | timeseries |
| | `bar_chart` | Vertical/horizontal bars | timeseries, latest |
| | `pie_chart` | Pie/donut chart | latest |
| **Values** | `gauge` | Radial gauge with thresholds | latest |
| | `value_card` | Single value display | latest |
| | `led_indicator` | On/off status indicator | latest |
| | `stats_card` | Value with trend indicator | latest |
| **Tables** | `alarm_table` | Alert list with actions | alerts |
| | `device_table` | Device list with status | devices |
| | `telemetry_table` | Raw telemetry data table | timeseries |
| **Controls** | `control_button` | Command trigger button | n/a |
| | `control_slider` | Value slider control | n/a |
| | `control_switch` | On/off toggle | n/a |
| **Maps** | `device_map` | Device location map | devices |
| | `heatmap` | Value density map | latest |
| **Static** | `html` | Custom HTML content | static |
| | `markdown` | Markdown content | static |
| | `image` | Image display | static |
| **AI** | `ai_insight` | AI-generated insights | ai |
| | `anomaly_chart` | Anomaly-highlighted chart | timeseries |

## 7.2 Widget Type Definitions

```typescript
// types/widget.ts

export type WidgetType =
  // Charts
  | 'line_chart'
  | 'area_chart'
  | 'bar_chart'
  | 'pie_chart'
  // Values
  | 'gauge'
  | 'value_card'
  | 'led_indicator'
  | 'stats_card'
  // Tables
  | 'alarm_table'
  | 'device_table'
  | 'telemetry_table'
  // Controls
  | 'control_button'
  | 'control_slider'
  | 'control_switch'
  // Maps
  | 'device_map'
  | 'heatmap'
  // Static
  | 'html'
  | 'markdown'
  | 'image'
  // AI
  | 'ai_insight'
  | 'anomaly_chart';

export interface Widget {
  id: string;
  type: WidgetType;
  title: string;
  position: WidgetPosition;
  dataSource: DataSourceConfig;
  config: WidgetConfig;
  style?: WidgetStyle;
}

export interface WidgetPosition {
  x: number;      // Grid column (0-11)
  y: number;      // Grid row
  w: number;      // Width in columns (1-12)
  h: number;      // Height in rows
}

export interface DataSourceConfig {
  type: 'timeseries' | 'latest' | 'alerts' | 'devices' | 'static' | 'ai';
  
  // For telemetry data
  deviceIds?: string[];
  deviceProfileId?: string;
  keys?: string[];
  
  // Time range
  timeRange?: TimeRange;
  
  // Aggregation
  aggregation?: 'none' | 'avg' | 'min' | 'max' | 'sum' | 'count';
  interval?: '1m' | '5m' | '15m' | '1h' | '1d';
  
  // For static content
  content?: string;
}

export type TimeRange =
  | { type: 'relative'; value: string }  // '15m', '1h', '24h', '7d', '30d'
  | { type: 'absolute'; start: string; end: string };
```

## 7.3 Widget Configurations

### Line/Area Chart Config
```typescript
interface ChartConfig {
  chartType: 'line' | 'area' | 'bar';
  showLegend: boolean;
  showGrid: boolean;
  showTooltip: boolean;
  yAxisMin?: number;
  yAxisMax?: number;
  yAxisLabel?: string;
  xAxisLabel?: string;
  colors?: string[];
  stacked?: boolean;
  smooth?: boolean;
}
```

### Gauge Config
```typescript
interface GaugeConfig {
  min: number;
  max: number;
  unit: string;
  decimals: number;
  thresholds: {
    value: number;
    color: string;
    label?: string;
  }[];
  showMinMax: boolean;
  arcWidth: number;
}
```

### Value Card Config
```typescript
interface ValueCardConfig {
  unit: string;
  decimals: number;
  fontSize: 'small' | 'medium' | 'large';
  showTrend: boolean;
  trendPeriod: string;
  colorRules?: {
    condition: 'gt' | 'lt' | 'eq';
    value: number;
    color: string;
  }[];
}
```

### Alarm Table Config
```typescript
interface AlarmTableConfig {
  columns: ('severity' | 'device' | 'message' | 'time' | 'status' | 'actions')[];
  pageSize: number;
  showFilters: boolean;
  defaultSeverityFilter?: string[];
  defaultStatusFilter?: string[];
}
```

### Control Button Config
```typescript
interface ControlButtonConfig {
  commandType: string;
  commandParams: Record<string, any>;
  label: string;
  confirmRequired: boolean;
  confirmMessage?: string;
  variant: 'default' | 'primary' | 'danger';
  icon?: string;
}
```

### Map Config
```typescript
interface MapConfig {
  mapStyle: 'streets' | 'satellite' | 'dark' | 'light';
  defaultZoom: number;
  defaultCenter: [number, number];
  clusterDevices: boolean;
  showStatusColors: boolean;
  popupFields: string[];
}
```

## 7.4 Widget Component Pattern

```typescript
// components/widgets/base/widget-wrapper.tsx

interface WidgetWrapperProps {
  widget: Widget;
  isEditing: boolean;
  isSelected: boolean;
  onSelect: () => void;
  onUpdate: (updates: Partial<Widget>) => void;
  children: React.ReactNode;
}

export function WidgetWrapper({
  widget,
  isEditing,
  isSelected,
  onSelect,
  onUpdate,
  children
}: WidgetWrapperProps) {
  return (
    <Card
      className={cn(
        'h-full flex flex-col overflow-hidden',
        isEditing && 'cursor-move hover:ring-2 hover:ring-primary/50',
        isSelected && 'ring-2 ring-primary'
      )}
      onClick={isEditing ? onSelect : undefined}
    >
      <WidgetHeader
        title={widget.title}
        isEditing={isEditing}
        onTitleChange={(title) => onUpdate({ title })}
        onRefresh={() => {/* trigger data refresh */}}
        onSettings={() => {/* open settings panel */}}
      />
      <CardContent className="flex-1 p-4 overflow-hidden">
        <ErrorBoundary fallback={<WidgetError />}>
          <Suspense fallback={<WidgetLoading />}>
            {children}
          </Suspense>
        </ErrorBoundary>
      </CardContent>
    </Card>
  );
}
```

## 7.5 Widget Data Hook

```typescript
// hooks/useWidgetData.ts

export function useWidgetData(dataSource: DataSourceConfig) {
  const queryClient = useQueryClient();
  const { socket } = useSocket();
  
  const queryKey = useMemo(() => ['widget-data', dataSource], [dataSource]);
  
  // Fetch initial/historical data
  const query = useQuery({
    queryKey,
    queryFn: () => fetchWidgetData(dataSource),
    staleTime: dataSource.type === 'latest' ? 0 : 60000,
    refetchInterval: dataSource.type === 'latest' ? 5000 : false,
  });
  
  // Subscribe to real-time updates
  useEffect(() => {
    if (!socket || !['timeseries', 'latest'].includes(dataSource.type)) {
      return;
    }
    
    const deviceIds = dataSource.deviceIds || [];
    const keys = dataSource.keys || [];
    
    deviceIds.forEach(deviceId => {
      socket.emit('subscribe:telemetry', { deviceId, keys });
    });
    
    const handleTelemetry = (payload: TelemetryUpdate) => {
      queryClient.setQueryData(queryKey, (old: any) => {
        return mergeTelemetryData(old, payload);
      });
    };
    
    socket.on('telemetry:update', handleTelemetry);
    
    return () => {
      deviceIds.forEach(deviceId => {
        socket.emit('unsubscribe:telemetry', { deviceId });
      });
      socket.off('telemetry:update', handleTelemetry);
    };
  }, [dataSource, socket, queryClient, queryKey]);
  
  return query;
}
```

## 7.6 Widget Registry

```typescript
// lib/widgets/registry.ts

export interface WidgetDefinition {
  type: WidgetType;
  name: string;
  description: string;
  icon: LucideIcon;
  category: WidgetCategory;
  component: React.ComponentType<WidgetProps>;
  configComponent: React.ComponentType<WidgetConfigProps>;
  defaultConfig: Partial<WidgetConfig>;
  defaultSize: { w: number; h: number };
  minSize: { w: number; h: number };
  maxSize: { w: number; h: number };
  dataSourceTypes: DataSourceConfig['type'][];
}

export const WIDGET_REGISTRY: Record<WidgetType, WidgetDefinition> = {
  line_chart: {
    type: 'line_chart',
    name: 'Line Chart',
    description: 'Display time-series data as a line chart',
    icon: LineChart,
    category: 'charts',
    component: LineChartWidget,
    configComponent: LineChartConfig,
    defaultConfig: { showLegend: true, showGrid: true },
    defaultSize: { w: 6, h: 3 },
    minSize: { w: 3, h: 2 },
    maxSize: { w: 12, h: 6 },
    dataSourceTypes: ['timeseries'],
  },
  gauge: {
    type: 'gauge',
    name: 'Gauge',
    description: 'Display a single value as a radial gauge',
    icon: Gauge,
    category: 'values',
    component: GaugeWidget,
    configComponent: GaugeConfig,
    defaultConfig: { min: 0, max: 100, decimals: 1 },
    defaultSize: { w: 2, h: 2 },
    minSize: { w: 2, h: 2 },
    maxSize: { w: 4, h: 4 },
    dataSourceTypes: ['latest'],
  },
  // ... other widgets
};

export const WIDGET_CATEGORIES = {
  charts: { name: 'Charts', icon: BarChart3 },
  values: { name: 'Values', icon: Activity },
  tables: { name: 'Tables', icon: Table },
  controls: { name: 'Controls', icon: Sliders },
  maps: { name: 'Maps', icon: Map },
  static: { name: 'Static', icon: FileText },
  ai: { name: 'AI', icon: Sparkles },
};
```

---

# 8. Dashboard Builder

## 8.1 Builder UI Layout

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│  Dashboard Builder                                              [Preview] [Save]    │
├────────────┬────────────────────────────────────────────────────────────────────────┤
│            │                                                                        │
│  WIDGETS   │                        CANVAS                                          │
│            │  ┌──────────────────────────────────────────────────────────────────┐  │
│  ○ Charts  │  │                                                                  │  │
│    Line    │  │    ┌────────────┐  ┌────────────┐  ┌────────────┐               │  │
│    Area    │  │    │   Widget   │  │   Widget   │  │   Widget   │               │  │
│    Bar     │  │    │     1      │  │     2      │  │     3      │               │  │
│            │  │    └────────────┘  └────────────┘  └────────────┘               │  │
│  ○ Values  │  │                                                                  │  │
│    Gauge   │  │    ┌─────────────────────────────────────────────┐               │  │
│    Card    │  │    │                Widget 4                      │               │  │
│            │  │    │                                              │               │  │
│  ○ Tables  │  │    └─────────────────────────────────────────────┘               │  │
│            │  │                                                                  │  │
│  ○ Controls│  └──────────────────────────────────────────────────────────────────┘  │
│            │                                                                        │
│  ○ Maps    ├────────────────────────────────────────────────────────────────────────┤
│            │                     PROPERTIES PANEL                                   │
│  ○ Static  │  ┌──────────────────────────────────────────────────────────────────┐  │
│            │  │  Widget: Line Chart                                              │  │
│  ○ AI      │  │  ─────────────────────────────────────────────────────────────   │  │
│            │  │                                                                  │  │
│ ───────────│  │  📊 Data Source                                                  │  │
│            │  │  Device: [Select devices...                    ▼]               │  │
│  🤖 AI     │  │  Keys:   [temperature, humidity               ▼]               │  │
│  Assistant │  │  Time:   [Last 24 hours                       ▼]               │  │
│            │  │  Agg:    [5 minute average                    ▼]               │  │
│  "Create a │  │                                                                  │  │
│   dashboard│  │  🎨 Appearance                                                   │  │
│   for..."  │  │  Title: [Temperature Trend                     ]               │  │
│            │  │  Legend: ☑ Show                                                 │  │
│  [Send]    │  │  Grid:   ☑ Show                                                 │  │
│            │  │                                                                  │  │
│            │  │  [🤖 AI: Suggest optimal config]                                │  │
│            │  └──────────────────────────────────────────────────────────────────┘  │
└────────────┴────────────────────────────────────────────────────────────────────────┘
```

## 8.2 Builder State Management

```typescript
// stores/useDashboardStore.ts

interface DashboardBuilderState {
  // Dashboard data
  dashboard: Dashboard | null;
  widgets: Widget[];
  
  // Edit state
  isEditing: boolean;
  isDirty: boolean;
  
  // Selection
  selectedWidgetId: string | null;
  
  // Clipboard
  copiedWidget: Widget | null;
  
  // History (undo/redo)
  history: HistoryEntry[];
  historyIndex: number;
  
  // Actions
  setDashboard: (dashboard: Dashboard) => void;
  addWidget: (widget: Omit<Widget, 'id'>) => void;
  updateWidget: (id: string, updates: Partial<Widget>) => void;
  removeWidget: (id: string) => void;
  moveWidget: (id: string, position: WidgetPosition) => void;
  resizeWidget: (id: string, size: { w: number; h: number }) => void;
  selectWidget: (id: string | null) => void;
  copyWidget: (id: string) => void;
  pasteWidget: () => void;
  undo: () => void;
  redo: () => void;
  save: () => Promise<void>;
}

export const useDashboardStore = create<DashboardBuilderState>()(
  devtools(
    immer((set, get) => ({
      dashboard: null,
      widgets: [],
      isEditing: false,
      isDirty: false,
      selectedWidgetId: null,
      copiedWidget: null,
      history: [],
      historyIndex: -1,
      
      addWidget: (widget) => {
        const newWidget = { ...widget, id: generateId() };
        set((state) => {
          state.widgets.push(newWidget);
          state.isDirty = true;
          state.selectedWidgetId = newWidget.id;
          pushHistory(state);
        });
      },
      
      updateWidget: (id, updates) => {
        set((state) => {
          const index = state.widgets.findIndex(w => w.id === id);
          if (index !== -1) {
            state.widgets[index] = { ...state.widgets[index], ...updates };
            state.isDirty = true;
            pushHistory(state);
          }
        });
      },
      
      // ... other actions
    }))
  )
);
```

## 8.3 Grid Layout System

```typescript
// components/builder/dashboard-canvas.tsx

import { DndContext, DragOverlay } from '@dnd-kit/core';
import { restrictToParentElement } from '@dnd-kit/modifiers';

interface DashboardCanvasProps {
  widgets: Widget[];
  isEditing: boolean;
  onWidgetMove: (id: string, position: WidgetPosition) => void;
  onWidgetResize: (id: string, size: { w: number; h: number }) => void;
}

export function DashboardCanvas({
  widgets,
  isEditing,
  onWidgetMove,
  onWidgetResize,
}: DashboardCanvasProps) {
  const [activeId, setActiveId] = useState<string | null>(null);
  const gridRef = useRef<HTMLDivElement>(null);
  
  const GRID_COLS = 12;
  const ROW_HEIGHT = 80;
  const GAP = 16;
  
  const handleDragEnd = (event: DragEndEvent) => {
    const { active, delta } = event;
    if (!gridRef.current) return;
    
    const widget = widgets.find(w => w.id === active.id);
    if (!widget) return;
    
    const gridRect = gridRef.current.getBoundingClientRect();
    const colWidth = (gridRect.width - GAP * (GRID_COLS - 1)) / GRID_COLS;
    
    const newX = Math.round((widget.position.x * colWidth + delta.x) / colWidth);
    const newY = Math.round((widget.position.y * ROW_HEIGHT + delta.y) / ROW_HEIGHT);
    
    onWidgetMove(widget.id, {
      ...widget.position,
      x: Math.max(0, Math.min(GRID_COLS - widget.position.w, newX)),
      y: Math.max(0, newY),
    });
    
    setActiveId(null);
  };
  
  return (
    <DndContext
      modifiers={[restrictToParentElement]}
      onDragStart={({ active }) => setActiveId(active.id as string)}
      onDragEnd={handleDragEnd}
    >
      <div
        ref={gridRef}
        className="relative min-h-[600px] bg-muted/30 rounded-lg p-4"
        style={{
          backgroundImage: isEditing
            ? `repeating-linear-gradient(
                0deg,
                transparent,
                transparent ${ROW_HEIGHT - 1}px,
                hsl(var(--border)) ${ROW_HEIGHT - 1}px,
                hsl(var(--border)) ${ROW_HEIGHT}px
              )`
            : 'none',
        }}
      >
        {widgets.map((widget) => (
          <WidgetContainer
            key={widget.id}
            widget={widget}
            isEditing={isEditing}
            gridCols={GRID_COLS}
            rowHeight={ROW_HEIGHT}
            gap={GAP}
            onResize={(size) => onWidgetResize(widget.id, size)}
          />
        ))}
      </div>
      
      <DragOverlay>
        {activeId && (
          <WidgetDragPreview
            widget={widgets.find(w => w.id === activeId)!}
          />
        )}
      </DragOverlay>
    </DndContext>
  );
}
```

## 8.4 Widget Palette

```typescript
// components/builder/widget-palette.tsx

export function WidgetPalette() {
  const { addWidget } = useDashboardStore();
  
  return (
    <div className="space-y-4">
      {Object.entries(WIDGET_CATEGORIES).map(([key, category]) => (
        <Collapsible key={key} defaultOpen>
          <CollapsibleTrigger className="flex items-center gap-2 w-full p-2 hover:bg-muted rounded-md">
            <category.icon className="h-4 w-4" />
            <span className="font-medium">{category.name}</span>
            <ChevronDown className="h-4 w-4 ml-auto" />
          </CollapsibleTrigger>
          <CollapsibleContent className="pl-6 space-y-1">
            {Object.values(WIDGET_REGISTRY)
              .filter(w => w.category === key)
              .map((widget) => (
                <button
                  key={widget.type}
                  className="flex items-center gap-2 w-full p-2 text-sm hover:bg-muted rounded-md"
                  onClick={() => addWidget({
                    type: widget.type,
                    title: widget.name,
                    position: findEmptyPosition(widget.defaultSize),
                    dataSource: { type: widget.dataSourceTypes[0] },
                    config: widget.defaultConfig,
                  })}
                >
                  <widget.icon className="h-4 w-4" />
                  <span>{widget.name}</span>
                </button>
              ))}
          </CollapsibleContent>
        </Collapsible>
      ))}
    </div>
  );
}
```

## 8.5 Property Panel

```typescript
// components/builder/property-panel.tsx

export function PropertyPanel() {
  const { selectedWidgetId, widgets, updateWidget } = useDashboardStore();
  
  const widget = widgets.find(w => w.id === selectedWidgetId);
  
  if (!widget) {
    return (
      <div className="p-4 text-center text-muted-foreground">
        Select a widget to edit its properties
      </div>
    );
  }
  
  const definition = WIDGET_REGISTRY[widget.type];
  const ConfigComponent = definition.configComponent;
  
  return (
    <ScrollArea className="h-full">
      <div className="p-4 space-y-6">
        {/* Title */}
        <div className="space-y-2">
          <Label>Title</Label>
          <Input
            value={widget.title}
            onChange={(e) => updateWidget(widget.id, { title: e.target.value })}
          />
        </div>
        
        {/* Data Source */}
        <DataSourceConfig
          dataSource={widget.dataSource}
          allowedTypes={definition.dataSourceTypes}
          onChange={(dataSource) => updateWidget(widget.id, { dataSource })}
        />
        
        {/* Widget-specific config */}
        <ConfigComponent
          config={widget.config}
          onChange={(config) => updateWidget(widget.id, { config })}
        />
        
        {/* AI Suggestions */}
        <div className="pt-4 border-t">
          <Button
            variant="outline"
            className="w-full"
            onClick={() => getAISuggestions(widget)}
          >
            <Sparkles className="h-4 w-4 mr-2" />
            AI: Suggest optimal config
          </Button>
        </div>
      </div>
    </ScrollArea>
  );
}
```
# 7. AI Features Specification

## 7.1 AI Features Overview

| Feature | Description | Priority |
|---------|-------------|----------|
| Natural Language Dashboard Builder | Create dashboards by describing what you need | Must Have |
| Natural Language Data Queries | Ask questions about your data in plain English | Must Have |
| Anomaly Detection | Automatic detection with AI explanations | Must Have |
| Alert Summarization | Daily digest with grouped alerts and insights | Must Have |
| Predictive Maintenance | Predict equipment failures before they happen | Must Have |
| Auto-Configuration | Suggest optimal settings for new devices | Must Have |
| Smart Widget Suggestions | Recommend widgets based on data patterns | Must Have |

**AI Autonomy Rule:** All AI suggestions require user approval before being applied.

## 7.2 Natural Language Dashboard Builder

### Example Flow

```
User: "Create a dashboard showing temperature and humidity from all sensors 
       in Production Line 1, with alerts when temperature > 35°C"

                    ↓ Intent Recognition
                    
Action: Create dashboard
Entities: temperature, humidity sensors
Location: Production Line 1
Additional: Alert rule (temperature > 35°C)

                    ↓ Context Gathering
                    
Query device profiles → Find matching devices → Get telemetry keys

                    ↓ Schema Generation (Claude API)
                    
Generate dashboard config with widgets + alert rules

                    ↓ Preview & Confirmation
                    
Show preview → [Apply] [Modify] [Cancel]
```

### Claude API Prompt Template

```
You are an IoT dashboard configuration assistant.
Generate dashboard configurations in JSON format.

Available device profiles: {deviceProfiles}
Location hierarchy: {locations}
Telemetry keys: {telemetryKeys}

Output: { dashboard: {...}, alertRules: [...], explanation: "..." }
```

## 7.3 Natural Language Data Queries

### Example Queries

| User Query | Generated Action |
|------------|------------------|
| "What was the average temperature last week?" | SQL query + value display |
| "Show me power consumption by building" | SQL query + bar chart |
| "Which devices had the most alerts yesterday?" | SQL query + table |
| "Compare humidity between Building A and B" | SQL query + comparison chart |

## 7.4 Anomaly Detection

### Methods

| Method | Use Case |
|--------|----------|
| Z-Score | Point anomalies (values far from mean) |
| IQR | Outlier detection |
| Moving Average | Trend deviations |
| Seasonal | Periodic pattern anomalies |

### Implementation

```typescript
// Z-Score based anomaly detection
function detectAnomalies(data, sensitivity = 3) {
  const mean = average(data);
  const stddev = standardDeviation(data);
  
  return data.filter(value => {
    const zscore = Math.abs((value - mean) / stddev);
    return zscore > sensitivity;
  });
}
```

### AI Explanation

For each detected anomaly, Claude generates:
1. Likely cause (1-2 sentences)
2. Recommended action (1-2 sentences)

## 7.5 Alert Summarization

### Daily Digest Format

```
📧 IoT Dashboard - Daily Alert Summary
January 10, 2026

🔴 CRITICAL ISSUES (2)
─────────────────────
1. Production Line 3 - Motor Temperature
   Exceeded 85°C for 45 minutes
   → Recommended: Schedule maintenance inspection

🟡 WARNINGS (12)
─────────────────
• Power fluctuations in Building A (8 events)
  Pattern: HVAC cycling issue suspected

📊 SYSTEM HEALTH: 94%
─────────────────────
• Devices Online: 847/862
• Data Quality: 99.2%
```

## 7.6 Auto-Configuration

When a new device is added, AI analyzes:
- Device type and profile
- Historical data from similar devices
- Existing alert rules

And suggests:
- Optimal alert thresholds
- Recommended dashboard widgets
- Aggregation settings

## 7.7 AI Approval Flow

All AI suggestions show:
1. Confidence score (0-100%)
2. Explanation of what will be created/changed
3. Preview of the result
4. Action buttons: [Apply] [Modify] [Reject]

```typescript
interface AISuggestion {
  type: 'dashboard' | 'alert' | 'config' | 'widget';
  suggestion: any;
  explanation: string;
  confidence: number; // 0-1
  onApprove: () => void;
  onModify: () => void;
  onReject: () => void;
}
```
# 10. Device Simulator (Standalone Tool)

## 10.1 Overview

The Device Simulator is a standalone tool for generating realistic IoT telemetry data for testing and demonstration purposes. It runs independently from the main platform and can simulate thousands of devices with various behaviors.

## 10.2 Simulator Architecture

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                           DEVICE SIMULATOR                                           │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                         Simulator Web UI                                     │    │
│  │                                                                              │    │
│  │  ┌───────────────────────────────────────────────────────────────────────┐  │    │
│  │  │  Simulation Control Panel                                              │  │    │
│  │  │                                                                        │  │    │
│  │  │  [+ New Simulation]  [Import Config]  [Export Config]                 │  │    │
│  │  │                                                                        │  │    │
│  │  │  ┌────────────────────────────────────────────────────────────────┐   │  │    │
│  │  │  │ Simulation: Smart Factory          Status: ▶ Running          │   │  │    │
│  │  │  │ Devices: 880    Messages/sec: 15,420    Data: 14.2 MB/s       │   │  │    │
│  │  │  │ [Pause] [Stop] [Configure] [Inject Anomaly]                   │   │  │    │
│  │  │  └────────────────────────────────────────────────────────────────┘   │  │    │
│  │  │                                                                        │  │    │
│  │  │  ┌────────────────────────────────────────────────────────────────┐   │  │    │
│  │  │  │ Simulation: Smart Building         Status: ⏸ Paused           │   │  │    │
│  │  │  │ Devices: 1,100  Messages/sec: 0         Data: 0 MB/s          │   │  │    │
│  │  │  │ [Resume] [Stop] [Configure] [Inject Anomaly]                  │   │  │    │
│  │  │  └────────────────────────────────────────────────────────────────┘   │  │    │
│  │  └───────────────────────────────────────────────────────────────────────┘  │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                         Simulator Engine                                     │    │
│  │                                                                              │    │
│  │  ┌───────────────┐  ┌───────────────┐  ┌───────────────┐                    │    │
│  │  │  Simulation   │  │   Device      │  │   Scenario    │                    │    │
│  │  │  Manager      │  │   Factory     │  │   Engine      │                    │    │
│  │  └───────────────┘  └───────────────┘  └───────────────┘                    │    │
│  │                                                                              │    │
│  │  ┌───────────────┐  ┌───────────────┐  ┌───────────────┐                    │    │
│  │  │   Data        │  │   Protocol    │  │   Metrics     │                    │    │
│  │  │   Generator   │  │   Adapters    │  │   Collector   │                    │    │
│  │  └───────────────┘  └───────────────┘  └───────────────┘                    │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                         Protocol Adapters                                    │    │
│  │                                                                              │    │
│  │  ┌───────────────┐  ┌───────────────┐  ┌───────────────┐                    │    │
│  │  │     MQTT      │  │     HTTP      │  │     CoAP      │                    │    │
│  │  │   Publisher   │  │   Sender      │  │   Client      │                    │    │
│  │  └───────────────┘  └───────────────┘  └───────────────┘                    │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

## 10.3 Pre-built Simulation Templates

### Template 1: Smart Factory

| Category | Device Type | Count | Total |
|----------|-------------|-------|-------|
| Production Lines (4) | Industrial Motor | 40 | |
| | Temperature Sensor | 80 | |
| | Pressure Sensor | 40 | |
| | Flow Meter | 20 | |
| | Power Meter | 20 | |
| Quality Control | Air Quality Sensor | 10 | |
| Warehouse | Humidity Sensor | 40 | |
| | Occupancy Sensor | 20 | |
| Infrastructure | IoT Gateway | 10 | |
| | | | **880** |

**Data Generation:**
- Messages per second: ~15,000
- Data throughput: ~14 MB/s
- Telemetry interval: 500ms - 5s depending on device type

### Template 2: Smart Building

| Category | Device Type | Count | Total |
|----------|-------------|-------|-------|
| HVAC (50 zones) | HVAC Unit | 50 | |
| | Temperature Sensor | 200 | |
| | Humidity Sensor | 100 | |
| Lighting | Lighting Controller | 200 | |
| Security | Occupancy Sensor | 100 | |
| Energy | Power Meter | 100 | |
| Air Quality | Air Quality Sensor | 50 | |
| Infrastructure | IoT Gateway | 20 | |
| | | | **1,100** |

### Template 3: Fleet Management

| Category | Device Type | Count | Total |
|----------|-------------|-------|-------|
| Vehicles | Vehicle GPS | 200 | |
| | Vehicle OBD | 200 | |
| Trailers | Temperature Sensor | 100 | |
| Infrastructure | IoT Gateway | 20 | |
| | | | **520** |

### Template 4: Agriculture

| Category | Device Type | Count | Total |
|----------|-------------|-------|-------|
| Fields (10) | Soil Sensor | 200 | |
| | Weather Station | 20 | |
| | Humidity Sensor | 100 | |
| Irrigation | Flow Meter | 50 | |
| Infrastructure | IoT Gateway | 30 | |
| | | | **600** |

## 10.4 Data Generation Patterns

### Generator Types

```typescript
// simulator/generators/index.ts

export type GeneratorType =
  | 'constant'      // Fixed value
  | 'random'        // Random within range
  | 'gaussian'      // Normal distribution
  | 'sine'          // Sinusoidal pattern
  | 'trend'         // Linear trend over time
  | 'step'          // Step changes at intervals
  | 'schedule'      // Time-based schedule
  | 'correlated'    // Correlated with another key
  | 'accumulator'   // Cumulative value
  | 'replay'        // Replay from file
  | 'gps_path';     // GPS coordinate path

interface GeneratorConfig {
  type: GeneratorType;
  // Type-specific parameters
  [key: string]: any;
}
```

### Generator Examples

```typescript
// Constant value
{ type: 'constant', value: 22 }

// Random within range
{ type: 'random', min: 20, max: 30, decimals: 1 }

// Gaussian distribution
{ type: 'gaussian', mean: 25, stddev: 3, min: 15, max: 35 }

// Sinusoidal (temperature varying through day)
{ type: 'sine', base: 25, amplitude: 5, period: 86400, phase: -6 }

// Linear trend (battery draining)
{ type: 'trend', start: 100, end: 0, duration: 86400 * 7 }

// Step changes (motor RPM)
{ 
  type: 'step', 
  values: [0, 1500, 3000, 1500, 0], 
  durations: [60, 300, 300, 60] 
}

// Time-based schedule (occupancy)
{ 
  type: 'schedule', 
  schedule: { 
    '08:00': true, 
    '12:00': false, 
    '13:00': true, 
    '18:00': false 
  }
}

// Correlated with another value
{ 
  type: 'correlated', 
  baseKey: 'rpm', 
  factor: 0.02, 
  offset: 25, 
  noise: 0.5,
  lag: 30 
}

// Cumulative (energy meter)
{ type: 'accumulator', rateKey: 'power', factor: 1/3600 }

// GPS path simulation
{ 
  type: 'gps_path', 
  startLat: 1.3521, 
  startLng: 103.8198, 
  pathType: 'random_walk',
  speedKmh: 40 
}
```

## 10.5 Anomaly Injection

### Predefined Scenarios

```typescript
// simulator/scenarios/anomalies.ts

export const ANOMALY_SCENARIOS = {
  temperature_spike: {
    name: 'Temperature Spike',
    description: 'Sudden temperature increase',
    duration: 300, // 5 minutes
    targetProfiles: ['temperature_sensor', 'industrial_motor'],
    effects: [{
      key: 'temperature',
      modification: { type: 'multiply', factor: 1.5 }
    }],
  },
  
  sensor_offline: {
    name: 'Sensor Offline',
    description: 'Device stops sending data',
    duration: 600, // 10 minutes
    targetProfiles: ['*'],
    effects: [{
      modification: { type: 'offline' }
    }],
  },
  
  gradual_degradation: {
    name: 'Equipment Degradation',
    description: 'Gradual performance decline',
    duration: 86400, // 24 hours
    targetProfiles: ['industrial_motor'],
    effects: [
      { key: 'vibration', modification: { type: 'trend', factor: 2 } },
      { key: 'temperature', modification: { type: 'trend', factor: 1.3 } },
    ],
  },
  
  power_fluctuation: {
    name: 'Power Fluctuation',
    description: 'Unstable power supply',
    duration: 60,
    targetProfiles: ['power_meter'],
    effects: [{
      key: 'voltage',
      modification: { type: 'oscillate', amplitude: 20, frequency: 2 }
    }],
  },
  
  data_drift: {
    name: 'Sensor Drift',
    description: 'Gradual calibration drift',
    duration: 86400 * 7, // 1 week
    targetProfiles: ['temperature_sensor', 'pressure_sensor'],
    effects: [{
      key: '*',
      modification: { type: 'drift', rate: 0.01 }
    }],
  },
  
  network_latency: {
    name: 'Network Latency',
    description: 'Delayed data transmission',
    duration: 1800, // 30 minutes
    targetProfiles: ['*'],
    effects: [{
      modification: { type: 'delay', minMs: 5000, maxMs: 30000 }
    }],
  },
};
```

## 10.6 Simulator Implementation

### Core Classes

```typescript
// simulator/core/simulation.ts

export class Simulation {
  id: string;
  name: string;
  status: 'running' | 'paused' | 'stopped';
  devices: SimulatedDevice[];
  config: SimulationConfig;
  metrics: SimulationMetrics;
  
  private intervalId?: NodeJS.Timeout;
  private protocolAdapter: ProtocolAdapter;
  
  constructor(config: SimulationConfig) {
    this.id = generateId();
    this.name = config.name;
    this.status = 'stopped';
    this.config = config;
    this.devices = [];
    this.metrics = {
      messagesPerSecond: 0,
      bytesPerSecond: 0,
      totalMessages: 0,
      errors: 0,
    };
    
    this.protocolAdapter = createProtocolAdapter(config.protocol);
  }
  
  async start() {
    if (this.status === 'running') return;
    
    // Connect to broker/endpoint
    await this.protocolAdapter.connect(this.config.connection);
    
    // Create devices
    this.devices = createDevicesFromTemplate(this.config.template);
    
    // Start generation loop
    this.status = 'running';
    this.runLoop();
  }
  
  private runLoop() {
    const tickMs = 100; // 100ms tick rate
    
    this.intervalId = setInterval(async () => {
      if (this.status !== 'running') return;
      
      const now = Date.now();
      const messages: TelemetryMessage[] = [];
      
      for (const device of this.devices) {
        if (device.shouldSend(now)) {
          const telemetry = device.generateTelemetry(now);
          messages.push({
            deviceId: device.id,
            accessToken: device.accessToken,
            ...telemetry,
          });
        }
      }
      
      if (messages.length > 0) {
        await this.protocolAdapter.sendBatch(messages);
        this.updateMetrics(messages);
      }
    }, tickMs);
  }
  
  pause() {
    this.status = 'paused';
  }
  
  resume() {
    this.status = 'running';
  }
  
  async stop() {
    this.status = 'stopped';
    if (this.intervalId) {
      clearInterval(this.intervalId);
    }
    await this.protocolAdapter.disconnect();
  }
  
  injectAnomaly(scenario: AnomalyScenario, targetDeviceIds?: string[]) {
    const targets = targetDeviceIds
      ? this.devices.filter(d => targetDeviceIds.includes(d.id))
      : this.devices.filter(d => 
          scenario.targetProfiles.includes('*') ||
          scenario.targetProfiles.includes(d.profileType)
        );
    
    for (const device of targets) {
      device.applyAnomaly(scenario);
    }
    
    // Schedule anomaly removal
    setTimeout(() => {
      for (const device of targets) {
        device.clearAnomaly();
      }
    }, scenario.duration * 1000);
  }
}
```

### Simulated Device

```typescript
// simulator/core/device.ts

export class SimulatedDevice {
  id: string;
  name: string;
  profileType: string;
  accessToken: string;
  generators: Map<string, DataGenerator>;
  lastSendTime: number = 0;
  sendInterval: number;
  activeAnomaly?: AnomalyScenario;
  
  constructor(config: DeviceConfig) {
    this.id = config.id || generateId();
    this.name = config.name;
    this.profileType = config.profileType;
    this.accessToken = config.accessToken || generateToken();
    this.sendInterval = config.sendInterval;
    
    this.generators = new Map();
    for (const key of config.telemetryKeys) {
      this.generators.set(key.key, createGenerator(key.generator));
    }
  }
  
  shouldSend(now: number): boolean {
    return now - this.lastSendTime >= this.sendInterval;
  }
  
  generateTelemetry(now: number): { ts: number; values: Record<string, any> } {
    this.lastSendTime = now;
    
    const values: Record<string, any> = {};
    
    for (const [key, generator] of this.generators) {
      let value = generator.generate(now);
      
      // Apply anomaly modification if active
      if (this.activeAnomaly) {
        value = this.applyAnomalyEffect(key, value);
      }
      
      values[key] = value;
    }
    
    return { ts: now, values };
  }
  
  applyAnomaly(scenario: AnomalyScenario) {
    this.activeAnomaly = scenario;
  }
  
  clearAnomaly() {
    this.activeAnomaly = undefined;
  }
  
  private applyAnomalyEffect(key: string, value: any): any {
    if (!this.activeAnomaly) return value;
    
    for (const effect of this.activeAnomaly.effects) {
      if (effect.key === '*' || effect.key === key) {
        switch (effect.modification.type) {
          case 'multiply':
            return value * effect.modification.factor;
          case 'add':
            return value + effect.modification.offset;
          case 'offline':
            return null; // Will skip sending
          default:
            return value;
        }
      }
    }
    
    return value;
  }
}
```

### Protocol Adapters

```typescript
// simulator/adapters/mqtt.ts

export class MQTTAdapter implements ProtocolAdapter {
  private client: mqtt.MqttClient | null = null;
  
  async connect(config: ConnectionConfig) {
    this.client = mqtt.connect(config.brokerUrl, {
      username: config.username,
      password: config.password,
    });
    
    return new Promise<void>((resolve, reject) => {
      this.client!.on('connect', () => resolve());
      this.client!.on('error', (err) => reject(err));
    });
  }
  
  async sendBatch(messages: TelemetryMessage[]) {
    if (!this.client) throw new Error('Not connected');
    
    const promises = messages.map(msg => {
      const topic = `devices/${msg.deviceId}/telemetry`;
      const payload = JSON.stringify({ ts: msg.ts, values: msg.values });
      
      return new Promise<void>((resolve, reject) => {
        this.client!.publish(topic, payload, { qos: 1 }, (err) => {
          if (err) reject(err);
          else resolve();
        });
      });
    });
    
    await Promise.all(promises);
  }
  
  async disconnect() {
    if (this.client) {
      this.client.end();
      this.client = null;
    }
  }
}

// simulator/adapters/http.ts

export class HTTPAdapter implements ProtocolAdapter {
  private baseUrl: string = '';
  
  async connect(config: ConnectionConfig) {
    this.baseUrl = config.httpEndpoint;
  }
  
  async sendBatch(messages: TelemetryMessage[]) {
    const promises = messages.map(msg =>
      fetch(`${this.baseUrl}/api/webhook/telemetry`, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Authorization': `Bearer ${msg.accessToken}`,
        },
        body: JSON.stringify({ ts: msg.ts, values: msg.values }),
      })
    );
    
    await Promise.all(promises);
  }
  
  async disconnect() {
    // No persistent connection
  }
}
```

## 10.7 Simulator Web UI

```typescript
// simulator/web/pages/index.tsx

export default function SimulatorDashboard() {
  const [simulations, setSimulations] = useState<Simulation[]>([]);
  const [metrics, setMetrics] = useState<GlobalMetrics>({
    totalDevices: 0,
    messagesPerSecond: 0,
    bytesPerSecond: 0,
  });
  
  return (
    <div className="container mx-auto p-6">
      <header className="flex justify-between items-center mb-8">
        <div>
          <h1 className="text-2xl font-bold">IoT Device Simulator</h1>
          <p className="text-muted-foreground">
            Generate realistic IoT telemetry for testing
          </p>
        </div>
        <div className="flex gap-2">
          <Button onClick={() => setShowNewDialog(true)}>
            <Plus className="h-4 w-4 mr-2" />
            New Simulation
          </Button>
          <Button variant="outline" onClick={handleImport}>
            <Upload className="h-4 w-4 mr-2" />
            Import
          </Button>
        </div>
      </header>
      
      {/* Global Metrics */}
      <div className="grid grid-cols-4 gap-4 mb-8">
        <MetricCard
          title="Total Devices"
          value={metrics.totalDevices}
          icon={Cpu}
        />
        <MetricCard
          title="Messages/sec"
          value={metrics.messagesPerSecond.toLocaleString()}
          icon={Activity}
        />
        <MetricCard
          title="Data Rate"
          value={formatBytes(metrics.bytesPerSecond) + '/s'}
          icon={ArrowUpDown}
        />
        <MetricCard
          title="Active Simulations"
          value={simulations.filter(s => s.status === 'running').length}
          icon={Play}
        />
      </div>
      
      {/* Simulation List */}
      <div className="space-y-4">
        {simulations.map(sim => (
          <SimulationCard
            key={sim.id}
            simulation={sim}
            onStart={() => sim.start()}
            onPause={() => sim.pause()}
            onStop={() => sim.stop()}
            onInjectAnomaly={(scenario) => sim.injectAnomaly(scenario)}
          />
        ))}
      </div>
      
      <NewSimulationDialog
        open={showNewDialog}
        onClose={() => setShowNewDialog(false)}
        onCreate={handleCreateSimulation}
      />
    </div>
  );
}
```
# 11. Dashboard Templates

## 11.1 Template Categories

| Category | Use Case | Templates |
|----------|----------|-----------|
| Industrial | Manufacturing, factory monitoring | Factory Floor, Production Line, Quality Control |
| Building | Building automation, facilities | Building Overview, HVAC, Energy Management |
| Environmental | Weather, air quality | Environmental Monitoring, Weather Station |
| Fleet | Vehicle tracking, logistics | Fleet Overview, Vehicle Details |
| Energy | Power, utilities | Energy Dashboard, Power Quality |
| Equipment | Asset monitoring | Equipment Health, Predictive Maintenance |

## 11.2 Template: Factory Floor Monitoring

```json
{
  "name": "Factory Floor Monitoring",
  "description": "Real-time monitoring of industrial equipment and production metrics",
  "category": "industrial",
  "thumbnail": "/templates/factory-floor.png",
  "widgets": [
    {
      "type": "stats_card",
      "title": "Active Machines",
      "position": { "x": 0, "y": 0, "w": 3, "h": 1 },
      "dataSource": {
        "type": "devices",
        "filter": { "profileId": "industrial_motor", "status": "active" }
      },
      "config": { "icon": "cog", "color": "green" }
    },
    {
      "type": "stats_card",
      "title": "Active Alerts",
      "position": { "x": 3, "y": 0, "w": 3, "h": 1 },
      "dataSource": {
        "type": "alerts",
        "filter": { "status": "active" }
      },
      "config": { "icon": "alert-triangle", "color": "red" }
    },
    {
      "type": "gauge",
      "title": "Avg Temperature",
      "position": { "x": 6, "y": 0, "w": 3, "h": 2 },
      "dataSource": {
        "type": "latest",
        "deviceProfileId": "temperature_sensor",
        "keys": ["temperature"],
        "aggregation": "avg"
      },
      "config": {
        "min": 0,
        "max": 60,
        "unit": "°C",
        "thresholds": [
          { "value": 40, "color": "yellow" },
          { "value": 50, "color": "red" }
        ]
      }
    },
    {
      "type": "gauge",
      "title": "Avg Humidity",
      "position": { "x": 9, "y": 0, "w": 3, "h": 2 },
      "dataSource": {
        "type": "latest",
        "deviceProfileId": "humidity_sensor",
        "keys": ["humidity"],
        "aggregation": "avg"
      },
      "config": {
        "min": 0,
        "max": 100,
        "unit": "%",
        "thresholds": [
          { "value": 70, "color": "yellow" },
          { "value": 85, "color": "red" }
        ]
      }
    },
    {
      "type": "line_chart",
      "title": "Motor Performance Trend",
      "position": { "x": 0, "y": 1, "w": 6, "h": 3 },
      "dataSource": {
        "type": "timeseries",
        "deviceProfileId": "industrial_motor",
        "keys": ["rpm", "current", "temperature"],
        "timeRange": { "type": "relative", "value": "24h" },
        "interval": "5m",
        "aggregation": "avg"
      },
      "config": {
        "showLegend": true,
        "showGrid": true
      }
    },
    {
      "type": "alarm_table",
      "title": "Active Alerts",
      "position": { "x": 0, "y": 4, "w": 6, "h": 2 },
      "dataSource": {
        "type": "alerts",
        "filter": { "status": ["active", "acknowledged"] }
      },
      "config": {
        "columns": ["severity", "device", "message", "time", "actions"],
        "pageSize": 5
      }
    },
    {
      "type": "device_map",
      "title": "Equipment Layout",
      "position": { "x": 6, "y": 2, "w": 6, "h": 4 },
      "dataSource": {
        "type": "devices",
        "filter": { "profileId": ["industrial_motor", "temperature_sensor"] }
      },
      "config": {
        "mapStyle": "light",
        "showStatusColors": true,
        "clusterDevices": false
      }
    }
  ]
}
```

## 11.3 Template: Smart Building Overview

```json
{
  "name": "Smart Building Overview",
  "description": "Building automation and environmental monitoring dashboard",
  "category": "building",
  "widgets": [
    {
      "type": "value_card",
      "title": "Current Occupancy",
      "position": { "x": 0, "y": 0, "w": 2, "h": 1 },
      "dataSource": {
        "type": "latest",
        "deviceProfileId": "occupancy_sensor",
        "keys": ["count"],
        "aggregation": "sum"
      },
      "config": { "unit": "people", "icon": "users" }
    },
    {
      "type": "value_card",
      "title": "Power Usage",
      "position": { "x": 2, "y": 0, "w": 2, "h": 1 },
      "dataSource": {
        "type": "latest",
        "deviceProfileId": "power_meter",
        "keys": ["power"],
        "aggregation": "sum"
      },
      "config": { "unit": "kW", "icon": "zap" }
    },
    {
      "type": "gauge",
      "title": "Avg Temperature",
      "position": { "x": 4, "y": 0, "w": 2, "h": 2 },
      "dataSource": {
        "type": "latest",
        "deviceProfileId": "hvac_unit",
        "keys": ["supply_temp"],
        "aggregation": "avg"
      },
      "config": { "min": 16, "max": 30, "unit": "°C" }
    },
    {
      "type": "gauge",
      "title": "Avg CO2",
      "position": { "x": 6, "y": 0, "w": 2, "h": 2 },
      "dataSource": {
        "type": "latest",
        "deviceProfileId": "air_quality_sensor",
        "keys": ["co2"],
        "aggregation": "avg"
      },
      "config": {
        "min": 400,
        "max": 2000,
        "unit": "ppm",
        "thresholds": [
          { "value": 1000, "color": "yellow" },
          { "value": 1500, "color": "red" }
        ]
      }
    },
    {
      "type": "bar_chart",
      "title": "Energy by Floor",
      "position": { "x": 8, "y": 0, "w": 4, "h": 2 },
      "dataSource": {
        "type": "latest",
        "deviceProfileId": "power_meter",
        "keys": ["energy"],
        "groupBy": "floor"
      },
      "config": { "orientation": "horizontal" }
    },
    {
      "type": "line_chart",
      "title": "Temperature & Humidity Trend",
      "position": { "x": 0, "y": 2, "w": 6, "h": 3 },
      "dataSource": {
        "type": "timeseries",
        "deviceProfileId": "hvac_unit",
        "keys": ["supply_temp", "return_temp"],
        "timeRange": { "type": "relative", "value": "24h" },
        "interval": "15m"
      }
    },
    {
      "type": "line_chart",
      "title": "Air Quality Trend",
      "position": { "x": 6, "y": 2, "w": 6, "h": 3 },
      "dataSource": {
        "type": "timeseries",
        "deviceProfileId": "air_quality_sensor",
        "keys": ["co2", "pm25"],
        "timeRange": { "type": "relative", "value": "24h" },
        "interval": "15m"
      }
    }
  ]
}
```

## 11.4 Template: Fleet Overview

```json
{
  "name": "Fleet Overview",
  "description": "Vehicle tracking and fleet management dashboard",
  "category": "fleet",
  "widgets": [
    {
      "type": "stats_card",
      "title": "Vehicles Moving",
      "position": { "x": 0, "y": 0, "w": 2, "h": 1 },
      "dataSource": {
        "type": "devices",
        "filter": {
          "profileId": "vehicle_gps",
          "telemetry": { "speed": { "gt": 0 } }
        }
      }
    },
    {
      "type": "stats_card",
      "title": "Vehicles Idle",
      "position": { "x": 2, "y": 0, "w": 2, "h": 1 },
      "dataSource": {
        "type": "devices",
        "filter": {
          "profileId": "vehicle_gps",
          "telemetry": { "speed": { "eq": 0 } }
        }
      }
    },
    {
      "type": "device_map",
      "title": "Live Vehicle Locations",
      "position": { "x": 0, "y": 1, "w": 8, "h": 5 },
      "dataSource": {
        "type": "devices",
        "filter": { "profileId": "vehicle_gps" }
      },
      "config": {
        "mapStyle": "streets",
        "showStatusColors": true,
        "clusterDevices": true,
        "popupFields": ["name", "speed", "driver"]
      }
    },
    {
      "type": "device_table",
      "title": "Vehicle Status",
      "position": { "x": 8, "y": 0, "w": 4, "h": 3 },
      "dataSource": {
        "type": "devices",
        "filter": { "profileId": "vehicle_gps" }
      },
      "config": {
        "columns": ["name", "speed", "fuel_level", "status"],
        "pageSize": 10
      }
    },
    {
      "type": "alarm_table",
      "title": "Vehicle Alerts",
      "position": { "x": 8, "y": 3, "w": 4, "h": 3 },
      "dataSource": {
        "type": "alerts",
        "filter": {
          "deviceProfileId": ["vehicle_gps", "vehicle_obd"],
          "status": "active"
        }
      }
    }
  ]
}
```

## 11.5 Template: Equipment Health

```json
{
  "name": "Equipment Health",
  "description": "Predictive maintenance and equipment monitoring",
  "category": "industrial",
  "widgets": [
    {
      "type": "stats_card",
      "title": "Healthy",
      "position": { "x": 0, "y": 0, "w": 2, "h": 1 },
      "dataSource": {
        "type": "devices",
        "filter": { "health": "good" }
      },
      "config": { "color": "green" }
    },
    {
      "type": "stats_card",
      "title": "Warning",
      "position": { "x": 2, "y": 0, "w": 2, "h": 1 },
      "dataSource": {
        "type": "devices",
        "filter": { "health": "warning" }
      },
      "config": { "color": "yellow" }
    },
    {
      "type": "stats_card",
      "title": "Critical",
      "position": { "x": 4, "y": 0, "w": 2, "h": 1 },
      "dataSource": {
        "type": "devices",
        "filter": { "health": "critical" }
      },
      "config": { "color": "red" }
    },
    {
      "type": "anomaly_chart",
      "title": "Vibration Analysis",
      "position": { "x": 0, "y": 1, "w": 6, "h": 3 },
      "dataSource": {
        "type": "timeseries",
        "deviceProfileId": "industrial_motor",
        "keys": ["vibration"],
        "timeRange": { "type": "relative", "value": "7d" }
      },
      "config": {
        "showAnomalies": true,
        "anomalyMethod": "zscore",
        "sensitivity": "medium"
      }
    },
    {
      "type": "ai_insight",
      "title": "Maintenance Predictions",
      "position": { "x": 6, "y": 1, "w": 6, "h": 3 },
      "dataSource": {
        "type": "ai",
        "insightType": "predictive_maintenance",
        "deviceProfileId": "industrial_motor"
      }
    },
    {
      "type": "device_table",
      "title": "Equipment Status",
      "position": { "x": 0, "y": 4, "w": 12, "h": 2 },
      "dataSource": {
        "type": "devices",
        "filter": { "profileId": "industrial_motor" }
      },
      "config": {
        "columns": ["name", "rpm", "temperature", "vibration", "health", "last_maintenance"],
        "sortBy": "health"
      }
    }
  ]
}
```

---

# 12. Project Structure

```
iot-dashboard/
├── app/                                # Next.js App Router
│   ├── (auth)/                        # Auth pages (no main layout)
│   │   ├── login/page.tsx
│   │   ├── register/page.tsx
│   │   ├── setup/page.tsx             # New user tenant setup
│   │   └── layout.tsx
│   │
│   ├── (dashboard)/                   # Main app (with layout)
│   │   ├── layout.tsx                 # App shell with sidebar
│   │   ├── page.tsx                   # Overview/Home
│   │   │
│   │   ├── dashboards/
│   │   │   ├── page.tsx               # Dashboard list
│   │   │   ├── new/page.tsx           # Create dashboard
│   │   │   └── [id]/
│   │   │       ├── page.tsx           # View dashboard
│   │   │       └── edit/page.tsx      # Edit dashboard (builder)
│   │   │
│   │   ├── devices/
│   │   │   ├── page.tsx               # Device list
│   │   │   ├── new/page.tsx           # Add device
│   │   │   └── [id]/page.tsx          # Device details
│   │   │
│   │   ├── alerts/
│   │   │   ├── page.tsx               # Alert list
│   │   │   └── rules/page.tsx         # Alert rules
│   │   │
│   │   ├── hierarchy/
│   │   │   └── page.tsx               # Site > Building > Floor > Area
│   │   │
│   │   ├── ai/
│   │   │   ├── assistant/page.tsx     # AI Chat interface
│   │   │   └── insights/page.tsx      # AI Insights dashboard
│   │   │
│   │   └── settings/
│   │       ├── page.tsx               # General settings
│   │       ├── users/page.tsx         # User management
│   │       ├── roles/page.tsx         # Role management
│   │       ├── profiles/page.tsx      # Device profiles
│   │       ├── api-keys/page.tsx      # API key management
│   │       └── export/page.tsx        # Data export
│   │
│   ├── public/[token]/                # Public dashboard view
│   │   └── page.tsx
│   │
│   └── api/                           # API Routes
│       ├── auth/[...nextauth]/route.ts
│       ├── trpc/[trpc]/route.ts
│       ├── v1/                        # REST API
│       │   ├── devices/route.ts
│       │   ├── telemetry/route.ts
│       │   ├── dashboards/route.ts
│       │   ├── alerts/route.ts
│       │   └── export/route.ts
│       ├── realtime/route.ts          # Socket.io upgrade
│       ├── webhook/telemetry/route.ts # Device telemetry webhook
│       └── ai/
│           ├── query/route.ts
│           ├── dashboard/route.ts
│           └── insights/route.ts
│
├── components/
│   ├── ui/                            # shadcn/ui components
│   │   ├── button.tsx
│   │   ├── card.tsx
│   │   ├── dialog.tsx
│   │   ├── dropdown-menu.tsx
│   │   ├── input.tsx
│   │   ├── select.tsx
│   │   ├── table.tsx
│   │   └── ...
│   │
│   ├── layout/                        # Layout components
│   │   ├── app-shell.tsx
│   │   ├── sidebar.tsx
│   │   ├── header.tsx
│   │   ├── page-header.tsx
│   │   └── breadcrumb.tsx
│   │
│   ├── widgets/                       # Dashboard widgets
│   │   ├── base/
│   │   │   ├── widget-wrapper.tsx
│   │   │   ├── widget-header.tsx
│   │   │   └── widget-loading.tsx
│   │   ├── charts/
│   │   │   ├── line-chart.tsx
│   │   │   ├── area-chart.tsx
│   │   │   ├── bar-chart.tsx
│   │   │   └── pie-chart.tsx
│   │   ├── values/
│   │   │   ├── gauge.tsx
│   │   │   ├── value-card.tsx
│   │   │   └── stats-card.tsx
│   │   ├── tables/
│   │   │   ├── alarm-table.tsx
│   │   │   └── device-table.tsx
│   │   ├── controls/
│   │   │   ├── control-button.tsx
│   │   │   └── control-slider.tsx
│   │   ├── maps/
│   │   │   └── device-map.tsx
│   │   └── ai/
│   │       ├── insight-widget.tsx
│   │       └── anomaly-chart.tsx
│   │
│   ├── builder/                       # Dashboard builder
│   │   ├── dashboard-canvas.tsx
│   │   ├── widget-palette.tsx
│   │   ├── property-panel.tsx
│   │   ├── data-source-picker.tsx
│   │   └── ai-assistant.tsx
│   │
│   ├── devices/                       # Device components
│   │   ├── device-card.tsx
│   │   ├── device-tree.tsx
│   │   └── command-panel.tsx
│   │
│   ├── alerts/                        # Alert components
│   │   ├── alert-list.tsx
│   │   └── alert-rule-form.tsx
│   │
│   ├── ai/                            # AI components
│   │   ├── chat-interface.tsx
│   │   ├── suggestion-card.tsx
│   │   └── insight-panel.tsx
│   │
│   └── shared/                        # Shared components
│       ├── data-table.tsx
│       ├── time-range-picker.tsx
│       ├── device-selector.tsx
│       └── empty-state.tsx
│
├── lib/
│   ├── api/                           # API utilities
│   │   └── client.ts
│   ├── hooks/                         # Custom hooks
│   │   ├── useWidgetData.ts
│   │   ├── useSocket.ts
│   │   └── usePermission.ts
│   ├── stores/                        # Zustand stores
│   │   ├── useAppStore.ts
│   │   └── useDashboardStore.ts
│   ├── utils/                         # Utilities
│   │   ├── cn.ts
│   │   ├── formatters.ts
│   │   └── validators.ts
│   └── widgets/                       # Widget registry
│       └── registry.ts
│
├── server/
│   ├── routers/                       # tRPC routers
│   │   ├── _app.ts
│   │   ├── auth.ts
│   │   ├── device.ts
│   │   ├── dashboard.ts
│   │   ├── alert.ts
│   │   ├── telemetry.ts
│   │   └── ai.ts
│   │
│   ├── services/                      # Business logic
│   │   ├── tenant.service.ts
│   │   ├── device.service.ts
│   │   ├── telemetry.service.ts
│   │   ├── alert.service.ts
│   │   ├── notification.service.ts
│   │   └── ai/
│   │       ├── dashboard-generator.ts
│   │       ├── data-query.ts
│   │       ├── anomaly-detector.ts
│   │       └── alert-summarizer.ts
│   │
│   ├── db/
│   │   ├── schema.prisma
│   │   ├── migrations/
│   │   └── tenant-manager.ts
│   │
│   └── realtime/
│       ├── server.ts
│       └── handlers/
│
├── types/                             # TypeScript types
│   ├── index.ts
│   ├── device.ts
│   ├── dashboard.ts
│   ├── widget.ts
│   └── alert.ts
│
├── config/
│   ├── site.ts
│   ├── dashboard-templates.ts
│   └── device-profiles.ts
│
├── public/
│   ├── icons/
│   └── templates/
│
├── benthos/                           # Stream processing
│   └── telemetry-pipeline.yaml
│
├── k8s/                               # Kubernetes manifests
│   ├── namespace.yaml
│   ├── app/
│   ├── databases/
│   └── monitoring/
│
├── simulator/                         # Device Simulator (separate)
│   ├── package.json
│   ├── src/
│   │   ├── core/
│   │   ├── generators/
│   │   ├── adapters/
│   │   └── scenarios/
│   └── web/
│
├── docker-compose.yml
├── Dockerfile
├── package.json
├── tsconfig.json
├── tailwind.config.ts
├── next.config.js
└── README.md
```

---

# 13. Implementation Priorities

## Phase 1: Foundation (Weeks 1-4)

| Week | Tasks |
|------|-------|
| 1 | Project setup (Next.js 15, TypeScript, Tailwind, shadcn/ui) |
| 1 | Database setup (PostgreSQL, TimescaleDB, Prisma) |
| 2 | Authentication (Auth.js with Google OAuth) |
| 2 | Multi-tenant foundation (master DB, tenant DBs) |
| 3 | User management, RBAC |
| 3 | Location hierarchy (Sites → Buildings → Floors → Areas) |
| 4 | Device profiles and templates |
| 4 | Basic device CRUD |

## Phase 2: Dashboard System (Weeks 5-8)

| Week | Tasks |
|------|-------|
| 5 | Dashboard CRUD |
| 5 | Widget registry and base components |
| 6 | Chart widgets (line, area, bar) |
| 6 | Value widgets (gauge, card) |
| 7 | Dashboard builder UI (grid, drag-drop) |
| 7 | Data source configuration |
| 8 | Real-time updates (Socket.io) |
| 8 | Widget property panel |

## Phase 3: Device Communication (Weeks 9-11)

| Week | Tasks |
|------|-------|
| 9 | MQTT broker setup (EMQX) |
| 9 | MQTT ingestion pipeline |
| 10 | HTTP webhook endpoint |
| 10 | TimescaleDB storage and aggregation |
| 11 | Device commands (RPC) |
| 11 | Gateway support |

## Phase 4: Alerting (Weeks 12-14)

| Week | Tasks |
|------|-------|
| 12 | Alert rules engine |
| 12 | Alert rule UI |
| 13 | Notification channels (email, in-app, webhook) |
| 13 | Alert management UI |
| 14 | Push notifications |
| 14 | Simple rule engine |

## Phase 5: AI Features (Weeks 15-18)

| Week | Tasks |
|------|-------|
| 15 | Claude API integration |
| 15 | Natural language dashboard builder |
| 16 | Natural language data queries |
| 16 | AI assistant chat interface |
| 17 | Anomaly detection (statistical) |
| 17 | Alert summarization |
| 18 | Smart suggestions |
| 18 | Predictive maintenance |

## Phase 6: Advanced Features (Weeks 19-22)

| Week | Tasks |
|------|-------|
| 19 | Public dashboards |
| 19 | Dashboard templates |
| 20 | Data export (CSV, JSON, Excel, PDF) |
| 20 | REST API and API keys |
| 21 | Audit logging |
| 21 | Cold storage archival |
| 22 | Performance optimization |
| 22 | Testing and bug fixes |

## Phase 7: Simulator (Weeks 23-24)

| Week | Tasks |
|------|-------|
| 23 | Simulator core engine |
| 23 | Device profile templates |
| 24 | Anomaly scenarios |
| 24 | Simulator web UI |

---

# 14. Environment Variables

```bash
# .env.example

# Application
NEXT_PUBLIC_APP_URL=http://localhost:3000
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=generate-a-secret-here

# OAuth - Google
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret

# Databases
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/iot_master
TIMESCALE_URL=postgresql://postgres:postgres@localhost:5433/iot_telemetry

# Redis
REDIS_URL=redis://localhost:6379

# Kafka/Redpanda
KAFKA_BROKERS=localhost:19092

# MQTT
MQTT_URL=mqtt://localhost:1883
MQTT_WS_URL=ws://localhost:8083

# AI
ANTHROPIC_API_KEY=your-anthropic-api-key

# Email
RESEND_API_KEY=your-resend-api-key

# Push Notifications
VAPID_PUBLIC_KEY=your-vapid-public-key
VAPID_PRIVATE_KEY=your-vapid-private-key

# Object Storage
S3_ENDPOINT=http://localhost:9000
S3_ACCESS_KEY=minioadmin
S3_SECRET_KEY=minioadmin
S3_BUCKET=iot-exports

# Feature Flags
ENABLE_AI_FEATURES=true
ENABLE_PUSH_NOTIFICATIONS=true
```

---

**End of Technical Specification**

*This document provides the complete technical foundation for implementing the IoT Dashboard Self-Service System using Claude Code CLI.*
