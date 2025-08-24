# Azure SQL Decision Guide

## 🎯 Decision Framework

### 1. **Azure SQL Database** (PaaS - Single Database)
**When to choose:**
- ✅ Modern cloud-native applications
- ✅ Microservices with separate databases
- ✅ Agile development/DevOps workflows
- ✅ Predictable and controlled budget
- ✅ Auto-scaling requirements
- ✅ Variable workloads (Serverless option)

**Typical AZ-305 use cases:**
- E-commerce web applications
- Mobile backend APIs
- Multi-tenant SaaS solutions
- Lightweight data warehouse with Serverless

---

### 2. **Azure SQL Managed Instance** (PaaS - Complete Instance)
**When to choose:**
- ✅ Lift-and-shift migration from SQL Server
- ✅ Complex legacy applications
- ✅ Advanced SQL Server features required
- ✅ 100% SQL Server compatibility needed
- ✅ Private networks/hybrid scenarios (VNet)
- ✅ Cross-database queries and linked servers

**Typical AZ-305 use cases:**
- Existing ERP/CRM migration
- Financial applications with CLR
- Cross-database queries
- Linked servers requirements
- SQL Agent jobs and advanced features

---

### 3. **SQL Server on Azure VMs** (IaaS)
**When to choose:**
- ✅ Full OS control required
- ✅ Highly specific/legacy applications
- ✅ Features not supported in PaaS
- ✅ Complex system integration
- ✅ Strict compliance with OS control
- ✅ Always On Availability Groups needed

**Typical AZ-305 use cases:**
- Legacy banking applications
- Systems with custom agents
- Windows clustering requirements
- Specific backup/restore needs
- OS-level compliance requirements

---

## 🔍 Decision Matrix

| Criteria | <center>Azure SQL DB</center> | <center>SQL MI</center> | <center>SQL on VM</center> |
|---------|--------------|---------|------------|
| **SQL Server Compatibility** | ~85% | ~100% | 100% |
| **Management Overhead** | Automatic | Semi-automatic | Manual |
| **Cost (TCO)** | € | €€ | €€€ |
| **Scaling** | Excellent | Good | Manual |
| **Security** | Built-in | Built-in | Configure |
| **Maintenance** | None | Minimal | Complete |
| **Max IOPS** | Up to 320K | Up to 200K | Unlimited |
| **Max Connections** | Up to 30K | Up to 32K | Unlimited |
| **Backup Retention** | 7-35 days | 7-35 days | Custom |
| **High Availability** | 99.99% SLA | 99.99% SLA | Custom config |

---

## 📋 Performance & Pricing Tiers

### Azure SQL Database Options
- **DTU Model**: Fixed performance bundle (Basic, Standard, Premium)
- **vCore Model**: Flexible CPU/memory allocation
- **Serverless**: Auto-pause for cost optimization
- **Hyperscale**: Up to 100TB, rapid scaling

### SQL Managed Instance Tiers
- **General Purpose**: Balanced compute and storage
- **Business Critical**: High performance, Always On
- **Memory Optimized**: In-memory OLTP workloads

### SQL on VM Sizing
- **Standard**: General purpose workloads
- **Memory Optimized**: RAM-intensive applications  
- **Compute Optimized**: CPU-intensive applications
- **Storage Optimized**: High disk throughput

---

## 🔄 Migration Patterns

### From On-Premises SQL Server

#### **Path 1: SQL Database**
```
✅ Best for: Modern apps, microservices
📋 Steps:
  1. Database Migration Assistant (DMA)
  2. Azure Database Migration Service
  3. Application connection string update
⚠️  Challenges: Feature compatibility (~85%)
```

#### **Path 2: SQL Managed Instance**
```
✅ Best for: Lift-and-shift with minimal changes
📋 Steps:
  1. Network setup (VNet, NSG)
  2. Azure Database Migration Service
  3. Minimal application changes
⚠️  Challenges: Network complexity, cost
```

#### **Path 3: SQL on VM**
```
✅ Best for: Legacy systems, full control
📋 Steps:
  1. VM sizing and configuration
  2. Backup/restore or replication
  3. Network and security setup
⚠️  Challenges: Management overhead, patching
```

