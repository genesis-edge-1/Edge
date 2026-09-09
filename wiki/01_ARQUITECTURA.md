# 🏗️ GENESIS EDGE One - Arquitectura Técnica

**EDGE-ID:** EXP-ARCH-001  
**Estado:** 🟢 VERIFIED  
**Última Actualización:** 2026-09-09  
**Versión:** 1.0.0  

---

## 🎯 Visión General

GENESIS EDGE One es una plataforma edge compute orchestrada en **K3s** con:

- 🔴 **Observabilidad integrada** (Prometheus + Grafana)
- 🔴 **Métricas extendidas** (CPU, Memory, Disk, Network, Redis, System)
- 🔴 **Alertas automáticas** (11 rules con thresholds inteligentes)
- 🔴 **Referencias arquitectónicas** (Z80 emulation patterns)

---

## 📐 Stack Técnico

### Componentes Principales

```
┌─────────────────────────────────────────┐
│     GENESIS EDGE One (K3s Cluster)      │
├─────────────────────────────────────────┤
│                                         │
│  ┌──────────────┐  ┌──────────────┐   │
│  │   Workload   │  │   Workload   │   │
│  │  (Application)│  │  (Services)  │   │
│  └──────────────┘  └──────────────┘   │
│         ↓                    ↓          │
│  ┌──────────────────────────────────┐  │
│  │   Metrics Worker                │  │
│  │   (genesis_edge_one.py)         │  │
│  │   - CPU, Memory, Disk, Network  │  │
│  │   - Redis status & memory       │  │
│  │   - System load, RTT            │  │
│  └──────────────────────────────────┘  │
│         ↓                               │
│  ┌──────────────────────────────────┐  │
│  │   Prometheus Scraper             │  │
│  │   - Interval: 5s                 │  │
│  │   - ServiceMonitor integration   │  │
│  └──────────────────────────────────┘  │
│         ↓                               │
│  ┌──────────────────────────────────┐  │
│  │   PrometheusRule (Alerts)        │  │
│  │   - 11 alert definitions         │  │
│  │   - Severity: WARNING/CRITICAL   │  │
│  └──────────────────────────────────┘  │
└─────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────┐
│   Prometheus Storage & Query Engine     │
│   - Time-series database               │
│   - 15m retention (configurable)       │
└─────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────┐
│   Grafana Visualization                │
│   - 10+ dashboard panels               │
│   - Real-time + historical views       │
│   - Dynamic $node_id filtering         │
└─────────────────────────────────────────┘
```

---

## 📊 Métricas Disponibles

### Sistema Operativo

| Métrica | Tipo | Fuente | Intervalo |
|---------|------|--------|-----------|
| `genesis_edge_cpu_usage_percent` | Gauge | psutil.cpu_percent() | 5s |
| `genesis_edge_memory_usage_percent` | Gauge | psutil.virtual_memory() | 5s |
| `genesis_edge_disk_usage_percent` | Gauge | psutil.disk_usage("/") | 5s |
| `genesis_edge_system_load_1m` | Gauge | os.getloadavg()[0] | 5s |
| `genesis_edge_system_load_5m` | Gauge | os.getloadavg()[1] | 5s |
| `genesis_edge_system_load_15m` | Gauge | os.getloadavg()[2] | 5s |

### Red

| Métrica | Tipo | Fuente | Intervalo |
|---------|------|--------|-----------|
| `genesis_edge_network_bytes_sent_total` | Counter | psutil.net_io_counters() | 5s |
| `genesis_edge_network_bytes_recv_total` | Counter | psutil.net_io_counters() | 5s |
| `genesis_edge_network_rtt_ms` | Gauge | ICMP echo / socket measurement | 5s |

### Redis

| Métrica | Tipo | Fuente | Intervalo |
|---------|------|--------|-----------|
| `genesis_edge_redis_connected` | Gauge | redis_client.ping() | 5s |
| `genesis_edge_redis_memory_used_bytes` | Gauge | redis.info("memory") | 5s |

---

## 🔗 Integración Z80 (Swifty-Z80)

### Relevancia Arquitectónica

**Repositorio:** https://github.com/kaypes/Swifty-Z80/commits/trunk

**Uso en GE-ONE:**

1. **🎓 Referencia de CPU Architecture**
   - Full Z80 instruction set implementation
   - Undocumented instructions & flags handling
   - Timing precision (T-cycles)

2. **⚙️ Interrupt Handling Patterns**
   - IM0 (device-driven), IM1, IM2 (vectored)
   - NMI (non-maskable interrupt)
   - intDelay mechanism (EI instruction)
   - P/V flag silicon bugs

3. **🔧 Legacy Device Integration**
   - Z80 still present in industrial controllers
   - Pattern for emulating retro CPUs on edge nodes
   - Protocol translation between Z80 <-> modern systems

4. **🧪 Unit Testing Patterns**
   - Swift Testing framework setup
   - CPU correctness verification
   - Flag & register testing methodology

### Componentes de Swifty-Z80

```
Swifty-Z80/
├── Z80.swift              # CPU emulator core
├── Registers.swift        # 16 registers + internal state
├── MemoryBus.swift        # Memory access protocol
├── PortBus.swift          # I/O port protocol
├── Z80+RegularOpcodes.swift   # 256 regular instructions
├── Z80+CBPrefix.swift     # 256 CB-prefixed instructions
├── Z80+EDPrefix.swift     # ED-prefixed instructions + control
├── Z80+IndexPrefix.swift  # DD/FD (IX/IY) index register ops
├── Flag.swift             # Type-safe flag enum
├── Logger.swift           # Debug logging
└── Tests/                 # 29 unit tests
```

