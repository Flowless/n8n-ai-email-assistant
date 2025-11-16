# n8n AI Email Assistant

A self-hosted n8n automation setup featuring an AI-powered email assistant for managing cybersecurity freelancer communications.

## Overview

This repository contains a Docker-based n8n installation with a pre-configured AI agent workflow designed to help process and categorize emails efficiently. The setup includes persistent data storage and custom input directories for seamless automation workflows.

## Features

- **Self-hosted n8n instance** running via Docker Compose
- **AI Email Assistant Agent** with Gmail integration
- Persistent workflow and configuration storage
- Custom input directory mounting for file processing
- Timezone configured for Europe/Stockholm

## Quick Start

### Prerequisites

- Docker and Docker Compose installed
- Gmail account credentials (for email processing workflows)

### Installation

1. Clone the repository:
```bash
git clone <your-repo-url>
cd n8n
```

2. Start the n8n container:
```bash
docker-compose up -d
```

3. Access n8n at `http://localhost:5678`

## Directory Structure

```
.
├── docker-compose.yml          # Docker configuration
├── n8n_data/                   # Persistent n8n data (workflows, credentials, settings)
├── input_wsl/                  # Mounted input directory for file processing
├── workflows/                  # Exported workflow JSON files
│   └── AI Email Assistant.json   # AI email assistant workflow
└── README.md
```

## Included Workflows

### AI Email Assistant

A sophisticated AI agent designed to:

- **Email Processing**: Read and analyze emails from Gmail inbox (your-email@example.com)
- **Smart Categorization**: Automatically categorize emails by priority (URGENT, HIGH, MEDIUM, LOW)
- **Security Awareness**: Flag phishing attempts and suspicious content
- **Actionable Summaries**: Extract key points, deadlines, and action items
- **Daily Digest**: Generate organized email summaries

**Key Features:**
- Chat trigger interface for interactive communication
- Context-aware memory (10-message window)
- Gmail integration for email retrieval
- Professional categorization for cybersecurity business context

**Security & Privacy:**
- Read-only Gmail access
- No automatic email sending
- Confidential client data protection
- Suspicious email verification required

### Importing Workflows

1. Navigate to n8n UI at `http://localhost:5678`
2. Go to **Workflows** → **Import from File**
3. Select the workflow JSON from the `workflows/` directory
4. Configure Gmail credentials when prompted

## Configuration

### Docker Compose Settings

- **Port**: 5678 (host:container)
- **Timezone**: Europe/Stockholm
- **Restart Policy**: unless-stopped
- **Volumes**:
  - `./n8n_data` → n8n configuration and data
  - `./input_wsl` → Custom input directory for file processing

### Environment Variables

Modify `docker-compose.yml` to customize:
- `TZ`: Timezone setting
- `N8N_HOST`: Hostname
- `N8N_PORT`: Internal port
- `N8N_PROTOCOL`: HTTP/HTTPS protocol

## Usage

### Managing the Container

```bash
# Start n8n
docker-compose up -d

# Stop n8n
docker-compose down

# View logs
docker-compose logs -f

# Restart n8n
docker-compose restart
```

### Backing Up Data

The `n8n_data/` directory contains all workflows, credentials, and settings. Back it up regularly:

```bash
tar -czf n8n_backup_$(date +%Y%m%d).tar.gz n8n_data/
```

### Exporting Workflows

1. Open workflow in n8n UI
2. Click **...** menu → **Download**
3. Save to `workflows/` directory
4. Commit to version control

## Development

### Adding New Workflows

1. Create workflows in the n8n UI
2. Export as JSON
3. Save to `workflows/` directory
4. Document functionality in this README

### Custom Nodes

Install custom nodes via the n8n UI:
- Settings → Community Nodes → Install
- Or add to `docker-compose.yml` environment variables

## Troubleshooting

### Container Won't Start
```bash
# Check logs
docker-compose logs

# Verify port availability
sudo lsof -i :5678
```

### Permission Issues
```bash
# Fix n8n_data permissions
sudo chown -R 1000:1000 n8n_data/
```

### Workflows Not Persisting
Ensure the `./n8n_data` volume mount is correctly configured in `docker-compose.yml`

## Security Notes

- This setup uses HTTP (not HTTPS) and is intended for local/development use
- For production deployment, configure SSL/TLS termination
- Store sensitive credentials using n8n's built-in credential management
- Never commit actual credentials to version control
- Review the AI agent's Gmail permissions regularly

## License

This configuration is provided as-is for personal use.

## Contributing

Feel free to submit issues or pull requests for improvements to workflows or configuration.