### Cross-Cloud Migration
- **AWS RDS → Azure SQL**: Use DMS with VPN
- **Google Cloud SQL → Azure**: Backup/restore method
- **Oracle → Azure SQL**: Schema conversion required

---

## 🌐 Hybrid & Multi-Cloud Scenarios

### **Hybrid Deployments**
```
Scenario: "On-premises + Azure integration"
Solutions:
├── SQL Data Sync (SQL Database)
├── Hybrid connections (SQL MI)  
├── VPN/ExpressRoute (All options)
└── Azure Arc (SQL on VM)
```

### **Disaster Recovery Patterns**
- **Active Geo-Replication** (SQL Database)
- **Auto-failover Groups** (SQL DB/MI)
- **Always On AG** (SQL on VM only)
- **Zone Redundancy** (Premium tiers)

---

## 📊 Advanced Security Features

### **Built-in Security (SQL DB/MI)**
- Advanced Threat Protection
- Dynamic Data Masking
- Transparent Data Encryption
- Always Encrypted
- Row Level Security
- Column Level Security

### **Network Security**
- Private Endpoints (SQL DB/MI)
- VNet Integration (SQL MI/VM)
- Service Endpoints
- Firewall Rules

### **Compliance Certifications**
- SOC 1, SOC 2, SOC 3
- ISO 27001, ISO 27018
- GDPR, HIPAA compliance
- FedRAMP (SQL on VM)

---

## 📋 Key Questions for the Exam

### Enhanced Scenario Analysis

**🔴 RED FLAGS for SQL Database:**
- "SQL Agent Jobs" → Use SQL MI or VM
- "Cross-database queries" → Use SQL MI or VM  
- "Linked servers" → Use SQL MI or VM
- "CLR assemblies" → Use SQL MI or VM
- "Always On Availability Groups" → Use SQL on VM only
- "Custom backup schedules" → Use SQL MI or VM
- "Database Mail" → Use SQL MI or VM

**🟢 GREEN FLAGS for SQL Database:**
- "Modern application" → SQL Database
- "Microservices" → SQL Database
- "Auto-scaling" → SQL Database (especially Serverless)
- "Cost optimization" → SQL Database Serverless
- "Serverless workload" → SQL Database Serverless
- "Multi-tenant SaaS" → SQL Database with Elastic Pools
- "Variable workload patterns" → SQL Database Serverless

**🔴 RED FLAGS for SQL MI:**
- "Tight budget" → Consider SQL Database
- "Simple application" → SQL Database often better
- "OS control required" → Use SQL on VM
- "Custom Windows services" → Use SQL on VM
- "Always On AGs" → Use SQL on VM

**🟢 GREEN FLAGS for SQL MI:**
- "Migration from SQL Server" → SQL MI
- "Minimal code changes" → SQL MI
- "Advanced SQL features" → SQL MI
- "VNet integration required" → SQL MI
- "Cross-database functionality" → SQL MI
- "SQL Agent jobs" → SQL MI
- "Service Broker" → SQL MI

**🔴 RED FLAGS for SQL on VM:**
- "Cost optimized" → Use SQL Database
- "Simplified management" → Use PaaS options
- "Auto-scaling required" → Use SQL Database
- "Cloud-native applications" → Use SQL Database

**🟢 GREEN FLAGS for SQL on VM:**
- "Full OS control" → SQL on VM
- "OS customization" → SQL on VM
- "Always On Availability Groups" → SQL on VM
- "Windows clustering" → SQL on VM
- "Custom compliance requirements" → SQL on VM
- "Legacy system integration" → SQL on VM

---

## 🎯 Enhanced AZ-305 Exam Strategies

### 1. **Analyze Keywords Systematically**
```
Migration Keywords:
├── "Lift-and-shift" → SQL MI
├── "Modernize" → SQL Database  
├── "Minimal changes" → SQL MI
└── "Cloud-native" → SQL Database

Performance Keywords:
├── "Variable workload" → SQL Database Serverless
├── "High IOPS" → Business Critical tiers
├── "Memory-intensive" → Memory Optimized
└── "Elastic scaling" → SQL Database

Cost Keywords:
├── "Budget optimized" → SQL Database
├── "Pay only when used" → Serverless
├── "Reserved capacity" → All options with RIs
└── "Minimize TCO" → PaaS options preferred
```

