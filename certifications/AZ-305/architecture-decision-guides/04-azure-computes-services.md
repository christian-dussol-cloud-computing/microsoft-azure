# Azure Compute Services Decision Guide

## 🎯 Quick Overview

| Service | Type | Use Case | Management | Scaling | Cost |
|:-------:|:----:|:--------:|:----------:|:-------:|:----:|
|**Azure Kubernetes Service (AKS)**|Orchestrated Containers|Complex microservices|Medium|Excellent|€€|
|**Container Instances (ACI)**|Simple Containers|Quick tasks, serverless containers|Low|Manual|€|
|**Container Apps**|Managed Containers|Microservices without K8s complexity|Low|Automatic|€€|
|**Azure Functions**|Serverless Compute|Event-driven, short tasks|None|Automatic|€|
|**Logic Apps**|Workflow Orchestration|Business process automation|Low|Automatic|€€|
|**Virtual Machines**|Infrastructure|Legacy apps, full control|High|Manual/VMSS|€€€|
|**App Service**|PaaS Web Apps|Web applications, APIs|Low|Automatic|€€|
|**Service Fabric**|Microservices Platform|Stateful microservices|High|Automatic|€€€|

-----

## 🔥 AZ-305 Exam Focus Areas

### **Key Decision Criteria for Exam**

1. **Stateless vs Stateful Applications**
   - Stateless → Functions, Container Apps, ACI
   - Stateful → AKS, Service Fabric, VMs

2. **Communication Patterns**
   - HTTP/REST → Container Apps, App Service
   - Event-driven → Functions, Logic Apps
   - Complex messaging → AKS with Service Mesh

3. **Scaling Requirements**
   - Scale to zero → Functions (Consumption), Container Apps
   - Predictable scaling → AKS, App Service
   - Manual scaling → ACI, VMs

4. **Integration Complexity**
   - Simple → Functions, Container Apps
   - Enterprise → Logic Apps, Service Fabric
   - Custom → AKS, VMs

-----

## 🐳 Container Services Comparison

### **Azure Kubernetes Service (AKS)**

**When to choose:**
- ✅ Complex microservices architectures
- ✅ Need full Kubernetes ecosystem
- ✅ Advanced networking and security requirements
- ✅ Multi-environment deployments (dev/staging/prod)
- ✅ Team has Kubernetes expertise
- ✅ **Stateful applications with persistent volumes**
- ✅ **Service mesh requirements (Istio, Linkerd)**

**AZ-305 Exam Scenarios:**
```
• "Design a solution for a financial trading platform requiring 
  sub-millisecond latency and complex inter-service communication"
• "Architect a multi-tenant SaaS platform with strict tenant isolation"
• "Migrate a complex on-premises application with 15+ services"
```

**Key features for exam:**
- **Cluster autoscaler** + **Horizontal Pod Autoscaler**
- **Azure AD integration** for RBAC
- **Azure CNI** vs **Kubenet** networking
- **Private clusters** for security
- **Azure Policy** integration for governance
- **AGIC (Application Gateway Ingress Controller)**

**Integration points:**
- Azure Container Registry (ACR)
- Azure Monitor + Container Insights
- Azure Key Vault (CSI driver)
- Azure Files/Disks for persistent storage

**❌ Avoid when:**
- Simple containerized applications
- Team lacks Kubernetes knowledge
- Rapid prototyping needs
- Cost optimization is primary concern

-----

### **Azure Container Instances (ACI)**

**When to choose:**
- ✅ Simple containerized workloads
- ✅ Burst computing scenarios
- ✅ CI/CD build agents
- ✅ Batch processing jobs
- ✅ No orchestration needed
- ✅ **Quick container testing**
- ✅ **Sidecar patterns with AKS virtual nodes**

**AZ-305 Exam Scenarios:**
```
• "Design a CI/CD pipeline that needs temporary build environments"
• "Process uploaded files without maintaining infrastructure"
• "Provide additional compute capacity during peak times"
```

**Key features for exam:**
- **Per-second billing** - cost-effective for short tasks
- **Virtual network integration** - can join existing VNets
- **Container groups** - multiple containers sharing resources
- **Restart policies** - Always, Never, OnFailure
- **GPU support** - for ML/AI workloads
- **Windows and Linux containers**

**Integration with AKS:**
- **Virtual nodes** - burst capacity for AKS
- **ACI Connector** - seamless scaling

