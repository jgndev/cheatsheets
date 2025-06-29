---
id: 19
date: 2025-06-29T00:00:00Z
title: "Industry Defined Latencies"
author: "Jeremy Novak"
summary: "Industry defined latency numbers for system performance optimization"
slug: latency-cheatsheet
tags:
  - performance
  - latency
  - systems
  - optimization
published: true
---

# System Latency Cheatsheet

---

## CPU & Memory Latencies

| Operation | Latency | Notes |
|-----------|---------|-------|
| **L1 Cache Reference** | 0.5 ns | Fastest cache level |
| **Branch Mispredict** | 5 ns | CPU pipeline penalty |
| **L2 Cache Reference** | 7 ns | Still very fast |
| **Mutex Lock/Unlock** | 25 ns | Synchronization overhead |
| **L3 Cache Reference** | 35 ns | Last level cache |
| **Main Memory Reference** | 100 ns | RAM access |
| **Compress 1K with Snappy** | 3,000 ns (3 μs) | Fast compression |
| **Send 1K bytes over 1 Gbps Network** | 10,000 ns (10 μs) | Network transmission |
| **Read 4K randomly from SSD** | 150,000 ns (150 μs) | Solid state drive |
| **Read 1MB sequentially from Memory** | 250,000 ns (250 μs) | Memory bandwidth |
| **Round Trip within Same Datacenter** | 500,000 ns (0.5 ms) | Network latency |
| **Read 1MB sequentially from SSD** | 1,000,000 ns (1 ms) | Sequential SSD read |
| **Disk Seek** | 10,000,000 ns (10 ms) | Hard disk seek time |
| **Read 1MB sequentially from Disk** | 20,000,000 ns (20 ms) | Hard disk read |
| **Send packet CA→Netherlands→CA** | 150,000,000 ns (150 ms) | Intercontinental |

---

## Network Latencies

| Connection Type | Typical Latency | Notes |
|----------------|----------------|-------|
| **Same Datacenter** | 0.5 ms | Local network |
| **Same City** | 1-2 ms | Metropolitan area |
| **Same Region** | 5-20 ms | Regional network |
| **Cross Country (US)** | 60-80 ms | Coast to coast |
| **Transatlantic** | 80-120 ms | US ↔ Europe |
| **Transpacific** | 120-180 ms | US ↔ Asia |
| **Satellite Internet** | 500-700 ms | Geostationary orbit |
| **Low Earth Orbit Satellite** | 25-35 ms | Starlink-style |

---

## Database Operation Latencies

| Operation | Typical Latency | Notes |
|-----------|----------------|-------|
| **Index Lookup (B-tree)** | 0.1-1 ms | In-memory index |
| **Primary Key Lookup** | 1-5 ms | Single row by ID |
| **Simple Query (indexed)** | 1-10 ms | With proper indexing |
| **Complex Query** | 10-100 ms | Joins, aggregations |
| **Full Table Scan (small)** | 10-100 ms | < 1M rows |
| **Full Table Scan (large)** | 1-10 s | > 10M rows |
| **Database Connection** | 1-10 ms | Connection establishment |
| **Transaction Commit** | 1-50 ms | Depends on durability |

---

## Application Latencies

| Operation | Typical Latency | Notes |
|-----------|----------------|-------|
| **Function Call** | 1 ns | Same process |
| **System Call** | 1,000 ns (1 μs) | Kernel transition |
| **HTTP Request (local)** | 1-10 ms | Same datacenter |
| **REST API Call** | 10-100 ms | Typical web service |
| **DNS Lookup** | 10-200 ms | Domain resolution |
| **SSL Handshake** | 50-200 ms | TLS negotiation |

---

## Rule of Thumb Conversions

| Unit | Nanoseconds | Human Scale |
|------|------------|-------------|
| **1 nanosecond** | 1 ns | 1 second |
| **1 microsecond** | 1,000 ns | 17 minutes |
| **1 millisecond** | 1,000,000 ns | 11.5 days |
| **1 second** | 1,000,000,000 ns | 32 years |

---

## Performance Optimization Guidelines

### CPU Bound Operations
- Keep data in L1/L2 cache when possible
- Minimize branch mispredictions
- Use CPU-friendly data structures (arrays vs linked lists)
- Consider SIMD instructions for parallel operations

### Memory Bound Operations  
- Prefer sequential memory access patterns
- Use memory pools to reduce allocation overhead
- Consider memory-mapped files for large datasets
- Implement proper cache locality

### I/O Bound Operations
- Use asynchronous I/O when possible
- Implement connection pooling for databases
- Consider read replicas for read-heavy workloads
- Use CDNs for static content delivery

### Network Bound Operations
- Minimize round trips
- Use connection pooling
- Implement proper caching strategies
- Consider data compression for large payloads

---

## Monitoring & Measurement

### Key Metrics to Track
- **P50, P95, P99 latencies** - Understand distribution
- **Throughput vs Latency** - Often inverse relationship  
- **Queue depths** - Identify bottlenecks
- **Resource utilization** - CPU, memory, I/O, network

### Tools for Measurement
- **Application**: New Relic, DataDog, AppDynamics
- **System**: htop, iostat, netstat, sar
- **Network**: ping, traceroute, mtr
- **Database**: Query profilers, slow query logs

---

## References

- [Numbers Every Programmer Should Know](https://gist.github.com/jboner/2841832)
- [Latency Numbers Every Programmer Should Know](https://colin-scott.github.io/personal_website/research/interactive_latency.html)
- [AWS Network Performance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/enhanced-networking.html)
- [Google Cloud Network Performance](https://cloud.google.com/compute/docs/networking)
