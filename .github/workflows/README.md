# 🚀 GitHub Actions Workflows

## 📋 Workflows Disponibles

### 1. `build-docker.yml` ⚡

#### Build de imagen Docker - Rápido y optimizado

- **Trigger**: Push a main, PRs, manual
- **Tiempo**: 3-5 minutos
- **Características**:
  - ✅ Multi-arch (AMD64 + ARM64)
  - ✅ Cache optimizado con GitHub Actions
  - ✅ Push automático a ghcr.io
  - ✅ Mínima complejidad

### 2. `ci-cd-complete.yml` 🏗️

#### Pipeline completo con todas las validaciones

- **Trigger**: Push a main/develop, releases, manual
- **Tiempo**: 8-12 minutos
- **Características**:
  - ✅ Linting y type checking
  - ✅ Security scanning (Trivy)
  - ✅ Multi-environment support
  - ✅ Deploy notifications

## 🎯 Cuándo usar cada uno

| Situación | Workflow Recomendado |
|-----------|---------------------|
| Feature branch | `build-docker.yml` |
| Hotfix rápido | `build-docker.yml` |
| Pre-release | `ci-cd-complete.yml` |
| Validación completa | `ci-cd-complete.yml` |
| Deploy a producción | `ci-cd-complete.yml` |

## 🐳 Acceso a las imágenes

```bash
# Pull última versión
docker pull ghcr.io/[tu-org]/backstage:latest

# Pull específico para ARM64 (M1/M2 Mac, Raspberry Pi)
docker pull ghcr.io/[tu-org]/backstage:latest --platform linux/arm64

# Pull por SHA
docker pull ghcr.io/[tu-org]/backstage:main-abc1234
```

## 🔧 Configuración inicial

### 1. Permisos de GitHub Actions

```text
Settings → Actions → General → Workflow permissions
✅ Read and write permissions
```

### 2. GitHub Container Registry

- Automático con `GITHUB_TOKEN`
- No requiere configuración adicional

## 💡 Tips

- **Cache**: Se limpia automáticamente después de 7 días
- **Multi-arch**: Builds paralelos para mejor performance
- **Free tier**: Optimizado para < 2000 minutos/mes
- **Security**: Scanning automático en builds de main

## 📊 Métricas esperadas

| Métrica | Build Simple | CI/CD Completo |
|---------|-------------|----------------|
| Tiempo inicial | 5-7 min | 10-12 min |
| Con cache | 3-4 min | 8-10 min |
| Costo/build | ~$0.03 | ~$0.10 |