**❌ Avoid when:**
- Complex microservices communication
- Advanced scaling requirements
- Long-running production workloads
- Service mesh needed

-----

### **Azure Container Apps**

**When to choose:**
- ✅ Microservices without Kubernetes complexity
- ✅ Event-driven applications
- ✅ HTTP-based services with auto-scaling
- ✅ DAPR (Distributed Application Runtime) scenarios
- ✅ Kubernetes benefits without management overhead
- ✅ **Scale-to-zero requirements**
- ✅ **Modern cloud-native applications**

**AZ-305 Exam Scenarios:**
```
• "Build a modern API that handles variable traffic patterns"
• "Create event-driven microservices with pub/sub messaging"
• "Develop a solution that needs advanced scaling with minimal management"
```

**Key features for exam:**
- **KEDA-based autoscaling** - scale based on external metrics
- **Built-in DAPR integration** - service-to-service communication
- **Revisions** - blue-green deployments
- **Ingress controller** - built-in traffic management
- **Environment variables and secrets** management
- **Integration with Azure Monitor**

**DAPR capabilities:**
- Service discovery and invocation
- State management
- Pub/sub messaging
- Bindings to external systems
- Observability

**❌ Avoid when:**
- Need full Kubernetes control
- Complex networking requirements
- Existing Kubernetes workloads
- Windows containers required

-----

## ⚡ Serverless Compute Comparison

### **Azure Functions**

**When to choose:**
- ✅ Event-driven processing
- ✅ Short-duration tasks (<10 minutes default, 60 min max)
- ✅ Pay-per-execution model desired
- ✅ Simple business logic
- ✅ Integration with Azure services
- ✅ **Trigger-based execution**
- ✅ **Stateless operations**

**AZ-305 Exam Scenarios:**
```
• "Process images uploaded to blob storage and create thumbnails"
• "Respond to IoT device telemetry in real-time"
• "Execute scheduled maintenance tasks"
• "Create a serverless API for mobile applications"
```

**Hosting plans comparison:**
| Plan | Use Case | Cold Start | VNet | Duration Limit |
|:----:|:--------:|:----------:|:----:|:--------------:|
|**Consumption**|Variable workloads|Yes|No|5 min (configurable to 10)|
|**Premium**|Predictable workloads|No|Yes|60 min|
|**Dedicated (App Service)**|Always-on needs|No|Yes|Unlimited|

**Triggers (exam favorites):**
- **HTTP Trigger** - REST APIs
- **Timer Trigger** - Scheduled tasks
- **Blob Trigger** - File processing
- **Service Bus Trigger** - Message processing
- **Event Grid Trigger** - Event-driven workflows
- **Cosmos DB Trigger** - Database changes

**❌ Avoid when:**
- Long-running processes (>60 minutes)
- Complex state management
- Real-time bidirectional communication
- Heavy computational workloads

-----

### **Logic Apps**

**When to choose:**
- ✅ Business process automation
- ✅ Integration with SaaS services
- ✅ Workflow orchestration
- ✅ No-code/low-code requirements
- ✅ Enterprise integration patterns
- ✅ **B2B/EDI scenarios**
- ✅ **Complex approval workflows**

**AZ-305 Exam Scenarios:**
```
• "Automate invoice approval process across multiple systems"
• "Synchronize customer data between CRM and ERP systems"
• "Process EDI transactions from trading partners"
• "Create incident management workflows"
```

**Logic Apps vs Functions decision:**
| Scenario | Logic Apps | Functions |
|:--------:|:----------:|:---------:|
|**Workflow orchestration**|✅|❌|
|**SaaS integration**|✅|Manual coding|
|**Visual design**|✅|Code-based|
|**Complex logic**|Limited|✅|
|**Performance**|Lower|Higher|
|**Custom code**|Limited|✅|

**Key connectors for exam:**
- Office 365, SharePoint, Teams
- Dynamics 365, Salesforce
- SAP, Oracle
- Azure services (Storage, SQL, Service Bus)
- On-premises systems (via Gateway)

**❌ Avoid when:**
- High-performance computing needed
- Complex algorithms required
- Real-time processing critical
- Custom code-heavy solutions

-----

## 🏗️ Platform Services

### **Azure App Service**

**When to choose:**
- ✅ Traditional web applications
- ✅ RESTful APIs
- ✅ Multi-language support (.NET, Java, Python, Node.js)
- ✅ Built-in DevOps integration
- ✅ **Minimal management overhead**
- ✅ **Integrated authentication**

