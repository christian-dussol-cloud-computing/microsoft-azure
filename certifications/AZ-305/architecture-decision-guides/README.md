![AZ-305](https://img.shields.io/badge/Microsoft-AZ--305-blue)
![Azure](https://img.shields.io/badge/Cloud-Azure-007FFF)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

# 🏗️ AZ-305 Solution Architecture Guides

> Practical decision guides for **Azure Solutions Architect Expert (AZ-305)** exam preparation

## 🎯 What This Repository Provides

Unlike official Microsoft documentation that explains *what* Azure services do, these guides focus on **when** and **why** to choose specific services (exactly what you need to succeed in the AZ-305 exam).

Each guide provides:
- **Quick overview tables** for quick decision-making
- **Real-world scenarios** with concrete business examples  
- **Decision frameworks** based on team expertise and requirements
- **Cost optimization strategies** for each service category
- **Anti-patterns** to help eliminate wrong decision according to requirements and contexts

## 📚 Decision Guides

| Guide | Focus Areas | Key Services Covered |
|:-----:|:-----------:|:-------------------:|
| [💾 **Storage Services**](./01-azure-storage-services.md) | Databases, Files, Data Lakes | SQL Database, Cosmos DB, Storage Accounts, Synapse |
| [🗄️ **Azure SQL Services**](./02-azure-sql-services.md) | SQL Deployment Options, Performance | SQL Database, SQL MI, SQL on VMs |
| [📡 **Messaging & Analytics**](./03-azure-messaging-analytics.md) | Event Processing, Data Integration | Service Bus, Event Grid, Event Hubs, Data Factory |
| [🚀 **Compute Services**](./04-azure-compute-services.md) | Containers, Serverless, VMs | AKS, Container Apps, Functions, Logic Apps, VMs |
| [🌐 **Networking Services**](./05-azure-networking-services.md) | Connectivity, Load Balancing | VNet, Application Gateway, Front Door, VPN Gateway |
| [🔒 **Security & Identity**](./06-azure-security-identity.md) | Authentication, Authorization, Secrets | Entra ID, Key Vault, Sentinel, Defender, WAF |

## 🎓 How to Use These Guides

### **For AZ-305 Exam Preparation**
1. **Start with your weakest domain** - use the comparison tables for quick overview
2. **Focus on decision criteria** - understand *when* to choose each service
3. **Study the scenarios** - these mirror real exam question patterns
4. **Review anti-patterns** - learn what NOT to choose and why

### **For Real-World Architecture**
1. **Use as decision framework** - systematic approach to service selection
2. **Consider team expertise** - guides include team capability assessments
3. **Factor in costs** - each guide includes cost optimization strategies
4. **Apply patterns** - proven architectural patterns for common scenarios

## ⭐ Why These Guides Are Different

### **Decision-Focused Approach**
- **Comparison matrices** for quick service selection
- **When to choose** vs **when to avoid** for each service
- **Decision trees** based on real requirements

### **Exam-Relevant Content**
- **Scenario-based examples** matching AZ-305 question style
- **Trade-off analysis** for architecture decisions
- **Cost considerations** integrated into every choice

### **Practical Experience**
- **Real industry examples** from finance, healthcare, retail
- **Team expertise mapping** - services by skill level required
- **Operational considerations** beyond just technical features

## 🎯 Example: How This Helps in AZ-305

**Typical Exam Question Style:**
> "A company needs to process IoT data from 10,000 devices. The processing must scale automatically and cost should be minimized. Which compute service should you recommend?"

**How These Guides Help:**
- **Compute guide** provides clear decision matrix comparing Functions, Container Apps, and AKS
- **Cost section** shows Functions Consumption plan is most cost-effective for variable workloads
- **Scenarios section** includes IoT processing patterns with specific recommendations

## 🚀 Quick Start

1. **Browse the quick overview tables** in each guide for service overviews
2. **Jump to relevant scenarios** that match your study focus or real project needs
3. **Use decision frameworks** to practice systematic architecture thinking
4. **Review cost considerations** to understand business impact of choices

## 💡 Contributing

Found an error or have a suggestion? 
- **Open an issue** with your feedback
- **Submit a pull request** with improvements
- **Share real-world scenarios** that could help others

## 📄 License

Feel free to use these guides for your AZ-305 preparation and share with the Azure community!

---

## 🔗 Additional Resources

- **Official AZ-305 Exam**: [Microsoft Learn](https://learn.microsoft.com/en-us/credentials/certifications/exams/az-305/)
- **Azure Architecture Center**: [Microsoft Docs](https://learn.microsoft.com/en-us/azure/architecture/)
- **Azure Well-Architected Framework**: [Microsoft Learn](https://learn.microsoft.com/en-us/azure/well-architected/)

---

*Created with ❤️ for the Azure community by Christian Dussol*

**⭐ If these guides help you, please give this repository a star!**
