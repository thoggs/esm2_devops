# ESM2 Infrastructure Project

This project sets up a Docker Swarm infrastructure for the ESM2 project, including services for backend, frontend,
monitoring, and a PostgreSQL database. The project uses Ansible to automate the deployment and configuration of these
services.

## Project Structure

```bash
├── inventories/          # Inventory files for Ansible
│   └── hosts.ini         # Host definitions for Ansible playbooks
├── playbooks/            # Ansible playbooks to deploy different parts of the stack
│   ├── backend-playbook.yml
│   ├── check-stack-status.yml
│   ├── db-playbook.yml
│   ├── docker-playbook.yml
│   ├── esm2-playbook.yml
│   ├── frontend-playbook.yml
│   ├── monitoring-playbook.yml
│   └── populate-db-playbook.yml
├── stacks/               # Docker stack definitions for different services
│   ├── esm2/
│   │   ├── backend/      # Backend service configuration
│   │   ├── db/           # Database service configuration and SQL scripts
│   │   └── frontend/     # Frontend service configuration
│   └── monitoring/       # Monitoring services (Grafana, Prometheus, etc.)
│       ├── blackbox/
│       ├── grafana/
│       ├── loki/
│       ├── opentelemetry/
│       ├── prometheus/
│       ├── promtail/
│       └── docker-compose-monitoring.yml
├── vars/                 # Variable definitions and secrets for Ansible
│   └── secrets/
│       └── create-secrets.yml
├── env.yml               # Environment variables for the Ansible playbooks
└── README.md             # Project documentation
```

## Installation

### Install Ansible

To install Ansible on your machine, run the following commands:

```bash
sudo apt update && sudo apt install -y python3-pip
```

```bash
python3 -m pip install --user ansible --break-system-packages
```

### Update Ansible

To update your Ansible version, use this command:

```bash
python3 -m pip install --upgrade --user ansible --break-system-packages
```

### Add Ansible to PATH

Make sure Ansible is available in your terminal by adding it to your PATH:

```bash
echo 'export PATH=$PATH:$HOME/.local/bin' >> ~/.bashrc
```

```bash
source ~/.bashrc
```

## Running the Playbooks

### Running the Full ESM2 Playbook

To run the complete setup of the ESM2 infrastructure, use the following command:

```bash
ansible-playbook -i inventories/hosts.ini playbooks/esm2-playbook.yml
```

### Running Playbook with Specific Tags

If you want to run only a specific part of the setup, you can use tags. For example, to run only the backend playbook:

```bash
ansible-playbook -i inventories/hosts.ini playbooks/esm2-playbook.yml --tags "backend"
```

Multiple tags can be specified by separating them with a comma.

```bash
ansible-playbook -i inventories/hosts.ini playbooks/esm2-playbook.yml --tags "backend,frontend,db"
```

### Playbook Tags

Each part of the infrastructure is tagged to allow selective execution:

- `docker`: For Docker installation and setup.
- `db`: For setting up the PostgreSQL database.
- `backend`: For deploying the backend services.
- `frontend`: For deploying the frontend services.
- `monitoring`: For setting up monitoring tools like Grafana, Prometheus, etc.
- `populate-db`: For populating the database with initial data.
- `check-status`: For verifying the status of the deployed services.

## License

This project is licensed under the Siemens License.
