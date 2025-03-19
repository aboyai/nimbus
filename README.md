# Nimbus

![Nimbus Logo](https://your-logo-url.com/logo.png)

**Nimbus Blob Storage** is a high-performance, scalable, and fault-tolerant object storage solution designed for modern cloud-native applications. Built with Go and powered by Raft for strong consistency, Nimbus supports massive concurrency, efficient multipart uploads, S3-compatible APIs, and pluggable backends.

---

## ✨ Features

- **S3-Compatible APIs**
  - Upload, Download, Delete, List Objects
  - Bucket Management
  - Pre-signed URLs for secure access

- **Clustered Storage with Raft**
  - Leader Election, Log Replication
  - Strong Consistency Guarantees

- **High Performance**
  - Concurrent Multipart Uploads
  - Efficient Sharding and Indexing

- **Pluggable Backends**
  - Local Filesystem, MinIO, Amazon S3, GCS, Azure Blob

- **Security**
  - Token-Based Authentication (JWT, OAuth2)
  - TLS Encryption (REST/gRPC)

- **Extensible**
  - gRPC + REST APIs
  - Plugin System for Custom Backends

---

## 🌐 Architecture Overview

```
 +-----------+     +------------+     +----------------+
 |  Clients  | --> |  Nimbus API| --> | Raft Consensus |
 +-----------+     +------------+     +----------------+
        |                  |                  |
        |              +---v---+        +----v----+
        +------------> |Storage| <----> |Metadata |
                       +-------+        +---------+
```

- **API Layer**: REST/gRPC endpoints
- **Raft Layer**: Ensures consistency across nodes
- **Storage Layer**: Pluggable backend storage
- **Metadata**: Indexing, Sharding, Object Metadata

---

## 📄 Configuration (`config.yaml`)

```yaml
server:
  listen: ":8080"
  tls_enabled: true
  cert_file: "cert.pem"
  key_file: "key.pem"

raft:
  node_id: "nimbus-node-1"
  data_dir: "./raft_data"
  peers:
    - "nimbus-node-1=127.0.0.1:7001"
    - "nimbus-node-2=127.0.0.1:7002"

storage:
  backend: "local"  # local | minio | s3 | gcs | azure
  path: "./blobs"

security:
  jwt_secret: "your-secret"
```

---

## 🚀 Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/aboyai/nimbus.git
cd nimbus
```

### 2. Build and Run
```bash
go build -o nimbus
./nimbus --config=config.yaml
```

### 3. Interact with the API
```bash
curl -X PUT http://localhost:8080/buckets/mybucket
curl -X PUT http://localhost:8080/buckets/mybucket/objects/file.txt --data-binary @file.txt
```

---

## 📅 Roadmap
- ☑ Multi-Region Replication
- ☑ Object Versioning
- ☐ Erasure Coding
- ☐ Lambda Triggers on Events

---

## 🛡 Use Cases
- Backup and Archival Storage
- CDN Origin Storage
- Data Lake Storage
- Media & Content Delivery

---

## 🌟 Credits
Developed with ❤ by [Aboyai LLC](https://aboyai.com)

---

## 🚫 License
[Apache 2.0 License](LICENSE)

---

## 🚀 Contributing
PRs welcome! Please see the [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

