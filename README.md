# Docker Odoo Setup

A complete Odoo development environment using Docker Compose with PostgreSQL database and custom addons support.

## 🚀 Quick Start

### Prerequisites
- Docker
- Docker Compose

### Installation & Setup

1. **Clone or download this repository**
2. **Navigate to the project directory:**
   ```bash
   cd odoo
   ```

3. **Start the services:**
   ```bash
   docker-compose up --build
   ```

4. **Access Odoo:**
   - Open your browser and go to: `http://localhost:8069`
   - Database: `odoo`
   - Email: `admin`
   - Password: `admin`

## 📁 Project Structure

```
odoo/
├── docker-compose.yml          # Docker Compose configuration
├── README.md                   # This documentation file
├── addons/                     # Directory for custom Odoo modules
└── config/
    └── odoo.conf              # Odoo configuration file
```

## ⚙️ Configuration

### Docker Services
- **PostgreSQL 13**: Database service running on port 5433
- **Odoo 17**: Application service running on port 8069
- **Custom Network**: Isolated network for services
- **Persistent Volumes**: Data persistence for database and Odoo files

### Odoo Configuration
- **Admin Password**: `admin`
- **XML-RPC Port**: `8069`
- **Database Host**: `db` (Docker service name)
- **Database User**: `odoo`
- **Database Password**: `odoo`
- **Database Port**: `5432`
- **Addons Path**: `/mnt/extra-addons`

## 🔧 Usage

### Starting Services
```bash
# Start in background
docker-compose up -d

# Start with build (recommended for first run)
docker-compose up --build

# Start and view logs
docker-compose up
```

### Stopping Services
```bash
# Stop services
docker-compose down

# Stop and remove volumes (⚠️ WARNING: This will delete all data)
docker-compose down -v
```

### Viewing Logs
```bash
# View all logs
docker-compose logs

# View specific service logs
docker-compose logs odoo
docker-compose logs db
```

### Accessing Database
```bash
# Connect to PostgreSQL
docker-compose exec db psql -U odoo -d odoo
```

## 📦 Custom Addons

Place your custom Odoo modules in the `addons/` directory. They will be automatically available in Odoo.

### Example Addon Structure:
```
addons/
└── my_custom_module/
    ├── __init__.py
    ├── __manifest__.py
    ├── models/
    ├── views/
    └── ...
```

## 🔄 Development Workflow

1. **First Run**: The setup initializes the base module and stops after initialization
2. **Subsequent Runs**: Comment out the first command and uncomment the appropriate command based on your needs
3. **Module Updates**: Use the update command for specific modules

### Available Commands (in docker-compose.yml):
```yaml
# First time initialization
command: ["odoo", "-d", "odoo", "-i", "base", "--stop-after-init"]

# Update specific module
#command: ["odoo", "-d", "odoo", "-u", "money_management", "--without-demo-all"]

# Install specific module
#command: ["--", "-i", "base"]
```

## 🛠️ Troubleshooting

### Common Issues

1. **Port Already in Use**
   - Change ports in `docker-compose.yml` if 8069 or 5433 are occupied

2. **Permission Issues**
   - Ensure Docker has proper permissions to access the project directory

3. **Database Connection Issues**
   - Verify the database service is running: `docker-compose ps`
   - Check logs: `docker-compose logs db`

4. **Image Pull Issues**
   - Run: `docker pull odoo:17` and `docker pull postgres:13`

### Useful Commands
```bash
# Check service status
docker-compose ps

# Restart services
docker-compose restart

# Rebuild and start
docker-compose up --build

# Clean up everything
docker-compose down -v --remove-orphans
```

## 📝 Notes

- PostgreSQL runs on port 5433 on the host to avoid conflicts with local PostgreSQL installations
- All Odoo data is persisted in Docker volumes
- The setup includes demo data by default
- Custom modules in the `addons/` directory are automatically loaded

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is open source and available under the [MIT License](LICENSE). 