# 🛡️ SIEM AI Analyzer - Enterprise Security Operations Center

> **AI-Powered Security Information and Event Management System with Real-Time Threat Detection, Automated Response, and Intelligent Analysis**

[![Azure](https://img.shields.io/badge/Azure-VM-0078D4?logo=microsoft-azure)](https://azure.microsoft.com/)
[![Elasticsearch](https://img.shields.io/badge/Elasticsearch-8.x-005571?logo=elasticsearch)](https://www.elastic.co/)
[![Node.js](https://img.shields.io/badge/Node.js-18.x-339933?logo=node.js)](https://nodejs.org/)
[![Claude AI](https://img.shields.io/badge/Claude-Sonnet_4-8B5CF6)](https://www.anthropic.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Installation Guide](#installation-guide)
- [Configuration](#configuration)
- [Dashboard Features](#dashboard-features)
- [API Documentation](#api-documentation)
- [Alert System](#alert-system)
- [Security Operations Workflow](#security-operations-workflow)
- [Compliance & Regulatory](#compliance--regulatory)
- [Scaling to Production](#scaling-to-production)
- [Screenshots](#screenshots)
- [Troubleshooting](#troubleshooting)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)

---

## 🎯 Overview

This project is a **comprehensive Security Information and Event Management (SIEM) system** designed from the ground up to provide enterprise-grade security monitoring capabilities. It addresses critical business problems including:

- **Threat Detection**: Real-time identification of security incidents with AI-powered analysis
- **Compliance**: Satisfies PCI-DSS, HIPAA, SOC 2, and GDPR logging requirements
- **Incident Response**: Automated containment actions and AI-generated response plans
- **Operational Efficiency**: Centralized log aggregation and correlation across all infrastructure

### Why SIEM Matters

Modern IT infrastructures generate massive volumes of security data across disparate systems. Without centralized collection, correlation, and analysis, organizations remain blind to:

- **Coordinated attacks** spanning multiple systems
- **Insider threats** that don't trigger individual system alerts
- **Compliance violations** across the infrastructure
- **Attack dwell time** averaging 200+ days before detection

This SIEM reduces detection time from months to **minutes** through:
- Real-time log aggregation and correlation
- AI-powered threat analysis
- Automated playbook execution
- Comprehensive forensic timelines

---

## 🏗️ Architecture

### System Components

```
┌─────────────────────────────────────────────────────────────────┐
│                       Azure Cloud Platform                       │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │              Virtual Machine (Standard D2s v3)              │ │
│  │                   2 vCPUs | 8GB RAM                         │ │
│  │                                                              │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │ │
│  │  │              │  │              │  │              │     │ │
│  │  │ Elasticsearch│◄─┤   Filebeat   │◄─┤ Linux Auditd │     │ │
│  │  │              │  │              │  │              │     │ │
│  │  │  (Storage &  │  │ (Log Shipper)│  │(Kernel Audit)│     │ │
│  │  │   Search)    │  │              │  │              │     │ │
│  │  └──────┬───────┘  └──────────────┘  └──────────────┘     │ │
│  │         │                                                   │ │
│  │         │          ┌──────────────┐                        │ │
│  │         ├─────────►│              │                        │ │
│  │         │          │    Wazuh     │                        │ │
│  │         │          │              │                        │ │
│  │         │          │(Threat Intel)│                        │ │
│  │         │          └──────────────┘                        │ │
│  │         │                                                   │ │
│  │         ▼                                                   │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │ │
│  │  │              │  │              │  │              │     │ │
│  │  │    Kibana    │  │ Node.js API  │  │  Claude AI   │     │ │
│  │  │              │  │              │  │              │     │ │
│  │  │(Dashboards)  │  │  (Backend)   │  │  (Analysis)  │     │ │
│  │  └──────────────┘  └──────┬───────┘  └──────────────┘     │ │
│  │                            │                                │ │
│  │                            ▼                                │ │
│  │                     ┌──────────────┐                        │ │
│  │                     │              │                        │ │
│  │                     │  Frontend    │                        │ │
│  │                     │  Dashboard   │                        │ │
│  │                     │              │                        │ │
│  │                     └──────────────┘                        │ │
│  └────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │  Alert Integrations  │
                    │                      │
                    │  • Slack Webhooks    │
                    │  • Email (Gmail)     │
                    │  • AI Chatbot        │
                    └──────────────────────┘
```

### Data Flow

1. **Collection**: Filebeat monitors log files and system events via Auditd
2. **Forwarding**: Logs are shipped to Elasticsearch via HTTP
3. **Detection**: Wazuh applies 13,000+ detection rules with MITRE ATT&CK mapping
4. **Storage**: Elasticsearch indexes events with inverted index for fast search
5. **Analysis**: Claude AI analyzes patterns and generates insights
6. **Alerting**: Slack/Email notifications sent for critical events
7. **Visualization**: Real-time dashboards display security posture
8. **Response**: Automated playbooks execute containment actions

---

## ✨ Features

### Core SIEM Capabilities

#### 1. **Real-Time Alert Monitoring**
- Live feed of security events with severity classification
- Advanced filtering by time range, severity, source IP, and event type
- Alert drawer with detailed forensic information
- One-click actions: Block IP, Investigate, Escalate, Resolve

#### 2. **AI-Powered Analysis**
- **Summary Analysis**: Claude AI summarizes alert patterns and threat levels
- **Incident Response**: Generates step-by-step response plans
- **Threat Intelligence**: Contextual IP address analysis
- **Natural Language Interface**: AI chatbot for security questions

#### 3. **Automated Playbooks**
Six pre-configured automated response playbooks:
- **Brute Force Protection**: Blocks IPs after 10+ failed logins
- **Malware Containment**: Isolates infected hosts
- **Privilege Escalation Alert**: Creates critical cases for sudo abuse
- **Port Scan Response**: Blocks scanning IPs for 24 hours
- **DDoS Mitigation**: Activates rate limiting during traffic spikes
- **After-Hours Access Alert**: Verifies unusual login times

#### 4. **Case Management**
- Create and track security investigations
- Priority levels: Critical, High, Medium, Low
- Assign to analysts with notes and timestamps
- Link multiple alerts to single case

#### 5. **Incident Response Workflow**
- **Containment**: One-click IP blocking via iptables
- **Eradication**: SSH hardening and vulnerability patching
- **Recovery**: System health monitoring
- **Documentation**: AI-generated incident reports

#### 6. **Interactive Visualizations**
- Attack timeline graph showing threat trends
- Threat distribution pie charts
- Top attacker IP rankings
- Alert severity breakdowns
- Real-time metrics dashboard

### Enhanced Features (Latest)

#### 7. **Multi-Channel Alerting** 🔔
Six types of intelligent alerts via Slack and Email:
- **General Security Alerts**: AI analysis summaries
- **Critical Alerts**: High-severity incidents (level ≥ 10)
- **Playbook Executions**: Automated response actions
- **Containment Actions**: IP blocking confirmations
- **Incident Response**: AI-generated response plans
- **Case Creation**: Critical/high priority case notifications

#### 8. **AI Security Chatbot** 🤖
- Floating chat button (bottom-right corner)
- Conversational AI assistant powered by Claude
- Explains security concepts and threats
- Provides incident response guidance
- Natural language security queries
- Context-aware responses

#### 9. **Live SIEM Data Integration** (Pending Elasticsearch)
- Chatbot queries real alert data
- Answers "How many alerts today?"
- Shows top threat IPs from live data
- Current alert statistics

---

## 🛠️ Technology Stack

### Infrastructure
| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Cloud Platform** | Microsoft Azure | Scalable VM hosting |
| **Operating System** | Ubuntu 24.04 LTS | Linux-based security stack |
| **VM Specs** | Standard D2s v3 (2 vCPU, 8GB RAM) | Proof-of-concept deployment |

### SIEM Stack
| Component | Technology | Version | Purpose |
|-----------|-----------|---------|---------|
| **Search & Analytics** | Elasticsearch | 8.x | Log storage and search engine |
| **Visualization** | Kibana | 8.x | Security dashboards |
| **Log Shipping** | Filebeat | 8.x | Lightweight log forwarder |
| **Kernel Audit** | Linux Auditd | Native | System call monitoring |
| **Threat Detection** | Wazuh | Latest | 13,000+ detection rules, MITRE ATT&CK |

### Application Layer
| Component | Technology | Version | Purpose |
|-----------|-----------|---------|---------|
| **Backend** | Node.js + Express | 18.x | REST API server |
| **AI Engine** | Anthropic Claude | Sonnet 4 | Natural language analysis |
| **Frontend** | HTML/CSS/JavaScript | ES6+ | Interactive dashboard |
| **Charting** | Chart.js | 4.4.0 | Data visualizations |
| **Alerts** | Slack Webhooks + Nodemailer | Latest | Multi-channel notifications |

### Development Tools
- **Package Manager**: npm
- **Environment Config**: dotenv
- **HTTP Client**: axios
- **CORS**: cors middleware

---

## 📦 Installation Guide

### Prerequisites

```bash
# System Requirements
- Azure VM (or any Linux server)
- Ubuntu 24.04 LTS
- Minimum 2 vCPU, 8GB RAM
- 50GB+ storage
- Public IP address
- Open ports: 22 (SSH), 3000 (App), 9200 (Elasticsearch), 5601 (Kibana)
```

### Step 1: Azure VM Setup

```bash
# Create Azure VM
az vm create \
  --resource-group siem-rg \
  --name siem-analyzer \
  --image Ubuntu2404 \
  --size Standard_D2s_v3 \
  --admin-username azureuser \
  --generate-ssh-keys

# Configure network security group
az vm open-port --port 3000 --resource-group siem-rg --name siem-analyzer
az vm open-port --port 9200 --resource-group siem-rg --name siem-analyzer
az vm open-port --port 5601 --resource-group siem-rg --name siem-analyzer

# SSH into VM
ssh azureuser@<VM_PUBLIC_IP>
```

### Step 2: Install Elasticsearch

```bash
# Import Elasticsearch PGP Key
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg

# Add Elasticsearch repository
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list

# Install Elasticsearch
sudo apt-get update
sudo apt-get install elasticsearch

# Configure Elasticsearch
sudo nano /etc/elasticsearch/elasticsearch.yml
# Set: network.host: 0.0.0.0
# Set: discovery.type: single-node
# Enable X-Pack security

# Start and enable Elasticsearch
sudo systemctl daemon-reload
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch

# Get auto-generated password
sudo /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
```

### Step 3: Install Kibana

```bash
# Install Kibana
sudo apt-get install kibana

# Configure Kibana
sudo nano /etc/kibana/kibana.yml
# Set: server.host: "0.0.0.0"
# Set: elasticsearch.hosts: ["http://localhost:9200"]
# Set: elasticsearch.username: "elastic"
# Set: elasticsearch.password: "<YOUR_PASSWORD>"

# Start Kibana
sudo systemctl enable kibana
sudo systemctl start kibana

# Access Kibana at http://<VM_PUBLIC_IP>:5601
```

### Step 4: Install Filebeat

```bash
# Install Filebeat
sudo apt-get install filebeat

# Enable system and auditd modules
sudo filebeat modules enable system
sudo filebeat modules enable auditd

# Configure Filebeat
sudo nano /etc/filebeat/filebeat.yml
# Set Elasticsearch output and credentials

# Setup Filebeat
sudo filebeat setup -e

# Start Filebeat
sudo systemctl enable filebeat
sudo systemctl start filebeat
```

### Step 5: Install Wazuh

```bash
# Add Wazuh repository
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && chmod 644 /usr/share/keyrings/wazuh.gpg

echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list

# Install Wazuh manager
sudo apt-get update
sudo apt-get install wazuh-manager

# Install Wazuh agent
sudo apt-get install wazuh-agent

# Start Wazuh
sudo systemctl enable wazuh-manager
sudo systemctl start wazuh-manager

# Configure Wazuh to forward to Elasticsearch
sudo nano /var/ossec/etc/ossec.conf
# Add Elasticsearch integration
```

### Step 6: Configure Linux Auditd

```bash
# Auditd is pre-installed on Ubuntu, configure rules
sudo nano /etc/audit/rules.d/audit.rules

# Add monitoring rules
-w /etc/passwd -p wa -k passwd_changes
-w /etc/shadow -p wa -k shadow_changes
-w /etc/sudoers -p wa -k sudoers_changes
-w /etc/ssh/sshd_config -p wa -k sshd_config_changes
-a always,exit -F arch=b64 -S execve -F exe=/usr/bin/sudo -k sudo_usage
-a always,exit -F arch=b64 -S execve -F exe=/bin/su -k su_usage

# Reload Auditd
sudo auditctl -R /etc/audit/rules.d/audit.rules

# Start Auditd
sudo systemctl enable auditd
sudo systemctl start auditd
```

### Step 7: Install Node.js and Application

```bash
# Install Node.js 18.x
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Create application directory
mkdir ~/siem-ai-analyzer
cd ~/siem-ai-analyzer

# Clone or upload your project files
# - index.html
# - server.js
# - package.json
# - .env

# Install dependencies
npm install express @anthropic-ai/sdk @elastic/elasticsearch cors axios dotenv nodemailer

# Start the application
node server.js
```

---

## ⚙️ Configuration

### Environment Variables (.env)

Create a `.env` file in your project root:

```bash
# Slack Configuration
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL

# Elasticsearch Configuration
ES_NODE=http://localhost:9200
ES_USERNAME=elastic
ES_PASSWORD=your_elasticsearch_password

# Anthropic API Configuration
ANTHROPIC_API_KEY=sk-ant-api03-your-api-key-here

# Email Configuration (Gmail)
EMAIL_SERVICE=gmail
EMAIL_USER=your-email@gmail.com
EMAIL_PASSWORD=your-gmail-app-password
EMAIL_TO=security-team@yourcompany.com

# Server Configuration
PORT=3000
```

### Slack Webhook Setup

1. Go to https://api.slack.com/apps
2. Create a new app → "From scratch"
3. Name your app (e.g., "SIEM Security Alerts")
4. Select your workspace
5. Navigate to "Incoming Webhooks" → Activate
6. Click "Add New Webhook to Workspace"
7. Select channel (e.g., #security-alerts)
8. Copy webhook URL to `.env`

### Gmail App Password Setup

1. Go to https://myaccount.google.com/security
2. Enable 2-Step Verification (if not enabled)
3. Navigate to "App passwords"
4. Create new app password
5. Name it "SIEM Alerts"
6. Copy 16-character password to `.env`

### Anthropic API Key

1. Go to https://console.anthropic.com/
2. Sign up or log in
3. Navigate to API Keys
4. Create new API key
5. Copy to `.env`

---

## 🎨 Dashboard Features

### Main Interface

```
┌─────────────────────────────────────────────────────────────┐
│  🛡️ SIEM AI Analyzer - Security Operations Center  [🟢 LIVE]│
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  FILTERS                                              │   │
│  │  Time: [Last 24h ▼]  Severity: [All ▼]  Type: [All ▼] │   │
│  │  Quick: [1h] [6h] [24h] [7d]                          │   │
│  └──────────────────────────────────────────────────────┘   │
│                                                               │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  QUICK ACTIONS                                        │   │
│  │  [📊 Fetch Alerts] [🤖 AI Summary] [🚨 Response Plan]│   │
│  │  [🔍 Threat Intel] [🚫 Block IP] [💬 AI Chat]       │   │
│  └──────────────────────────────────────────────────────┘   │
│                                                               │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  📋 RECENT ALERTS                                     │   │
│  │  ┌─────────────────────────────────────────────────┐ │   │
│  │  │ 🔴 CRITICAL  10:45:23 • 192.168.1.100 • root    │ │   │
│  │  │ Multiple failed SSH login attempts detected     │ │   │
│  │  └─────────────────────────────────────────────────┘ │   │
│  │  ┌─────────────────────────────────────────────────┐ │   │
│  │  │ 🟠 HIGH      10:42:15 • 45.33.32.156 • admin   │ │   │
│  │  │ Privilege escalation attempt via sudo           │ │   │
│  │  └─────────────────────────────────────────────────┘ │   │
│  └──────────────────────────────────────────────────────┘   │
│                                                               │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  📊 ANALYTICS                                         │   │
│  │  [Attack Timeline Chart] [Threat Distribution]       │   │
│  └──────────────────────────────────────────────────────┘   │
│                                                               │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  🤖 AUTOMATED PLAYBOOKS                               │   │
│  │  [✅ Brute Force] [✅ Malware] [⚫ Port Scan]        │   │
│  └──────────────────────────────────────────────────────┘   │
│                                                               │
│                                               [💬 AI Chat] ← │
└─────────────────────────────────────────────────────────────┘
```

### Alert Drawer (Detail View)

Click any alert to open detailed drawer:

```
┌───────────────────────────────────────┐
│  📋 Alert Details              [✕]   │
├───────────────────────────────────────┤
│  Severity: 🔴 CRITICAL                │
│  Time: 2026-01-03 10:45:23           │
│  Source IP: 192.168.1.100            │
│  User: root                           │
│  Agent: server-01                     │
│                                       │
│  Event Description:                   │
│  Multiple failed SSH login attempts   │
│  detected from suspicious IP address  │
│                                       │
│  MITRE ATT&CK:                        │
│  T1110 - Brute Force                  │
│                                       │
│  Related Alerts: [5 similar events]   │
│                                       │
│  [🚫 Block IP] [🔍 Investigate]      │
│  [⬆️ Escalate] [✓ Mark Resolved]    │
└───────────────────────────────────────┘
```

### AI Chatbot

```
┌─────────────────────────────────────┐
│  🤖 Security AI Assistant    [✕]   │
├─────────────────────────────────────┤
│                                     │
│  🤖  Hi! I'm your AI Security       │
│      Assistant. I can help you     │
│      with:                          │
│      • Analyzing security alerts    │
│      • Explaining threats           │
│      • Incident response guidance   │
│      • Understanding SIEM data      │
│                                     │
│  👤  What is a brute force attack?  │
│                                     │
│  🤖  A brute force attack is when   │
│      attackers systematically try   │
│      multiple password combinations │
│      until finding the correct one. │
│      Your SIEM detects this by      │
│      monitoring failed login        │
│      attempts.                      │
│                                     │
├─────────────────────────────────────┤
│  [Type your question...]      [➤]  │
└─────────────────────────────────────┘
```

---

## 🔌 API Documentation

### Endpoints Overview

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/` | Serve main dashboard HTML |
| `GET` | `/health` | Health check |
| `GET` | `/api/alerts` | Fetch recent security alerts |
| `POST` | `/api/analyze` | AI-powered alert analysis |
| `POST` | `/api/threat-intel` | Threat intelligence lookup |
| `POST` | `/api/incident-response` | Generate incident response plan |
| `POST` | `/api/containment/block-ip` | Block malicious IP address |
| `GET` | `/api/containment/blocked-ips` | List blocked IP addresses |
| `POST` | `/api/eradication/harden-ssh` | Harden SSH configuration |
| `GET` | `/api/recovery/system-status` | Check system health |
| `POST` | `/api/playbook/execute` | Execute automated playbook |
| `POST` | `/api/case/create` | Create new security case |
| `POST` | `/api/chatbot` | AI chatbot conversation |

### Detailed Endpoint Documentation

#### 1. Fetch Alerts

```http
GET /api/alerts?from=0&size=50
```

**Query Parameters:**
- `from` (optional): Offset for pagination (default: 0)
- `size` (optional): Number of alerts to return (default: 50)

**Response:**
```json
{
  "total": 147,
  "alerts": [
    {
      "@timestamp": "2026-01-03T10:45:23.000Z",
      "rule": {
        "description": "Multiple failed SSH login attempts",
        "level": 10,
        "id": 5710,
        "groups": ["authentication", "ssh"]
      },
      "source": {
        "ip": "192.168.1.100"
      },
      "data": {
        "srcuser": "root",
        "srcip": "192.168.1.100"
      },
      "agent": {
        "name": "server-01"
      }
    }
  ]
}
```

#### 2. AI Analysis

```http
POST /api/analyze
Content-Type: application/json

{
  "alerts": [...],
  "analysisType": "summary"
}
```

**Request Body:**
- `alerts`: Array of alert objects (max 20 for performance)
- `analysisType`: "summary" or "incident"

**Response:**
```json
{
  "analysis": "Threat Level: High\n\nMultiple SSH brute force attempts detected from 192.168.1.100. Recommend immediate IP blocking and credential rotation.",
  "alertCount": 15,
  "analysisType": "summary"
}
```

**Triggers:**
- ✅ Sends Slack alert
- ✅ Sends Email alert

#### 3. Block IP Address

```http
POST /api/containment/block-ip
Content-Type: application/json

{
  "ip": "192.168.1.100",
  "reason": "Brute force attack detected"
}
```

**Response:**
```json
{
  "success": true,
  "action": "IP Blocked",
  "ip": "192.168.1.100",
  "reason": "Brute force attack detected",
  "timestamp": "2026-01-03T10:50:00.000Z"
}
```

**Action Taken:**
```bash
# Executes on server:
sudo iptables -A INPUT -s 192.168.1.100 -j DROP
```

**Triggers:**
- ✅ Sends Slack containment alert
- ✅ Logs action in SIEM

#### 4. Incident Response Plan

```http
POST /api/incident-response
Content-Type: application/json

{
  "alerts": [...],
  "incidentType": "brute_force"
}
```

**Response:**
```json
{
  "responsePlan": "BLOCK THESE IPs NOW:\n192.168.1.100\n\nRUN THESE COMMANDS:\nsudo iptables -A INPUT -s 192.168.1.100 -j DROP\n\nCHECK THESE USERS:\nroot, admin\n\nIMMEDIATE ACTIONS:\n• Block attacker IPs\n• Review authentication logs\n• Rotate compromised credentials",
  "alertCount": 15,
  "timestamp": "2026-01-03T10:55:00.000Z"
}
```

**Triggers:**
- ✅ Sends Slack incident response alert
- ✅ Creates audit trail

#### 5. Execute Playbook

```http
POST /api/playbook/execute
Content-Type: application/json

{
  "playbookId": "pb-001",
  "playbookName": "Brute Force Protection",
  "trigger": "10+ failed SSH logins",
  "actions": ["Block IP", "Create case", "Alert SOC"],
  "targetIP": "192.168.1.100",
  "status": "success"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Playbook executed and alert sent",
  "timestamp": "2026-01-03T11:00:00.000Z"
}
```

**Triggers:**
- ✅ Sends Slack playbook execution alert
- ✅ Logs execution in SIEM

#### 6. Create Security Case

```http
POST /api/case/create
Content-Type: application/json

{
  "id": "CASE-001",
  "title": "Suspected Data Exfiltration",
  "description": "Unusual outbound traffic detected",
  "priority": "critical",
  "status": "open",
  "assignee": "analyst1"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Case created and alert sent",
  "caseId": "CASE-001",
  "timestamp": "2026-01-03T11:05:00.000Z"
}
```

**Triggers (for critical/high priority only):**
- ✅ Sends Slack case creation alert
- ✅ Creates case in tracking system

#### 7. AI Chatbot

```http
POST /api/chatbot
Content-Type: application/json

{
  "message": "What is a brute force attack?"
}
```

**Response:**
```json
{
  "response": "A brute force attack is when attackers systematically try multiple username and password combinations until finding the correct credentials. Your SIEM detects this by monitoring failed authentication attempts and alerting when thresholds are exceeded."
}
```

---

## 🔔 Alert System

### Alert Types

#### 1. General Security Alerts
**Trigger**: AI analysis completion  
**Channels**: Slack + Email  
**Format**:
```
🚨 SECURITY ALERT
Threat Level: High
Alert Count: 15
Summary: Multiple brute force attempts detected...
Top Threat IPs: 192.168.1.100, 45.33.32.156
```

#### 2. Critical Alerts
**Trigger**: Alert severity level ≥ 10  
**Channels**: Slack + Email  
**Format**:
```
🔴 CRITICAL SECURITY INCIDENT
Severity: CRITICAL
Incident: Multiple failed SSH login attempts
Source IP: 192.168.1.100
User: root
Action Required: Immediate investigation required
```

#### 3. Playbook Execution Alerts
**Trigger**: Automated playbook runs  
**Channels**: Slack  
**Format**:
```
✅ Automated Playbook Executed
Playbook: Brute Force Protection
Status: Success
Trigger: 10+ failed logins in 5 minutes
Actions: Block IP, Create case, Alert SOC
Target IP: 192.168.1.100
```

#### 4. Containment Action Alerts
**Trigger**: IP blocking or security hardening  
**Channels**: Slack  
**Format**:
```
🛡️ Containment Action Executed
Action: IP Blocked
Success: ✅ Yes
Blocked IP: 192.168.1.100
Reason: Brute force attack detected
```

#### 5. Incident Response Alerts
**Trigger**: AI response plan generation  
**Channels**: Slack  
**Format**:
```
⚡ Incident Response Plan Generated
Alert Count: 15
Incident Type: Brute Force Attack
Summary: Block IPs 192.168.1.100, investigate user accounts...
Immediate Actions: Review full response plan
```

#### 6. Case Creation Alerts
**Trigger**: Critical/High priority cases created  
**Channels**: Slack  
**Format**:
```
🔴 New Security Case: CASE-001
Priority: 🔴 CRITICAL
Status: Open
Title: Suspected Data Exfiltration
Description: Unusual outbound traffic detected
Assignee: analyst1
```

### Alert Configuration

**Slack Setup:**
```javascript
// In .env
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL

// Alert functions automatically called by:
- /api/analyze (analysis completion)
- /api/alerts (critical alerts detected)
- /api/containment/block-ip (IP blocking)
- /api/incident-response (response plan)
- /api/playbook/execute (playbook runs)
- /api/case/create (critical cases)
```

**Email Setup:**
```javascript
// In .env
EMAIL_SERVICE=gmail
EMAIL_USER=your-email@gmail.com
EMAIL_PASSWORD=your-gmail-app-password
EMAIL_TO=security-team@yourcompany.com

// HTML formatted emails sent for:
- AI analysis completion
- Critical alert detection
```

### Alert Customization

**Adjust Critical Alert Threshold:**
```javascript
// In server.js, line ~470
const criticalAlerts = alerts.filter(alert => 
  (alert.rule?.level >= 10 || alert.severity === 'critical')
);

// Change to >= 8 for more alerts:
const criticalAlerts = alerts.filter(alert => 
  (alert.rule?.level >= 8 || alert.severity === 'critical')
);
```

**Add Custom Slack Channels:**
```javascript
// Create separate webhooks for different channels:
const CRITICAL_WEBHOOK = process.env.SLACK_CRITICAL_WEBHOOK;
const PLAYBOOK_WEBHOOK = process.env.SLACK_PLAYBOOK_WEBHOOK;

// Route alerts to appropriate channels:
if (severity === 'critical') {
  await axios.post(CRITICAL_WEBHOOK, message);
} else {
  await axios.post(SLACK_WEBHOOK_URL, message);
}
```

---

## 🔐 Security Operations Workflow

### 1. Alert Triage (Tier 1 Analyst)

```mermaid
graph TD
    A[Alert Appears] --> B{Severity Check}
    B -->|Critical/High| C[Open Alert Drawer]
    B -->|Medium/Low| D[Review Later]
    C --> E{Threat Intel Check}
    E -->|Known Malicious| F[Escalate to Tier 2]
    E -->|Unknown/Clean| G{Context Analysis}
    G -->|Suspicious| F
    G -->|Likely Benign| H[Mark Resolved]
```

**Actions:**
- Review alert details in drawer
- Check source IP reputation
- Verify user/system context
- Determine if true positive or false positive

### 2. Investigation (Tier 2 Analyst)

```mermaid
graph TD
    A[Escalated Alert] --> B[Run AI Analysis]
    B --> C[Search Related Alerts]
    C --> D[Build Timeline]
    D --> E{Compromise Confirmed?}
    E -->|Yes| F[Generate Response Plan]
    E -->|No| G[Document Findings]
    F --> H[Escalate to IR Team]
```

**Actions:**
- Use AI analysis for pattern detection
- Correlate events across time/systems
- Identify attack stages (MITRE ATT&CK)
- Document evidence in case

### 3. Incident Response

```mermaid
graph TD
    A[Confirmed Incident] --> B[CONTAINMENT]
    B --> C[Block Attacker IPs]
    C --> D[Disable Compromised Accounts]
    D --> E[Isolate Affected Systems]
    E --> F[ERADICATION]
    F --> G[Remove Backdoors]
    G --> H[Patch Vulnerabilities]
    H --> I[Rotate Credentials]
    I --> J[RECOVERY]
    J --> K[Restore Systems]
    K --> L[Verify Security]
    L --> M[LESSONS LEARNED]
    M --> N[Update Detections]
    N --> O[Document Findings]
```

**Containment Actions:**
```bash
# Block IP
sudo iptables -A INPUT -s <ATTACKER_IP> -j DROP

# Disable account
sudo usermod -L <USERNAME>

# Isolate system
sudo iptables -A INPUT -j DROP
sudo iptables -A OUTPUT -j DROP
```

**Eradication Actions:**
```bash
# Remove backdoor users
sudo userdel -r <BACKDOOR_USER>

# Remove malicious cron jobs
sudo crontab -u <USER> -e

# Harden SSH
sudo sed -i 's/PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
sudo systemctl restart sshd
```

---

## 📜 Compliance & Regulatory

### PCI-DSS Requirements

**Requirement 10**: Track and monitor all access to network resources and cardholder data

| Requirement | Implementation |
|-------------|----------------|
| 10.2 - Audit Logs | ✅ Filebeat + Auditd capture all system events |
| 10.3 - Record Details | ✅ Logs include timestamp, user, action, result |
| 10.4 - Time Sync | ✅ NTP configured on all systems |
| 10.5 - Secure Logs | ✅ Centralized storage, access controls |
| 10.6 - Review Logs | ✅ Real-time dashboards + alerts |
| 10.7 - Retain Logs | ✅ Elasticsearch retention policies |

**Evidence for Auditors:**
- Kibana dashboards showing log review
- Alert configurations proving real-time monitoring
- Elasticsearch index lifecycle policies for retention

### HIPAA Security Rule

**§164.312(b) - Audit Controls**: Implement hardware, software, and/or procedural mechanisms that record and examine activity

| Requirement | Implementation |
|-------------|----------------|
| Audit Logs | ✅ All access to ePHI logged |
| Monitoring | ✅ Real-time SIEM monitoring |
| Incident Response | ✅ Documented IR procedures |
| Review Process | ✅ Daily dashboard reviews |

**Evidence for Auditors:**
- SIEM audit trail reports
- Incident response documentation
- Access logs for all ePHI systems

### SOC 2 Trust Service Criteria

**CC7.2**: The entity monitors system components and the operation of those components for anomalies

| Criterion | Implementation |
|-----------|----------------|
| Monitoring Tools | ✅ SIEM with Wazuh detection |
| Anomaly Detection | ✅ Baseline + AI analysis |
| Alerting | ✅ Multi-channel alerts |
| Documentation | ✅ All events logged |

**Evidence for Auditors:**
- SIEM configuration documentation
- Alert testing results
- Incident response logs

### GDPR Article 33

**Data Breach Notification**: Must notify within 72 hours of becoming aware

| Requirement | Implementation |
|-------------|----------------|
| Breach Detection | ✅ Real-time monitoring |
| 72-Hour Window | ✅ Immediate alerts enable fast response |
| Forensic Evidence | ✅ Complete audit trail |
| Notification Process | ✅ Automated alerting to DPO |

**Evidence for Regulators:**
- SIEM alert timestamps
- Incident response timelines
- Breach notification procedures

---

## 🚀 Scaling to Production

### Architecture Enhancements

#### Multi-Node Elasticsearch Cluster

```yaml
# elasticsearch.yml for 3-node cluster
cluster.name: siem-production
node.name: node-1
node.roles: [master, data, ingest]

network.host: 0.0.0.0
discovery.seed_hosts: ["node-1", "node-2", "node-3"]
cluster.initial_master_nodes: ["node-1", "node-2", "node-3"]

# Index lifecycle management
xpack.ilm.enabled: true
```

**Node Specifications:**
- **Master nodes**: 3 nodes, 4 vCPU, 16GB RAM each
- **Data nodes**: 5+ nodes, 8 vCPU, 32GB RAM, 500GB+ SSD each
- **Coordinating nodes**: 2 nodes, 4 vCPU, 8GB RAM each

#### High Availability Configuration

```
┌─────────────────────────────────────────────────┐
│            Load Balancer (Azure LB)             │
└────────────┬───────────────┬────────────────────┘
             │               │
     ┌───────▼──────┐ ┌─────▼────────┐
     │   Kibana 1   │ │   Kibana 2   │
     └───────┬──────┘ └──────┬───────┘
             │                │
     ┌───────▼────────────────▼─────────┐
     │  Elasticsearch Cluster (3 nodes) │
     └───────┬────────────────┬─────────┘
             │                │
     ┌───────▼──────┐ ┌──────▼───────┐
     │  Filebeat    │ │  Filebeat    │
     │  (1000+ VMs) │ │  (1000+ VMs) │
     └──────────────┘ └──────────────┘
```

### Index Lifecycle Management

```json
PUT _ilm/policy/siem-policy
{
  "policy": {
    "phases": {
      "hot": {
        "actions": {
          "rollover": {
            "max_size": "50GB",
            "max_age": "1d"
          }
        }
      },
      "warm": {
        "min_age": "7d",
        "actions": {
          "allocate": {
            "require": {
              "data": "warm"
            }
          }
        }
      },
      "cold": {
        "min_age": "30d",
        "actions": {
          "allocate": {
            "require": {
              "data": "cold"
            }
          }
        }
      },
      "delete": {
        "min_age": "90d",
        "actions": {
          "delete": {}
        }
      }
    }
  }
}
```

**Storage Tiers:**
- **Hot**: Days 0-7, SSD, fast searches
- **Warm**: Days 7-30, SSD/HDD hybrid, infrequent searches
- **Cold**: Days 30-90, HDD, rare searches
- **Delete**: After 90 days (adjust per compliance)

### Performance Optimization

```yaml
# Elasticsearch tuning
indices.memory.index_buffer_size: 30%
thread_pool.write.queue_size: 1000
search.max_buckets: 100000

# JVM heap (50% of RAM, max 31GB)
-Xms16g
-Xms16g
```

**Filebeat Tuning:**
```yaml
# filebeat.yml
queue.mem:
  events: 4096
  flush.min_events: 2048
  flush.timeout: 1s

output.elasticsearch:
  bulk_max_size: 5000
  worker: 4
```

### Monitoring Stack

```
┌─────────────────────────────────────────────┐
│         Prometheus + Grafana                │
│  • Elasticsearch cluster health             │
│  • Node resource utilization                │
│  • Ingestion rate metrics                   │
│  • Query performance                        │
│  • Alert on failures                        │
└─────────────────────────────────────────────┘
```

**Key Metrics:**
- Ingestion rate: Events per second
- Search latency: Average query time
- Index size: GB per day
- Heap usage: Percentage of allocated
- CPU/Memory: Per-node utilization

### Backup & Disaster Recovery

```bash
# Elasticsearch snapshot repository
PUT /_snapshot/azure_backup
{
  "type": "azure",
  "settings": {
    "account": "siem_backup",
    "container": "elasticsearch-snapshots",
    "base_path": "production"
  }
}

# Daily snapshot
PUT /_snapshot/azure_backup/snapshot_daily
{
  "indices": "filebeat-*,wazuh-*",
  "ignore_unavailable": true,
  "include_global_state": false
}
```

**Recovery Procedures:**
1. Restore Elasticsearch from snapshot (RPO: 24 hours)
2. Redeploy Filebeat to all systems
3. Verify log ingestion
4. Test alerting pipelines

### Geographic Distribution

For global enterprises:

```
┌────────────────────────────────────────────┐
│          Region: US East                   │
│  Elasticsearch Cluster (Primary)           │
│  • Cross-region replication to EU/Asia     │
│  • Local Filebeat → Local cluster          │
│  • Aggregate critical alerts centrally     │
└────────────────────────────────────────────┘
```

**Benefits:**
- Reduced latency for distributed teams
- Compliance with data residency laws
- Resilience against regional outages

---

## 📸 Screenshots

### Main Dashboard
![Dashboard](docs/screenshots/dashboard.png)
*Real-time security monitoring interface with alert feed and analytics*

### Alert Drawer
![Alert Details](docs/screenshots/alert-drawer.png)
*Detailed forensic view with MITRE ATT&CK mapping and quick actions*

### AI Analysis
![AI Summary](docs/screenshots/ai-analysis.png)
*Claude AI analyzing security patterns and providing threat intelligence*

### Incident Response Plan
![Response Plan](docs/screenshots/incident-response.png)
*AI-generated step-by-step response plan with copy-paste commands*

### Playbooks
![Playbooks](docs/screenshots/playbooks.png)
*Automated response playbooks for common attack scenarios*

### AI Chatbot
![Chatbot](docs/screenshots/chatbot.png)
*Conversational AI assistant for security questions and guidance*

### Slack Alerts
![Slack](docs/screenshots/slack-alerts.png)
*Multi-channel alerts via Slack for immediate team notification*

---

## 🐛 Troubleshooting

### Common Issues

#### 1. Elasticsearch Connection Failed

**Symptom**: `ConnectionError` in server logs

**Solutions:**
```bash
# Check Elasticsearch status
sudo systemctl status elasticsearch

# Verify Elasticsearch is listening
curl -X GET "localhost:9200/?pretty"

# Check credentials in .env
ES_NODE=http://localhost:9200
ES_USERNAME=elastic
ES_PASSWORD=<correct_password>

# Reset Elasticsearch password
sudo /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
```

#### 2. No Alerts Appearing

**Symptom**: Dashboard shows 0 alerts

**Solutions:**
```bash
# Check Filebeat status
sudo systemctl status filebeat

# Verify Filebeat is sending data
sudo filebeat test output

# Check Elasticsearch indices
curl -X GET "localhost:9200/_cat/indices?v"

# Manual log ingestion test
sudo journalctl -u ssh -n 50 --no-pager
```

#### 3. AI Analysis Not Working

**Symptom**: "API unavailable" or "Failed to analyze"

**Solutions:**
```bash
# Verify Anthropic API key
echo $ANTHROPIC_API_KEY

# Test API key
curl https://api.anthropic.com/v1/messages \
  -H "x-api-key: $ANTHROPIC_API_KEY" \
  -H "anthropic-version: 2023-06-01" \
  -H "content-type: application/json" \
  -d '{"model":"claude-sonnet-4-20250514","max_tokens":100,"messages":[{"role":"user","content":"test"}]}'

# Check server logs
tail -f /var/log/siem/server.log
```

#### 4. Slack Alerts Not Sending

**Symptom**: No messages in Slack channel

**Solutions:**
```bash
# Test webhook manually
curl -X POST $SLACK_WEBHOOK_URL \
  -H 'Content-Type: application/json' \
  -d '{"text":"Test alert"}'

# Verify webhook URL format
# Should be: https://hooks.slack.com/services/T.../B.../...

# Check server logs for Slack errors
grep "Slack" /var/log/siem/server.log

# Verify webhook permissions in Slack app settings
```

#### 5. Email Alerts Not Sending

**Symptom**: No emails received

**Solutions:**
```bash
# Verify Gmail app password (not regular password!)
echo $EMAIL_PASSWORD

# Test SMTP connection
node -e "
const nodemailer = require('nodemailer');
const transporter = nodemailer.createTransport({
  service: 'gmail',
  auth: { user: '$EMAIL_USER', pass: '$EMAIL_PASSWORD' }
});
transporter.verify((err, success) => {
  console.log(err || 'SMTP OK');
});
"

# Check Gmail "Less secure app access" (should be OFF, use app password)
# Enable 2FA + App Passwords at: https://myaccount.google.com/security
```

#### 6. High Memory Usage

**Symptom**: Server becomes slow or crashes

**Solutions:**
```bash
# Check memory usage
free -h
top

# Reduce Elasticsearch heap if needed
sudo nano /etc/elasticsearch/jvm.options
# Set: -Xms4g -Xmx4g (for 8GB RAM VM)

# Restart Elasticsearch
sudo systemctl restart elasticsearch

# Consider upgrading VM size
az vm resize --resource-group siem-rg --name siem-analyzer --size Standard_D4s_v3
```

---

## 🔮 Future Enhancements

### Planned Features

#### 1. JARVIS Voice Copilot 🎙️
```
Voice-activated AI security assistant:
- "JARVIS, analyze critical alerts"
- "JARVIS, what's our threat level?"
- "JARVIS, block IP 192.168.1.100"
- "JARVIS, generate incident report"

Technology: Web Speech API + Claude AI
Status: In Development
```

#### 2. Advanced AI Features

**AI Alert Correlation:**
- Machine learning to detect multi-stage attacks
- Behavioral anomaly detection
- Automatic alert grouping/deduplication

**Natural Language Queries:**
```
"Show me all failed logins from China in the last week"
"Which users accessed the database at 3 AM?"
"Alert me if anyone tries to escalate privileges"
```

**AI Shift Handoff Reports:**
- Automated daily/weekly summaries
- Key incidents and resolutions
- Trending threats
- Recommended actions for next shift

#### 3. Auto-Block Rules Engine

```
Rule: Block brute force attempts
IF failed_logins > 10 WITHIN 5 minutes
THEN block_ip FOR 24 hours
AND notify_soc
```

**Features:**
- Visual rule builder
- Whitelist/blacklist management
- Time-based rules (e.g., "after hours only")
- Threat intelligence integration

#### 4. Risk Scoring Dashboard

```
┌────────────────────────────────────────┐
│  ORGANIZATIONAL RISK SCORE: 72/100    │
│  🔴 Critical Risk                     │
├────────────────────────────────────────┤
│  Top Risk Factors:                    │
│  • Unpatched systems: 15 servers      │
│  • Weak passwords: 23 accounts        │
│  • Outdated software: 8 applications  │
│  • Open ports: 12 unnecessary         │
└────────────────────────────────────────┘
```

**Scoring Factors:**
- Vulnerability scan results
- Patch compliance
- Configuration assessment
- Attack surface analysis

#### 5. Mobile App

**Features:**
- Push notifications for critical alerts
- Quick actions: Block IP, Acknowledge alert
- Dashboard overview
- Offline mode with sync

**Platforms:**
- iOS (Swift)
- Android (Kotlin)

#### 6. Threat Intelligence Feeds

**Integration:**
- AlienVault OTX
- VirusTotal
- AbuseIPDB
- Malware Bazaar
- Shodan

**Features:**
- Automatic IP reputation checks
- Malware hash verification
- Domain reputation scoring
- Indicator of Compromise (IOC) matching

#### 7. SOAR Integration

**Security Orchestration, Automation, and Response:**
- Integrate with ticketing systems (Jira, ServiceNow)
- Automated playbook orchestration
- Case management workflows
- Remediation tracking

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

### Reporting Bugs

```
Issue Title: [Bug] Brief description

Environment:
- OS: Ubuntu 24.04
- Node.js: v18.x
- Elasticsearch: 8.x

Steps to Reproduce:
1. Step one
2. Step two

Expected Behavior:
What should happen

Actual Behavior:
What actually happens

Logs:
```paste relevant logs```
```

### Feature Requests

```
Issue Title: [Feature] Brief description

Use Case:
Why is this feature needed?

Proposed Solution:
How should it work?

Alternatives Considered:
Other approaches you've thought about
```

### Pull Requests

1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open Pull Request

**PR Guidelines:**
- Include tests if applicable
- Update documentation
- Follow existing code style
- Describe what and why (not just what)

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2026 SIEM AI Analyzer Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 📞 Contact & Support

- **Project Repository**: https://github.com/kiransairammuntha/AI-Driven-SIEM-Analyzer-for-Automated-SOC-Threat-Detection-Response
- **Issues**: https://github.com/kiransairammuntha/AI-Driven-SIEM-Analyzer-for-Automated-SOC-Threat-Detection-Response/issues
- **Discussions**: https://github.com/kiransairammuntha/AI-Driven-SIEM-Analyzer-for-Automated-SOC-Threat-Detection-Response/discussions
---

## 🙏 Acknowledgments

- **Elastic** for Elasticsearch, Kibana, and Filebeat
- **Wazuh** for open-source SIEM capabilities
- **Anthropic** for Claude AI API
- **Chart.js** for visualization library
- **Microsoft Azure** for cloud infrastructure
- **Open Source Community** for invaluable tools and support

---

## 📊 Project Stats

![GitHub stars](https://img.shields.io/github/stars/kiransairammuntha/SIEM-AI-Analyzer?style=social)
![GitHub forks](https://img.shields.io/github/forks/kiransairammuntha/SIEM-AI-Analyzer?style=social)
![GitHub issues](https://img.shields.io/github/issues/kiransairammuntha/SIEM-AI-Analyzer)
![GitHub pull requests](https://img.shields.io/github/issues-pr/kiransairammuntha/SIEM-AI-Analyzer)

---

<div align="center">

**Built with ❤️ for Security Operations Centers worldwide**

[⬆ Back to Top](#-siem-ai-analyzer---enterprise-security-operations-center)

</div>
