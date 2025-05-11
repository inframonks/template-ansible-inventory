# Ansible Projekt mit versionierten Rollen und Collections

Dieses Repository enthält ein strukturiertes Ansible-Setup mit eigenen Rollen, externen Collections und klar definiertem Inventory.

---

## 🔧 Voraussetzungen

- Python 3.x (empfohlen: Ubuntu 22.04+ / 24.04)
- Ansible >= 2.15 (empfohlen via `pip`)
- Git
- SSH-Zugriff auf Zielsysteme

Installiere Ansible lokal:
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install ansible
```

---

## 📦 Installation der Rollen & Collections

```bash
# Rollen installieren
ansible-galaxy role install -r requirements.yml -p roles/

# Collections installieren
ansible-galaxy collection install -r requirements.yml -p collections/
```

Diese werden lokal in ./roles/ und ./collections/ abgelegt.

---

## 🗂 Projektstruktur

Hier ist eine erweiterte, saubere Projektstruktur mit einer klaren Trennung von:
```bash
  • inventory/hosts.yml
  • inventory/group_vars/<group>.yml
  • inventory/host_vars/<hostname>/<details>.yml
```

Das Setup eignet sich hervorragend für größere Ansible-Projekte mit gepflegten Rollen, Versionierung und Mandantentrennung.

```bash
.
├── ansible.cfg
├── requirements.yml
├── roles/
│   └── proxmox_automatic/
├── collections/
│   └── ansible_collections/
├── inventory/
│   ├── hosts.yml
│   ├── group_vars/
│   │   ├── all/
│   │   │   ├── main.yml
│   │   │   └── proxy.yml
│   │   ├── proxmox/
│   │   │   ├── main.yml
│   │   │   ├── firewall.yml
│   │   │   └── secrets.yml
│   │   ├── helper/
│   │   │   └── main.yml
│   └── host_vars/
│       ├── pve01/
│       │   ├── main.yml
│       │   ├── network.yml
│       │   └── secrets.yml
│       ├── pve02/
│       │   ├── main.yml
│       │   ├── network.yml
│       │   └── secrets.yml
│       ├── pve03/
│       │   ├── main.yml
│       │   ├── network.yml
│       │   └── secrets.yml
│       └── shell01/
│           └── main.yml
├── playbooks/
│   └── site.yml
├── ansible.log
└── README.md
```

---

## 🧪 Beispielausführung

```bash
ansible-playbook playbooks/setup.yml --limit testhost --tags common
```

---

## 🛠 Pflege

**Rollen oder Collections aktualisieren**

```bash
# Alte Inhalte löschen
rm -rf roles/* collections/*

# Neu installieren
ansible-galaxy role install -r requirements.yml -p roles/
ansible-galaxy collection install -r requirements.yml -p collections/
```