**AZ-305 Exam Scenarios:**
```
• "Migrate existing web applications to cloud"
• "Build REST APIs with built-in authentication"
• "Deploy applications with CI/CD integration"
```

**Service plans comparison:**
- **Free/Shared** - Development/testing
- **Basic** - Low traffic production apps
- **Standard** - Production apps with scaling
- **Premium** - High-performance, advanced features
- **Isolated** - Network isolation, compliance

**Key features:**
- Auto-scaling based on metrics
- Deployment slots for blue-green deployments
- Application Gateway integration
- VNet integration for backend connectivity

### **Azure Service Fabric**

**When to choose:**
- ✅ Stateful microservices
- ✅ Complex distributed applications
- ✅ High availability requirements
- ✅ **Actor model patterns**
- ✅ **Legacy application modernization**

**AZ-305 Exam Scenarios:**
```
• "Modernize a monolithic application with complex state management"
• "Build a distributed system with actor-based patterns"
• "Require 99.95% availability with automatic failover"
```

**Service types:**
- **Stateless services** - similar to containers
- **Stateful services** - manage persistent state
- **Actor services** - virtual actor pattern

-----

## 🎯 Decision Framework

### **By Application Type**

| Application Type | Recommended Service | Alternative |
|:----------------:|:------------------:|:-----------:|
|**Microservices (Complex)**|AKS|Container Apps|
|**Microservices (Simple)**|Container Apps|AKS|
|**Event Processing**|Functions|Logic Apps|
|**Workflow Automation**|Logic Apps|Functions|
|**Batch Processing**|ACI|Functions|
|**Legacy Applications**|Virtual Machines|AKS|

### **By Team Expertise**

| Team Profile | Best Fit |
|:------------:|:--------:|
|**Kubernetes Experts**|AKS|
|**Cloud-Native Beginners**|Container Apps|
|**Serverless Focused**|Functions|
|**Business Process Focus**|Logic Apps|
|**Infrastructure Teams**|Virtual Machines|

### **By Scaling Requirements**

| Scaling Need | Solution |
|:------------:|:--------:|
|**Predictable Load**|AKS with HPA|
|**Variable/Bursty**|Functions Consumption|
|**Event-Driven**|Container Apps|
|**Manual Control**|ACI|

### **By Application Characteristics**

| Characteristic | Best Fit |
|:--------------:|:--------:|
|**Stateless microservices**|Container Apps, Functions|
|**Stateful microservices**|AKS, Service Fabric|
|**Event-driven processing**|Functions, Container Apps|
|**Workflow automation**|Logic Apps|
|**Legacy applications**|App Service, VMs|
|**Complex distributed systems**|AKS, Service Fabric|

### **By Scaling Patterns**

| Pattern | Solution |
|:-------:|:--------:|
|**Scale to zero**|Functions (Consumption), Container Apps|
|**Predictable scaling**|App Service, AKS|
|**Event-based scaling**|Functions, Container Apps with KEDA|
|**Manual scaling**|VMs, ACI|

### **By Integration Requirements**

| Requirement | Best Choice |
|:-----------:|:-----------:|
|**Azure services only**|Functions, Container Apps|
|**Enterprise SaaS**|Logic Apps|
|**Custom protocols**|AKS, Service Fabric|
|**Legacy systems**|Logic Apps with Gateway|

-----

## 🚀 Architecture Patterns

### **Pattern 1: Event-Driven Microservices**
```
Event Grid → Functions → Service Bus → Container Apps → Cosmos DB
```
- Event Grid for event routing
- Functions for immediate processing
- Service Bus for reliable queuing
- Container Apps for business logic
- Cosmos DB for data persistence

### **Pattern 2: Modern Web Application**
```
Front Door → App Service → Functions → Azure SQL
```
- Front Door for global load balancing
- App Service for web frontend
- Functions for API endpoints
- Azure SQL for data storage

### **Pattern 3: Complex Microservices**
```
Application Gateway → AKS → Service Bus → Cosmos DB
```
- Application Gateway for ingress
- AKS for orchestration
- Service mesh for service communication
- External data services

### **Pattern 4: Hybrid Integration**
```
Logic Apps → On-premises Gateway → Functions → Azure Storage
```
- Logic Apps for workflow orchestration
- Gateway for on-premises connectivity
- Functions for data transformation
- Storage for cloud persistence

