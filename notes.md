# Module 2

## AWS Well Architected Framework

## ![Static Badge](https://img.shields.io/badge/Service-red) AWS Well-Architected Tool
-  Helps you review the state of your workloads and compares them to the latest AWS architectural best practices
-  Gives you access to knowledge and best practices used by AWS architects
-  Delivers an action plan with step-by-step guidance on how to build better workloads for the cloud
-  Provides a consistent process for you to review and measure your cloud architectures

## ![Static Badge](https://img.shields.io/badge/Best%20Practise-blue) Best Practises
1. Enable scalibility
2. Automate the environment
3. Treat resources as disposable (do things dynamically - don't run unnecessairy servers, use automatic IP adresses, automate deployment of resources)
4. Use loosely coupled components
5. Design services, not servers
6. Choose the right database solution
7. Avoid single points of failure
8. Optimize for cost
9. Use caching
10. Secure your entire infrastructure

## AWS Structure
- AWS Region (geographical area)
  - Availibility Zones (at least two in every Region)
    - Data centers (at leas one in every Availibility Zone)

**AWS Region** - regions are isolated from one another, not every service is avaliable in certain regions. Connected with backbone network.
**AWS Availibility Zone** -  is designed as an independent failure zone, they are physically separated. They are interconnected with other Availability Zones in a Region using high-speed privatelinks. ystems can span multiple Availability Zones. Distributing applications across multiple Availability Zones enables them to remain resilient in most failure situations, including natural disasters or system failures.
**AWS Local Zone** - type of AWS infrastructure deployment that places AWS compute, storage, database, and other select services closer to large population, industry, and IT centers where no AWS Region exists today. Each AWS Local Zone location is an extension of an AWS Region.
