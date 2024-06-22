---
tags:
  - OCI-Architecture
Links: "[[OCI Architecture.canvas|OCI Architecture]]"
---

> [!important]
> In most of the countries we operate we have at least 2 datacenters.

> [!important]
> Each Availability Domain (AD) has 3 Fault Domains (FD).

### Availability Domain (AD)

**Definition**: An Availability Domain is an isolated data center within a region. Each region can have multiple Availability Domains, and each AD is designed to be independent of the others in terms of power, cooling, and networking.

**Key Characteristics**:

- **Isolation**: Each AD is physically separated from the others to prevent failures from affecting multiple ADs.
- **High Availability**: Resources deployed in different ADs are isolated from each other, ensuring that a failure in one AD does not impact resources in another.
- **Data Center Level**: ADs are essentially separate data centers within a region.

**Use Cases**:

- **Disaster Recovery**: Deploying applications across multiple ADs ensures that if one AD goes down, the application can continue running in another AD.
- **Redundancy**: Critical applications can run in multiple ADs to avoid single points of failure.

### Fault Domain (FD)

**Definition**: A Fault Domain is a logical grouping of hardware and infrastructure within an Availability Domain. Fault Domains provide additional fault isolation within an AD by grouping resources in such a way that they do not share the same physical hardware.

**Key Characteristics**:

- **Sub-division of AD**: An AD is divided into multiple FDs.
- **Hardware Isolation**: Resources in different FDs do not share the same physical server or rack, reducing the risk of hardware failure affecting multiple resources.
- **Rack Level**: FDs operate at the rack level within an AD.

**Use Cases**:

- **High Availability within an AD**: Deploying applications across multiple FDs within the same AD to ensure that hardware failures (like server or rack failures) do not impact the entire application.
- **Fault Tolerance**: Critical components of an application can be distributed across different FDs to enhance fault tolerance.

### Differences Between Availability Domain and Fault Domain

| Feature                 | Availability Domain (AD)                                 | Fault Domain (FD)                                       |
| ----------------------- | -------------------------------------------------------- | ------------------------------------------------------- |
| **Scope**               | Data center level                                        | Rack level within a data center                         |
| **Isolation Level**     | Entire data center                                       | Physical server/rack within a data center               |
| **Purpose**             | Protect against data center-wide failures                | Protect against hardware failures within a data center  |
| **Physical Separation** | Separate physical data centers                           | Logical grouping within the same data center            |
| **Use Cases**           | Disaster recovery, high availability across data centers | High availability, fault tolerance within the same AD   |
| **Redundancy Strategy** | Deploying resources in different ADs                     | Deploying resources in different FDs within the same AD |

### Practical Example

Imagine you have a critical application that you want to deploy in Oracle Cloud Infrastructure. Here’s how you would use ADs and FDs to enhance its availability and fault tolerance:

1. **Multi-AD Deployment**:
    
    - Deploy instances of your application in multiple ADs within the same region. This ensures that even if one AD experiences a complete outage, the other ADs can keep your application running.
2. **Multi-FD Deployment**:
    
    - Within each AD, distribute your application instances across multiple FDs. This ensures that even if there is a hardware failure affecting a server or rack, it will not bring down your entire application within that AD.

By leveraging both Availability Domains and Fault Domains, you can build robust, highly available, and fault-tolerant applications that can withstand various types of failures.

> [!info]
> Availability Domains (ADs) and Fault Domains (FDs) in Oracle Cloud Infrastructure (OCI) are used at all times as part of your infrastructure design to ensure high availability and fault tolerance. They are not just backup systems that kick in only when the original servers are down. Instead, they are an integral part of the architecture to distribute workloads and manage risks continuously.