### Patrones Aplicables a GE-ONE

**Pattern 1: Interrupt Management**
```swift
// Similar en GE-ONE para manejar eventos:
- Hardware interrupts (edge device signals)
- NMI for critical conditions
- intDelay for atomic operations
```

**Pattern 2: T-Cycle Accuracy**
```swift
// Timing precision para:
- Network latency measurement (RTT)
- Prometheus scrape cycles
- Alert evaluation timing
```

**Pattern 3: Undocumented Behavior**
```swift
// Handlin edge cases en:
- Legacy device compatibility
- Non-standard configurations
- Backward compatibility layers
```

---

## 🚀 Deployment Topology

### K3s Nodes

```
Node A (master+worker)          Node B (worker)
├─ K3s Server                    ├─ K3s Agent
├─ Prometheus Server             ├─ Metrics Worker
├─ Grafana                       ├─ Redis (local)
├─ Metrics Worker                └─ Application
├─ Redis (local)
└─ Application
```

### Namespaces

| Namespace | Propósito |
|-----------|-----------|
| `kube-system` | Prometheus, Grafana, monitoring |
| `default` | Application workloads |
| `kube-node-lease` | K3s heartbeat |

### Services

| Service | Namespace | Port | Protocolo |
|---------|-----------|------|-----------|
| prometheus | kube-system | 9090 | HTTP |
| grafana | kube-system | 3000 | HTTP |
| edge-metrics-worker | kube-system | 8080 | HTTP /metrics |

---

## 📈 Alert Hierarchy

```
Critical (🔴)          → Página On-Call
├─ GenesisEdgeHighCPU        (>90% x 5m)
├─ GenesisEdgeCriticalMemory (>92% x 3m)
├─ GenesisEdgeDiskCritical   (>95% x 2m)
├─ GenesisEdgeSystemHighLoad (>4.5 x 3m)
└─ GenesisEdgeRedisDown      (offline x 1m)

Warning (🟡)           → Ticket + Slack
├─ GenesisEdgeCPUWarning         (>75% x 5m)
├─ GenesisEdgeHighMemory         (>80% x 5m)
├─ GenesisEdgeHighDiskUsage      (>85% x 5m)
├─ GenesisEdgeLoadWarning        (>3.0 x 5m)
├─ GenesisEdgeRedisMemoryHigh    (>256MB x 5m)
└─ GenesisEdgeHighNetworkLatency (>100ms x 5m)
```

---

## 🔐 Security Model

### RBAC

```yaml
ServiceAccount: prometheus-operator
ClusterRole: prometheus-operator
├─ get/list prometheusrules
├─ get/list servicemonitors
├─ patch prometheus
└─ [additional permissions]
```

### Network Policies (optional)

```yaml
Ingress:
  - from: [Grafana pod]
    to: prometheus:9090

Egress:
  - to: edge-metrics-worker:8080
  - to: redis:6379
```

### Data Encryption

- TLS for remote metric ingestion (if applicable)
- Secrets encrypted at rest (K3s default)
- Redis AUTH for local access

---

## 📊 Grafana Dashboard Structure

### Panel 1: Redis Status (Stat)
```
Metric: genesis_edge_redis_connected
Values: 0 = RED (OFFLINE), 1 = GREEN (ONLINE)
```

### Panel 2: CPU Usage (Stat)
```
Metric: genesis_edge_cpu_usage_percent
Thresholds: <75% 🟢 / 75-90% 🟡 / >90% 🔴
```

### Panel 3: Memory Usage (Stat)
```
Metric: genesis_edge_memory_usage_percent
Thresholds: <80% 🟢 / 80-92% 🟡 / >92% 🔴
```

### Panel 4: Network Latency (Stat)
```
Metric: genesis_edge_network_rtt_ms
Display: Milliseconds, color-coded
```

### Panel 5: CPU History (TimeSeries)
```
Query: genesis_edge_cpu_usage_percent[15m]
Display: Line chart with 90% threshold
```

### Panel 6-10: Extended Panels
```
- Disk usage history
- Network traffic (RX/TX)
- Redis memory usage
- System load (1m)
- Redis connection timeline
```

---

## 🔄 Data Flow

```
1. Metrics Collection (5s interval)
   └─ genesis_edge_one.py scrapes system stats
   
2. Prometheus Scrape
   └─ ServiceMonitor pulls /metrics endpoint
   
3. Storage
   └─ TSDB stores time-series data
   
4. Alert Evaluation
   └─ PrometheusRule triggers on thresholds
   
5. Visualization
   └─ Grafana queries TSDB and renders dashboards
   
6. Notification
   └─ AlertManager sends to Slack/email/PagerDuty
```

---

## 🎯 Design Principles

| Principio | Implementación |
|-----------|-----------------|
| **Precision** | 5s scrape interval, T-cycle accuracy from Z80 |
| **Reliability** | Redundant Redis, multi-node deployment |
| **Observability** | 10+ metrics, 11 alerts, historical data |
| **Compatibility** | Legacy Z80 device support patterns |
| **Auditability** | SHA-256 hashes, versioned docs, change log |

---

**Documento:** 01_ARQUITECTURA.md  
**Estado:** 🟢 VERIFIED  
**SHA-256:** [COMPUTED ON COMMIT]  
**Versión:** 1.0.0
