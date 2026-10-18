# UPI Offline Mesh Simulator

A Java Spring Boot project that demonstrates a simulated offline payment workflow using a virtual mesh network and deferred backend settlement.

The project explores how an encrypted payment packet can travel between virtual devices and reach a backend through a device that regains internet connectivity.

> **Disclaimer:** This is an educational simulation, not an official UPI application. It does not connect to real UPI infrastructure, use actual bank accounts, or process real payments.

## Features

- **Virtual Mesh Network:** Simulates payment packet propagation between devices.
- **REST APIs:** Provides endpoints for payment simulation, mesh operations, and backend ingestion.
- **Hybrid Encryption:** Demonstrates RSA-OAEP and AES-GCM encryption.
- **Idempotency:** Uses ciphertext hashing and an atomic in-memory cache to help prevent duplicate processing.
- **Replay Protection:** Includes a timestamp-based freshness check.
- **Transaction Settlement:** Demonstrates debit, credit, and transaction ledger operations.
- **Interactive Dashboard:** Provides a browser-based interface for exploring the simulated workflow.
- **Concurrency Testing:** Includes a test for simultaneous delivery of the same packet.

## Tech Stack

| Component | Technology |
|---|---|
| Language | Java |
| Backend Framework | Spring Boot |
| Build Tool | Maven Wrapper |
| Database | H2 In-Memory Database |
| Persistence | Spring Data JPA |
| Frontend | HTML, CSS, JavaScript |
| Cryptography | RSA-OAEP, AES-GCM |
| Testing | JUnit |

## Architecture

The simulated workflow consists of four main stages:

1. **Payment Creation:** A payment instruction is created and encrypted.
2. **Mesh Propagation:** The encrypted packet is distributed among virtual devices.
3. **Bridge Upload:** A simulated bridge device uploads the packet when internet connectivity is available.
4. **Backend Processing:** The backend checks for duplicate packets, decrypts valid payloads, verifies freshness, and attempts transaction settlement.

## Project Structure

```text
src/
├── main/
│   ├── java/com/demo/upimesh/
│   │   ├── config/
│   │   ├── controller/
│   │   ├── crypto/
│   │   ├── model/
│   │   └── service/
│   └── resources/
│       ├── application.properties
│       └── templates/dashboard.html
└── test/
    └── java/com/demo/upimesh/
        └── IdempotencyConcurrencyTest.java

pom.xml
mvnw
mvnw.cmd
```

## Getting Started

### Prerequisites

- JDK 17 or newer
- Internet connectivity for the initial Maven dependency download

### Run on Windows

Open PowerShell in the project directory:

```powershell
.\mvnw.cmd spring-boot:run
```

### Run on Linux or macOS

```bash
./mvnw spring-boot:run
```

Once the application starts, open:

http://localhost:8080

### Run Tests

On Windows:

```powershell
.\mvnw.cmd test
```

On Linux or macOS:

```bash
./mvnw test
```

**Verification status:** The project has not yet been run or tested by the current repository maintainer. Successful startup and test execution have not been verified.

## API Reference

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/` | Serves the dashboard |
| GET | `/api/server-key` | Retrieves the server public key |
| GET | `/api/accounts` | Retrieves account information |
| GET | `/api/transactions` | Retrieves recent transactions |
| GET | `/api/mesh/state` | Retrieves virtual mesh state |
| POST | `/api/demo/send` | Simulates creating and sending a payment |
| POST | `/api/mesh/gossip` | Simulates a mesh propagation round |
| POST | `/api/mesh/flush` | Simulates bridge uploads |
| POST | `/api/mesh/reset` | Resets the simulated mesh |
| POST | `/api/bridge/ingest` | Submits a packet for backend processing |

## Key Concepts Demonstrated

### Hybrid Encryption

The project demonstrates encrypting payment data with AES-GCM and protecting the AES key using RSA-OAEP.

### Idempotent Processing

An atomic in-memory cache based on ciphertext hashes helps ensure that repeated deliveries of the same packet are not processed multiple times within the running application instance.

### Transaction Management

Spring transaction management is used to demonstrate coordinated debit, credit, and ledger operations.

### Concurrency

The included test explores simultaneous delivery of the same packet and checks whether settlement occurs only once.

## Limitations

- The mesh network is software-simulated; real Bluetooth or Wi-Fi Direct communication is not implemented.
- The H2 database is in-memory, so application data does not persist across restarts.
- The idempotency cache is local to the application instance and is not a distributed production solution.
- The project does not implement actual UPI, banking, or NPCI integration.
- Production deployment would require additional authentication, authorization, key management, monitoring, and security reviews.

## Learning Objectives

This project can be used to explore:

- Java and Spring Boot backend development
- REST API design
- Database transactions and persistence
- Cryptography fundamentals
- Idempotency and concurrency
- Software simulation of distributed workflows