-----

## 💰 Cost Optimization Strategies

### **Detailed Cost Analysis**

| Workload Type | AKS | Container Apps | Functions | App Service |
|:-------------:|:---:|:--------------:|:---------:|:-----------:|
|**Always-on API**|€€ (with reserved instances)|€€|€€€ (Premium plan needed)|€€|
|**Variable traffic**|€€€ (always running)|€€ (scale to zero)|€ (consumption)|€€ (auto-scale)|
|**Batch processing**|€€ (spot instances)|€€|€ (consumption)|€€€|
|**Development/testing**|€€€ (expensive for dev)|€ (scale to zero)|€ (consumption)|€€ (dev tiers available)|

### **Cost Comparison (Rough estimates)**

| Workload | AKS | Container Apps | Functions | ACI |
|:--------:|:---:|:--------------:|:---------:|:---:|
|**Always-on API**|€€|€€|€€€|€€€|
|**Bursty traffic**|€€€|€€|€|€€|
|**Batch processing**|€€|€€|€|€|
|**Development**|€€€|€|€|€|

### **Cost Optimization Tips**

1. **Functions**: Use consumption plan for variable workloads
2. **Container Apps**: Enable scale-to-zero for development
3. **AKS**: Use spot node pools for fault-tolerant workloads
4. **App Service**: Use appropriate service plan tiers
5. **Logic Apps**: Monitor consumption pricing carefully

-----

## 🔒 Security & Compliance

### **Network Security Matrix**

| Service | VNet Integration | Private Endpoints | Network Policies |
|:-------:|:----------------:|:-----------------:|:----------------:|
|**AKS**|✅ (Azure CNI)|✅|✅ (Calico/Azure)|
|**Container Apps**|✅|✅|Limited|
|**Functions**|✅ (Premium/Dedicated)|✅|No|
|**App Service**|✅|✅|No|
|**Logic Apps**|✅ (ISE/Standard)|✅|No|
|**ACI**|✅|No|No|

### **Identity & Access Management**

- **Managed Identity**: Supported by all services
- **Azure AD Integration**: Native support varies
- **RBAC**: Most granular in AKS
- **Key Vault Integration**: Available across services

### **Compliance Considerations**

- **Financial Services**: AKS with private clusters + Azure Policy
- **Healthcare (HIPAA)**: App Service with VNet integration
- **Government**: Service Fabric in isolated environments
- **PCI DSS**: Any service with proper network isolation

-----

## 📋 AZ-305 Exam Tips

### **Common Exam Patterns**

1. **"Choose the most cost-effective solution"**
   - Look for scale-to-zero capabilities
   - Consider consumption-based pricing

2. **"Design for high availability"**
   - Multi-region deployments
   - Auto-scaling capabilities
   - Health checks and recovery

3. **"Integrate with existing systems"**
   - Logic Apps for SaaS integration
   - VNet integration for on-premises
   - API management for legacy systems

4. **"Minimize management overhead"**
   - Prefer managed services
   - Choose serverless when appropriate
   - Consider operational complexity

### **Red Flags in Exam Questions**

- ❌ **"Real-time processing"** + Functions → Consider Container Apps or AKS
- ❌ **"Complex state management"** + Serverless → Consider stateful services
- ❌ **"Long-running processes"** + Functions → Consider other options
- ❌ **"Simple web app"** + AKS → Consider App Service

### **Decision Tree for Exam**

1. **Is it event-driven?** → Functions or Logic Apps
2. **Is it a workflow?** → Logic Apps
3. **Is it containerized?** → AKS, Container Apps, or ACI
4. **Is it stateful?** → AKS or Service Fabric
5. **Is it a web app?** → App Service
6. **Need full control?** → VMs or AKS

-----

## 🎪 Advanced Scenarios

### **Multi-Cloud Considerations**
- **AKS**: Can run on Azure Stack HCI
- **Service Fabric**: Supports on-premises and other clouds
- **Functions**: Azure-specific, but similar patterns elsewhere

### **Edge Computing**
- **Azure IoT Edge**: Run Functions on edge devices
- **AKS Edge Essentials**: Kubernetes at the edge
- **Container Apps**: Future edge support planned

### **AI/ML Workloads**
- **Training**: AKS with GPU nodes
- **Inference**: Functions, Container Apps, or AKS
- **Batch processing**: ACI with GPU support
