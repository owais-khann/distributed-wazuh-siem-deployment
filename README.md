# Distributed Wazuh SIEM Architecture & Deployment Lab

A step-by-step architectural guide and hands-on lab implementation of a multi-node **Wazuh 4.14 SIEM** cluster deployed across isolated Linux virtual machines.

## Lab Architecture
The environment separates core SIEM components across three dedicated Linux nodes encrypted via mutual SSL/TLS certificates:
* **Wazuh Indexer (`192.168.4.136`):** OpenSearch-based indexing and storage engine for security alerts and telemetry.
* **Wazuh Server / Manager (`192.168.4.138`):** Central log analysis engine, rule/decoder processing, and Filebeat alert forwarding.
* **Wazuh Dashboard (`192.168.4.137`):** Web-based visualization, threat hunting, and cluster management interface.

## Key Implementation Phases
1. **PKI & SSL/TLS Certificate Generation:** Generated root CA and node-specific X.509 certificates using `wazuh-certs-tool.sh` for encrypted inter-node communication.
2. **Wazuh Indexer Cluster Setup:** Configured `opensearch.yml`, deployed TLS certificates with strict file permissions, and initialized the security plugin.
3. **Wazuh Manager & Filebeat Pipeline:** Installed `wazuh-manager` and configured Filebeat with a secure keystore to ship parsed alerts over TLS (`port 9200`) to the indexer.
4. **Wazuh Dashboard & API Integration:** Linked the dashboard to both the indexer and the Wazuh Server REST API (`port 5500`) with verified RBAC authentication.

## Documentation
* Full step-by-step deployment guide with terminal verification outputs: **[Wazuh_Installation_Guide.pdf](./Wazuh_Installation_Guide.pdf)**

---
**Author:** Owais Khan | [LinkedIn](https://www.linkedin.com/in/owais-khan-953089376)
