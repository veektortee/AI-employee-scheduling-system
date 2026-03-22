# Medical Staff Scheduling System

A modern, high-performance scheduling optimization system for medical staff built with **Next.js**, **FastAPI**, and **Google OR-Tools**.

## 🏥 Overview

This system provides comprehensive staff scheduling optimization for hospitals and medical facilities with:

- **Web-based Interface**: Modern React-based UI hosted on Vercel
- **High-Performance Solver**: Local FastAPI service with OR-Tools optimization
- **Real-time Updates**: WebSocket-powered progress tracking
- **Advanced Constraints**: Complex scheduling rules and preferences
- **Multiple Solutions**: Generate diverse scheduling alternatives
- **Excel Export**: Professional schedule outputs

## 🏗️ Architecture

- **Frontend**: Next.js 14 + TypeScript + Tailwind CSS (Vercel-hosted)
- **Backend**: FastAPI + OR-Tools + WebSockets (Local service)
- **Database**: File-based JSON cases (extensible to PostgreSQL/MongoDB)
- **Authentication**: NextAuth.js with credential recovery
- **Real-time**: WebSocket + polling fallback for progress updates

## 🚀 Quick Start

### 1. Clone and Install

```bash
git clone <repository-url>
cd scheduling-webapp

# Install Node.js dependencies
npm install

# Install Python dependencies  
pip install -r requirements.txt
```

### 2. Start Services

**Option A: Windows Quick Start**

```cmd
# Start solver service (double-click or run in cmd)
start_solver.bat

# In new terminal, start web app
npm run dev
```

**Option B: Manual Start**

```bash
# Terminal 1: Start FastAPI solver service
python fastapi_solver_service.py

# Terminal 2: Start Next.js web application
npm run dev
```

### 3. Access Application

For normal use, access the application through the deployed web interface using this [link](https://mlsched.com). Access is restricted to authorized users. The local URLs below are intended for development or running the system on your own machine.

- **Web App (Local)**: http://localhost:3000  
- **Solver API**: http://localhost:8000  
- **API Docs**: http://localhost:8000/docs

- **Web App**: http://localhost:3000
- **Solver API**: http://localhost:8000
- **API Docs**: http://localhost:8000/docs

## ⚙️ System Requirements

- **Node.js**: 18.17+
- **Python**: 3.8+
- **RAM**: 4GB+ (8GB+ recommended for large cases)
- **CPU**: Multi-core recommended for OR-Tools
- **OS**: Windows 10+, macOS, Linux

## 📊 Features

### Scheduling Optimization

- **OR-Tools CP-SAT Solver**: Google’s advanced constraint programming
- **Multi-objective Optimization**: Balance fairness, preferences, and constraints
- **Complex Constraints**: Provider types, availability, consecutive days, rest periods
- **Shift Types**: Day, night, weekend shifts with type-specific rules
- **Provider Preferences**: Hard/soft availability preferences

### User Interface

- **Modern Design**: Responsive, dark/light mode, professional styling
- **Real-time Progress**: Live optimization progress with WebSocket updates
- **Interactive Calendar**: Visual scheduling calendar with drag-drop
- **Provider Management**: Comprehensive provider profiles and preferences
- **Configuration**: Flexible solver weights and constraint settings

### Output & Export

- **Excel Export**: Professional schedule grids and calendar views
- **Multiple Formats**: JSON, Excel, CSV output options
- **Statistics**: Detailed optimization metrics and provider workloads
- **Diagnostics**: Constraint violation analysis and suggestions

## 🔧 Configuration

### Environment Variables

Create `.env.local`:

```env
# Authentication
NEXTAUTH_SECRET=your-secret-key
NEXTAUTH_URL=http://localhost:3000

# Solver Service
SOLVER_SERVICE_URL=http://localhost:8000
SOLVER_TIMEOUT=30000

# Optional: Email service for credential recovery  
EMAIL_SERVICE_ENABLED=false
```

### Solver Configuration

Edit constants in your scheduling cases:

```json
{
  "constants": {
    "solver": {
      "max_time_in_seconds": 300,
      "num_threads": 8,
      "relative_gap": 0.01
    },
    "weights": {
      "hard": {
        "slack_unfilled": 20,
        "slack_cant_work": 20
      },
      "soft": {
        "cluster_size": 15,
        "requested_off": 3
      }
    }
  }
}
```

## 📚 Documentation

- **[FastAPI Setup Guide](./FASTAPI_SETUP_GUIDE.md)**: Detailed solver service setup
- **[API Documentation](http://localhost:8000/docs)**: Interactive API reference (when running)
- **[Constraint Guide](./CONSTRAINT_GUIDE.md)**: Scheduling constraints and rules
- **[Deployment Guide](./DEPLOYMENT_GUIDE.md)**: Production deployment options

## 🐛 Troubleshooting

### Common Issues

#### Cannot connect to solver service

```bash
# Check if service is running
curl http://localhost:8000/health

# Restart service
python fastapi_solver_service.py
```

#### Import errors (OR-Tools, FastAPI)

```bash
# Reinstall Python dependencies
pip install --upgrade -r requirements.txt

# Or install individually
pip install ortools fastapi uvicorn
```

#### Performance issues

- Increase `max_time_in_seconds` for large problems
- Use `num_threads` matching your CPU cores
- Monitor system memory usage
- Close other applications during optimization

### Performance Benchmarks

|Problem Size              |Typical Runtime|Memory Usage|
|--------------------------|---------------|------------|
|50 shifts, 10 providers   |5-30 seconds   |1-2 GB      |
|200 shifts, 25 providers  |1-5 minutes    |2-4 GB      |
|500+ shifts, 50+ providers|5-15 minutes   |4-8 GB      |

## 🔒 Security Features

- **Authentication**: Secure login with account lockout protection
- **Credential Recovery**: Email-based credential recovery system
- **Session Management**: Secure session handling with NextAuth.js
- **Input Validation**: Comprehensive input sanitization
- **Local Processing**: Sensitive data processed locally (not cloud)

## 🚢 Deployment

### Local Development

- Perfect for testing and small-scale use
- Full feature access
- Easy debugging and customization

### Production Options

1. **Self-hosted**: Deploy to your own servers
1. **Docker**: Containerized deployment
1. **Cloud**: AWS/Azure/GCP with local solver instances
1. **Hybrid**: Vercel frontend + self-hosted solver service

See [Deployment Guide](./DEPLOYMENT_GUIDE.md) for detailed instructions.

## 🤝 Contributing

1. Fork the repository
1. Create feature branch: `git checkout -b feature/amazing-feature`
1. Commit changes: `git commit -m 'Add amazing feature'`
1. Push to branch: `git push origin feature/amazing-feature`
1. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the <LICENSE> file for details.

## 🆘 Support

- **Issues**: GitHub Issues for bugs and feature requests
- **Documentation**: Check `/docs` folder for detailed guides
- **API Reference**: http://localhost:8000/docs (when solver is running)

## 🙏 Acknowledgments

- **Google OR-Tools**: Advanced optimization engine
- **FastAPI**: High-performance API framework
- **Next.js**: Modern React framework
- **Vercel**: Excellent hosting platform
- **Tailwind CSS**: Beautiful, responsive styling

-----

**Ready to optimize your medical staff scheduling!** 🏥