### 2. **Decision Tree Approach**
```
Start: What's the primary requirement?

├── Migration from SQL Server?
│   ├── Complex features needed? → SQL MI
│   ├── OS control required? → SQL on VM  
│   └── Modern app architecture? → SQL Database
│
├── New cloud-native application?
│   ├── Variable workload? → SQL Database Serverless
│   ├── Multi-tenant? → SQL Database + Elastic Pools
│   └── High performance? → SQL Database Business Critical
│
└── Hybrid/On-premises integration?
    ├── Network isolation required? → SQL MI
    ├── Always On replication? → SQL on VM
    └── Simple sync requirements? → SQL Database + Data Sync
```

### 3. **Cost Optimization Patterns**
- **Reserved Instances**: Up to 55% savings on compute
- **Azure Hybrid Benefit**: Use existing licenses
- **Elastic Pools**: Shared resources for multi-tenant
- **Serverless**: Auto-pause for dev/test environments

---

## 🚀 Special Use Cases & Edge Scenarios

### **Enterprise Patterns**
```
Fortune 500 Migration:
├── Phase 1: Non-critical apps → SQL Database
├── Phase 2: Legacy systems → SQL MI  
├── Phase 3: Mission-critical → SQL on VM (if needed)
└── Phase 4: Optimize and consolidate
```

### **Compliance Scenarios**
```
Healthcare (HIPAA):
├── SQL Database: ✅ Built-in compliance
├── SQL MI: ✅ VNet isolation + compliance
└── SQL on VM: ✅ Full control + custom config

Financial Services:
├── PCI DSS: All options compliant
├── SOX: Audit trails available
└── Custom compliance: SQL on VM preferred
```

### **Performance Edge Cases**
- **> 4TB databases**: Hyperscale or SQL on VM
- **Cross-region replication**: Active Geo-Replication
- **Ultra-low latency**: Premium SSD + proximity placement

---

## 🛠️ Troubleshooting Common Scenarios

### **When SQL Database is NOT the Right Choice**
- Application uses SQL Server Agent
- Requires cross-database queries
- Uses Service Broker or SQL Mail
- Needs Always On Availability Groups
- Database > 4TB (except Hyperscale)

### **Performance Issues Identification**
```
Symptoms → Likely Cause → Solution
├── High CPU → DTU limits → Scale up or use vCore
├── Storage throttling → IOPS limits → Premium tier
├── Connection timeouts → Connection limits → Connection pooling
└── Memory pressure → Insufficient resources → Memory optimized tier
```

### **Connectivity Problems**
- **Firewall rules**: Check IP allowlist
- **Private endpoints**: Verify DNS resolution
- **VNet integration**: Confirm subnet delegation
- **Connection strings**: Validate format and credentials

---

## 💡 Pro Tips for AZ-305 Success

### **Memory Techniques**
```
SQL Database = "Simple, Serverless, Scalable"
SQL MI = "Migration, Managed, Most compatible"  
SQL on VM = "Virtual, Versatile, Very customizable"
```

### **Quick Elimination Method**
1. **Budget mentioned?** → Favor SQL Database
2. **Migration scenario?** → Consider SQL MI first
3. **OS control needed?** → Only SQL on VM
4. **Modern app?** → Likely SQL Database
5. **Complex SQL features?** → SQL MI or VM

### **Time Management**
- Spend 30 seconds identifying scenario type
- Apply decision framework quickly
- Don't overthink simple scenarios
- Trust the elimination process

---

## 🎯 Final Exam Checklist

### **Must Remember**
- [ ] SQL Database: 85% compatibility, lowest cost, best scaling
- [ ] SQL MI: 100% compatibility, VNet integration, moderate cost  
- [ ] SQL on VM: Full control, highest cost, manual management
- [ ] Serverless: Variable workloads, auto-pause capability
- [ ] Always On AGs: Only available on SQL on VM

### **Common Traps**
- Don't assume "enterprise" = SQL on VM
- "Migration" doesn't always mean SQL MI
- Consider total cost, not just compute
- Remember network requirements for SQL MI

### **Last-Minute Review**
- Review the decision matrix (5 minutes)
- Practice the elimination technique
- Memorize red/green flags
- Trust your systematic approach
