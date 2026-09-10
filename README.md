# GCP Cloud HA VPN ↔ FortiGate Dual-ISP BGP Integration

## 📌 Project Overview

This project documents the production implementation of a highly available
site-to-site VPN between an on-premises FortiGate firewall running FortiOS
7.4.11 and Google Cloud Platform (GCP).

The solution uses GCP Cloud HA VPN, Cloud Router, BGP, and two independent
IPsec tunnels over dual ISP connections to provide redundant connectivity
and dynamic routing between the on-premises LAN and GCP VPC.

**Status:** ✅ Production / Fully Operational

---

## 🏗️ Architecture

The solution uses two independent VPN paths:

```text
                         ┌─────────────────┐
                         │     GCP VPC     │
                         └────────┬────────┘
                                  │
                         ┌────────▼────────┐
                         │  Cloud HA VPN   │
                         │     Gateway     │
                         └───────┬─┬───────┘
                                 │ │
                        IPsec 1  │ │  IPsec 2
                                 │ │
                              ┌──▼─┴──┐
                              │       │
                           ISP1     ISP2
                              │       │
                              └───┬───┘
                                  │
                         ┌────────▼────────┐
                         │    FortiGate    │
                         │ FortiOS 7.4.11  │
                         └────────┬────────┘
                                  │
                         ┌────────▼────────┐
                         │   On-Prem LAN   │
                         └─────────────────┘
