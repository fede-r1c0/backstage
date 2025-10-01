# 🚀 GitHub Actions Workflows

## 📋 Workflows Disponibles

### 1. `pipeline.yml` 🔄

#### Pipeline CI/CD centralizado

- **Trigger**: Push a main/develop, PRs, tags versionados
- **Tiempo**: 6-8 minutos
- **Características**:
  - ✅ Validación de código (lint, type check, security)
  - ✅ Build multi-arch (AMD64 + ARM64)
  - ✅ Security scan con Trivy
  - ✅ Soporte para tags versionados de Semantic Release

### 2. `release.yml` 📦

#### Semantic Release - Versionado automático

- **Trigger**: Manual (workflow_dispatch)
- **Tiempo**: 1-2 minutos
- **Características**:
  - ✅ Versionado automático con Conventional Commits
  - ✅ Generación de CHANGELOG.md
  - ✅ Creación de GitHub Releases
  - ✅ Trigger automático del pipeline para build versionado
  - ✅ Dry run mode para preview

### 3. Reusable Jobs

#### `validate-job.yml`, `build-job.yml`, `security-job.yml`

- **Tipo**: Reusable workflows
- **Uso**: Llamados por `pipeline.yml`
- **Beneficio**: DRY - No repetir código

## 🎯 Cuándo usar cada uno

| Situación | Workflow | Trigger |
|-----------|----------|---------|
| **Feature/PR** | `pipeline.yml` | Automático en push/PR |
| **Validación completa** | `pipeline.yml` | Automático en push a main/develop |
| **Crear Release** | `release.yml` | Manual desde Actions UI |
| **Release automática** | `pipeline.yml` | Automático al crear tag (desde release.yml) |

## 🐳 Acceso a las imágenes

```bash
# Pull última versión (main branch o último release)
docker pull ghcr.io/[tu-org]/backstage:latest

# Pull versión específica (desde Semantic Release)
docker pull ghcr.io/[tu-org]/backstage:v1.2.3

# Pull por SHA
docker pull ghcr.io/[tu-org]/backstage:abc1234

# Pull específico para ARM64 (M1/M2 Mac, Raspberry Pi)
docker pull ghcr.io/[tu-org]/backstage:latest --platform linux/arm64
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
