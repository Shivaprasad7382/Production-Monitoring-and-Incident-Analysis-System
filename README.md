 🖥️ Production Monitoring & Incident Analysis System

A Flask-based web application for real-time system log capture, application health monitoring, and incident lifecycle management — backed by MySQL.

---

## 📌 Features

- **System Log Capture** — Ingest logs from any service via REST API with level filtering (INFO / WARNING / ERROR / CRITICAL)
- **Incident Management** — Create, track, and resolve incidents with severity levels and assignment
- **Health Monitoring** — Record and query live health status for all services
- **Operational Reports** — Auto-generated 24h summaries covering log volume, incidents, and service performance
- **Live Dashboard** — Dark-themed web UI showing service health and log level breakdown
- **Error Handling** — Structured exception handling for API and database failures with full logging

---

## 🛠️ Tech Stack

| Layer      | Technology              |
|------------|-------------------------|
| Backend    | Python 3.10+, Flask 3.x |
| Database   | MySQL 8.x               |
| ORM/Driver | mysql-connector-python  |
| Frontend   | HTML5, CSS3 (Jinja2)    |

---

## 📁 Project Structure

```
project1/
├── app.py                  # Main Flask application
├── schema.sql              # Database schema + seed data
├── requirements.txt        # Python dependencies
├── app.log                 # Runtime log output (auto-generated)
└── templates/
    └── dashboard.html      # Monitoring dashboard UI
```

---

## ⚙️ Setup & Installation

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/production-monitoring-system.git
cd production-monitoring-system
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Configure the database
Edit `app.py` and update the `DB_CONFIG` section:
```python
DB_CONFIG = {
    "host": "localhost",
    "user": "your_mysql_user",
    "password": "your_mysql_password",
    "database": "monitoring_db"
}
```

### 4. Initialize the database
```bash
mysql -u root -p < schema.sql
```

### 5. Run the application
```bash
python app.py
```

Visit: [http://localhost:5000](http://localhost:5000)

---

## 🔌 API Endpoints

### Logs
| Method | Endpoint       | Description              |
|--------|----------------|--------------------------|
| POST   | `/api/logs`    | Capture a new log entry  |
| GET    | `/api/logs`    | Retrieve logs (filterable by service, level, limit) |

**POST `/api/logs` — Example payload:**
```json
{
  "service_name": "auth-service",
  "log_level": "ERROR",
  "message": "Failed to connect to user database"
}
```

---

### Incidents
| Method | Endpoint                          | Description               |
|--------|-----------------------------------|---------------------------|
| POST   | `/api/incidents`                  | Create a new incident     |
| GET    | `/api/incidents`                  | List all incidents        |
| PUT    | `/api/incidents/<id>/resolve`     | Mark incident as resolved |

**POST `/api/incidents` — Example payload:**
```json
{
  "title": "DB Connection Failure",
  "description": "Primary database unreachable",
  "severity": "CRITICAL",
  "service_name": "db-service",
  "assigned_to": "dba-team"
}
```

---

### Health Checks
| Method | Endpoint      | Description                        |
|--------|---------------|------------------------------------|
| POST   | `/api/health` | Record a service health status     |
| GET    | `/api/health` | Get latest health for all services |

---

### Reports
| Method | Endpoint               | Description                        |
|--------|------------------------|------------------------------------|
| GET    | `/api/reports/summary` | Operational summary for last 24h   |

---

## 🗄️ Database Schema

```
system_logs     — id, service_name, log_level, message, source_ip, created_at
incidents       — id, title, description, severity, status, service_name, assigned_to, created_at, resolved_at
health_checks   — id, service_name, status, response_time_ms, error_message, checked_at
```

---

## 📊 Dashboard Preview

The dashboard (at `/`) provides:
- Total log count & open incident count
- Per-service health status badges (UP / DOWN / DEGRADED)
- Log level distribution table

---

## 🚀 Deployment Notes

- Set `debug=False` in `app.run()` for production
- Use environment variables for DB credentials (`.env` + `python-dotenv`)
- Consider using Gunicorn + Nginx for production serving

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.
