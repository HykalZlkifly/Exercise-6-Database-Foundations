# Database Foundations: Containerized MongoDB Orchestration and Secure Middleware Abstraction via Node-RED

## 📝 Introduction
In modern industrial IoT ecosystems and enterprise web applications, migrating from volatile, real-time debugging to persistent data storage is a critical operational milestone. While emitting raw telemetry strings directly to a system log is sufficient for initial hardware confirmation, production-grade applications require durable, resilient, and performant transaction layers.

This repository demonstrates a **decoupled, multi-tier architecture** that implements an API Gateway middleware layer using **Node-RED** to safely ingest, validate, and orchestrate unstructured JSON payloads into a containerized **MongoDB NoSQL database**. By encapsulating the database engine within an isolated Docker environment, the data layer remains entirely shielded from direct public network exposure, establishing a secure perimeter where communication is governed exclusively through structured RESTful endpoints.

---

## 🎯 Project Objectives
* **Containerized Infrastructure Provisioning:** Deploy, configure, and manage a local instance of the MongoDB engine encapsulated inside a Docker container, establishing proper port forwarding, bridge networking, and host volume binding for physical data persistence.
* **Middleware Interfacing:** Extend the capabilities of the Node-RED runtime engine by installing, configuring, and verifying native MongoDB v4 client drivers via the Palette Manager subsystem.
* **Stateful RESTful CRUD API Design:** Upgrade static HTTP endpoints into fully functional, dynamic, and stateful application programming interfaces (`POST`, `GET`, `PUT`, `DELETE`) capable of manipulating live NoSQL documents.
* **Architectural & Security Analysis:** Evaluate system resilience by analyzing the advantages of schema-less storage engines during iterative rapid prototyping, while defending a middleware-abstracted topology against common edge-network vectors.

---

## 🛠️ Advanced System Topology

```text
       ┌────────────────────────────────────────────────────────┐
       │                 UNTRUSTED PERIMETER                    │
       │  [ Edge IoT Hardware / Simulated Postman Clients ]     │
       └───────────────────────────┬────────────────────────────┘
                                   │
                                   │ HTTP Request (JSON Payload)
                                   ▼ [Port 1880]
       ┌────────────────────────────────────────────────────────┐
       │                   MIDDLEWARE LAYER                     │
       │              [ Node-RED Runtime Engine ]               │
       │   - Handles CORS, routes, logging, and processing      │
       └───────────────────────────┬────────────────────────────┘
                                   │
                                   │ Internal Route via host.docker.internal
                                   ▼ [Port 27017]
       ┌────────────────────────────────────────────────────────┐
       │                   PERSISTENCE LAYER                    │
       │        [ Sandboxed MongoDB Docker Container ]          │
       │   - Dynamic Database Generation: "smart_campus"        │
       │   - Dynamic Collection Target: "sensor_data"           │
       └───────────────────────────┬────────────────────────────┘
                                   │
                                   │ Hardware Mount (Bind Mount)
                                   ▼
       ┌────────────────────────────────────────────────────────┐
       │                PHYSICAL STORAGE LAYER                  │
       │         [ Host Machine Disk File System ]             │
       │   - Path: yewguan/Desktop/MongoDB -> /data/db          │
       └────────────────────────────────────────────────────────┘
