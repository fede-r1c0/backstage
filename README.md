# 🚀 Backstage IDP Platform

[![Docker Build](https://github.com/fede-r1c0/backstage/actions/workflows/docker-build.yml/badge.svg)](https://github.com/fede-r1c0/backstage/actions/workflows/docker-build.yml)
[![Security Scan](https://github.com/fede-r1c0/backstage/actions/workflows/security-scan.yml/badge.svg)](https://github.com/fede-r1c0/backstage/actions/workflows/security-scan.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **Internal Developer Platform (IDP)** built with [Backstage](https://backstage.io/) for infrastructure self-service, service catalog management, and developer productivity tools.

## 🎯 Overview

This project implements a professional-grade Internal Developer Platform using **Backstage** as the foundation. The platform is designed to run on a **homelab Kubernetes cluster** (k3s + Cilium) and serves as a learning environment for real-world DevOps practices while maintaining production-grade standards.

### ✨ Key Features

- 🏗️ **Infrastructure Self-Service**: Automated resource provisioning and management
- 📚 **Service Catalog**: Centralized discovery and documentation of services
- 🔌 **Plugin Ecosystem**: Extensible platform with popular Backstage plugins
- ☸️ **Kubernetes Native**: Designed for k3s with Cilium CNI
- 🚀 **GitOps Deployment**: ArgoCD-managed deployments
- 🔒 **Security First**: Container scanning, dependency audits, and best practices

## 🏗️ Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Backstage     │    │   Kubernetes    │    │   ArgoCD        │
│   Web Interface │───►│   (k3s +        │───►│   (GitOps)      │
│   (Browser)     │    │    Cilium)      │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

**Simple and Clean**: Backstage web interface runs on Kubernetes, managed by ArgoCD for GitOps deployment.

### 🧱 Technical Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Platform** | [Backstage](https://backstage.io/) | Core IDP framework |
| **Runtime** | [k3s](https://k3s.io/) | Lightweight Kubernetes |
| **Networking** | [Cilium](https://cilium.io/) | eBPF-based CNI |
| **GitOps** | [ArgoCD](https://argoproj.github.io/argo-cd/) | Deployment automation |
| **Container Registry** | [Docker Hub](https://hub.docker.com/) | Image distribution |
| **CI/CD** | [GitHub Actions](https://github.com/features/actions) | Automated builds |

## 🚀 Quick Start

### Prerequisites

- **Local Development**:
  - Node.js 18+ and npm
  - Docker Desktop
  - Git

- **Production Deployment**:
  - k3s cluster with Cilium CNI
  - ArgoCD installed and configured
  - Docker Hub account with repository access

### 🏠 Local Development

```bash
# 1. Clone the repository
git clone https://github.com/fede-r1c0/backstage.git
cd backstage

# 2. Install dependencies
npm install

# 3. Setup environment configuration
cp app-config.local.yaml.example app-config.local.yaml
# Edit app-config.local.yaml with your local settings

# 4. Start development server
npm run dev

# 5. Open in browser
open http://localhost:3000
```

### 🐳 Docker Build

```bash
# Build the image locally
docker build -t backstage-idp .

# Run the container
docker run -p 3000:3000 \
  -e NODE_ENV=production \
  -e LOG_LEVEL=info \
  backstage-idp

# Test the container
curl http://localhost:3000/health
```

### ☸️ Kubernetes Deployment

```bash
# 1. Ensure ArgoCD is running in your cluster
kubectl get pods -n argocd

# 2. Apply the ArgoCD application
kubectl apply -f argocd/backstage-idp.yaml

# 3. Check deployment status
kubectl get applications -n argocd
kubectl describe application backstage-idp -n argocd

# 4. Access the platform
kubectl port-forward svc/backstage-idp -n backstage 3000:3000
```

## 🔧 Configuration

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `NODE_ENV` | `development` | Node.js environment |
| `LOG_LEVEL` | `info` | Logging level |
| `PORT` | `3000` | HTTP server port |
| `DATABASE_URL` | - | PostgreSQL connection string |
| `GITHUB_TOKEN` | - | GitHub API token for integrations |

### Configuration Files

- **`app-config.yaml`**: Base configuration
- **`app-config.local.yaml`**: Local development overrides
- **`app-config.production.yaml`**: Production environment settings

## 🚀 CI/CD Pipeline

Our CI/CD pipeline automatically:

1. **Security Scanning**: Trivy vulnerability scanning + Snyk security analysis
2. **Quality Gates**: Unit tests, integration tests, linting, type checking
3. **Docker Build**: Multi-architecture builds (ARM64 + x86_64)
4. **Image Push**: Automatic push to Docker Hub with semantic tagging
5. **Deployment**: ArgoCD sync for GitOps deployment

### Pipeline Triggers

- **Push to `main`**: Production deployment
- **Push to `develop`**: Staging deployment
- **Pull Request**: Quality checks and security scanning

## 🔌 Plugin Ecosystem

### Core Plugins

| Plugin | Purpose | Status |
|--------|---------|--------|
| **@backstage/plugin-catalog-backend** | Service catalog management | ✅ Included |
| **@backstage/plugin-scaffolder-backend** | Template-based scaffolding | ✅ Included |
| **@backstage/plugin-techdocs-backend** | Technical documentation | ✅ Included |
| **@backstage/plugin-explore** | Service discovery | ✅ Included |

### Custom Plugins

| Plugin | Purpose | Status |
|--------|---------|--------|
| **@internal/infrastructure-plugin** | Infrastructure self-service | 🚧 In Development |
| **@internal/monitoring-plugin** | System monitoring dashboard | 🚧 In Development |
| **@internal/security-plugin** | Security compliance tools | 🚧 In Development |

## 🧪 Testing

```bash
# Run all tests
npm test

# Run specific test suites
npm run test:unit          # Unit tests
npm run test:integration   # Integration tests
npm run test:coverage      # Coverage report

# Linting and type checking
npm run lint               # ESLint
npm run lint:fix          # Auto-fix linting issues
npm run type-check        # TypeScript compilation check
```

## 📊 Monitoring & Health

### Health Endpoints

- **`/health`**: Basic health check
- **`/metrics`**: Prometheus metrics
- **`/ready`**: Readiness probe for Kubernetes

### Key Metrics

- HTTP request duration
- Memory usage
- Plugin performance
- Database connection status

## 🔒 Security

### Container Security

- **Base Image**: Alpine Linux (minimal attack surface)
- **User**: Non-root user (`backstage:1001`)
- **Vulnerability Scanning**: Trivy + Snyk integration
- **Dependency Audits**: Automated npm audit in CI/CD

### Best Practices

- Regular security updates
- Principle of least privilege
- Secrets management via Kubernetes
- Network policies with Cilium

## 🚨 Troubleshooting

### Common Issues

<details>
<summary><strong>Docker Build Fails</strong></summary>

```bash
# Clear Docker cache
docker system prune -a

# Rebuild without cache
docker build --no-cache .

# Check available disk space
df -h
```
</details>

<details>
<summary><strong>Backstage Won't Start</strong></summary>

```bash
# Clean install
rm -rf node_modules package-lock.json
npm install

# Check configuration
npm run type-check
npm run lint

# Verify environment variables
env | grep NODE
```
</details>

<details>
<summary><strong>ArgoCD Sync Issues</strong></summary>

```bash
# Check application status
kubectl get applications -n argocd
kubectl describe application backstage-idp -n argocd

# Check pod logs
kubectl logs -n backstage deployment/backstage-idp

# Verify image exists
docker pull fede-r1c0/backstage-idp:latest
```
</details>

### Getting Help

1. **Check the logs**: `kubectl logs -n backstage deployment/backstage-idp`
2. **Review ArgoCD status**: Check the ArgoCD UI for sync issues
3. **Verify configuration**: Ensure all required environment variables are set
4. **Check network policies**: Verify Cilium policies allow necessary traffic

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Workflow

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### Code Standards

- **TypeScript**: Strict mode enabled
- **Testing**: Minimum 80% coverage
- **Linting**: ESLint + Prettier
- **Commits**: Conventional commit format

## 📚 Documentation

- **[Deployment Guide](docs/DEPLOYMENT.md)**: Detailed deployment instructions
- **[Plugin Development](docs/PLUGINS.md)**: How to create custom plugins
- **[API Reference](docs/API.md)**: Backend API documentation
- **[Troubleshooting](docs/TROUBLESHOOTING.md)**: Common issues and solutions

## 🏗️ Roadmap

### Q1 2024
- [x] Project setup and basic Backstage configuration
- [x] Docker image with security best practices
- [x] CI/CD pipeline with security scanning
- [ ] Basic plugin ecosystem

### Q2 2024
- [ ] Infrastructure self-service plugin
- [ ] Monitoring and observability integration
- [ ] Multi-environment deployment support
- [ ] Performance optimization

### Q3 2024
- [ ] Advanced security features
- [ ] Multi-tenant support
- [ ] Advanced analytics and reporting
- [ ] Production hardening

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **[Backstage](https://backstage.io/)**: The amazing platform that makes this possible
- **[CNCF](https://cncf.io/)**: For incubating Backstage
- **[k3s](https://k3s.io/)**: Lightweight Kubernetes for edge computing
- **[Cilium](https://cilium.io/)**: eBPF-based networking and security

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/fede-r1c0/backstage/issues)
- **Discussions**: [GitHub Discussions](https://github.com/fede-r1c0/backstage/discussions)
- **Wiki**: [Project Wiki](https://github.com/fede-r1c0/backstage/wiki)

---

**Built with ❤️ for the DevOps community**

*This project serves as both a learning environment and a foundation for real-world Internal Developer Platforms. Every decision prioritizes simplicity, maintainability, and production-grade standards.*