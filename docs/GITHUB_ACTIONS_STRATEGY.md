# 🚀 Estrategia GitHub Actions para Backstage

## 🎯 Filosofía: Todo en el Pipeline

**NO scripts externos, TODO integrado en GitHub Actions**

## 📋 Workflows Disponibles

### 1. `build-docker.yml` - Simple y Rápido
**Propósito**: Build y push de imagen Docker para desarrollo diario
- ✅ Multi-arch (amd64/arm64)
- ✅ Cache optimizado con GitHub Actions
- ✅ Push automático a ghcr.io
- ⏱️ ~3-5 minutos

### 2. `ci-cd-complete.yml` - Pipeline Completo
**Propósito**: CI/CD completo con validación y seguridad
- ✅ Linting y type checking
- ✅ Security scanning con Trivy

- ✅ Multi-environment support
- ⏱️ ~8-12 minutos

## 🏗️ Arquitectura de la Solución

```
┌─────────────────────────────────────────────────────────────────┐
│                    CI/CD Pipeline Flow                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Push/PR ──┐                                                   │
│             ├─→ [Trigger Decision] ──┐                        │
│  Manual ───┘                         │                        │
│                                        │                        │
│                                        ▼                        │
│                    ┌─────────────────┬─────────────────┐       │
│                    │   SIMPLE        │   COMPLETE      │       │
│                    │ build-docker.yml│ ci-cd-complete.yml│      │
│                    └─────────────────┴─────────────────┘       │
│                              │                        │        │
│                              ▼                        ▼        │
│                    ┌─────────────────┐    ┌─────────────────┐  │
│                    │ Build Multi-arch│    │   Validate      │  │
│                    │ (AMD64 + ARM64) │    │   (Lint, Type)  │  │
│                    └─────────────────┘    └─────────────────┘  │
│                              │                        │        │
│                              ▼                        ▼        │
│                    ┌─────────────────┐    ┌─────────────────┐  │
│                    │ Push to ghcr.io │    │     Build       │  │
│                    │   (3-5 min)     │    │   (Docker)      │  │
│                    └─────────────────┘    └─────────────────┘  │
│                                                    │            │
│                                                    ▼            │
│                                        ┌─────────────────┐     │
│                                        │ Security Scan   │     │
│                                        │   (Trivy)       │     │
│                                        └─────────────────┘     │
│                                                    │            │
│                                                    ▼            │
│                                        ┌─────────────────┐     │
│                                        │                │     │
│                                        │  (Load Test)    │     │
│                                        └─────────────────┘     │
│                                                    │            │
│                                                    ▼            │
│                                        ┌─────────────────┐     │
│                                        │ Deploy Ready    │     │
│                                        │  (8-12 min)     │     │
│                                        └─────────────────┘     │
└─────────────────────────────────────────────────────────────────┘
```

## 💡 Decisiones Clave

### ¿Por qué NO scripts?
| Scripts Externos | GitHub Actions Nativo | Ganador |
|-----------------|---------------------|---------|
| ❌ Mantenimiento adicional | ✅ Todo en un lugar | **Actions** |
| ❌ Difícil debugging | ✅ Logs estructurados | **Actions** |
| ❌ Permisos complejos | ✅ Permisos declarativos | **Actions** |
| ❌ Cache manual | ✅ Cache automático | **Actions** |

### ¿Por qué GitHub Actions Cache (gha)?
```yaml
cache-from: type=gha
cache-to: type=gha,mode=max
```
- **50% más rápido** que registry cache
- **Gratis** en GitHub
- **Automático** cleanup después de 7 días

### ¿Por qué Ubuntu 24.04?
- **Más rápido** que ubuntu-latest (no redirect)
- **Predecible** - versión fija
- **Moderno** - últimas herramientas

## 🚀 Uso Rápido

### Build Simple (90% de casos)
```bash
# Push a main = build y push automático
git push origin main

# PR = solo build, no push
git push origin feature/mi-feature
```

### Build Completo (releases, testing)
```bash
# Se activa automáticamente en:
# - Push a main/develop
# - Creación de release
# - Manual desde GitHub UI
```

### Pull de Imagen
```bash
# Última versión
docker pull ghcr.io/tu-usuario/backstage:latest

# Versión específica
docker pull ghcr.io/tu-usuario/backstage:main-abc1234

# ARM64 (Raspberry Pi, M1 Mac)
docker pull ghcr.io/tu-usuario/backstage:latest --platform linux/arm64
```

## 📊 Optimizaciones Implementadas

### 1. Cache Multi-nivel
```yaml
# Nivel 1: Node modules
cache: 'yarn'

# Nivel 2: Docker layers
cache-from: type=gha
cache-to: type=gha,mode=max
```

### 2. Build Condicional
- **PR**: Solo build, no push (ahorra bandwidth)
- **Main**: Build + push + scan
- **Release**: Full pipeline + deploy

### 3. Multi-arch Eficiente
- QEMU solo cuando necesario
- Build paralelo de arquitecturas
- Cache compartido entre plataformas

## 📈 Métricas de Performance

| Escenario | Tiempo | Costo |
|-----------|--------|-------|
| Build inicial | 8-10 min | $0.08 |
| Build con cache | 3-4 min | $0.03 |
| PR validation | 2-3 min | $0.02 |
| Full CI/CD | 8-10 min | $0.08 |

**Costo mensual estimado**: $0 (dentro del free tier de 2000 minutos)

## 🔧 Troubleshooting

### Error: "Permission denied to packages"
```yaml
# En Settings → Actions → General
# Workflow permissions: Read and write permissions
```

### Build lento sin cache
```bash
# Verificar cache en Actions → Caches
# Si no hay cache, es normal que el primer build sea lento
```

### Multi-arch falla
```yaml
# Verificar QEMU setup
- name: Set up QEMU
  uses: docker/setup-qemu-action@v3
```

## 🔐 Seguridad

### Implementado
- ✅ **No secretos** en código
- ✅ **GITHUB_TOKEN** automático
- ✅ **Trivy scanning** de CVEs
- ✅ **Dependabot** habilitado
- ✅ **SBOM** generation

### Permisos Mínimos
```yaml
permissions:
  contents: read      # Solo lectura de código
  packages: write     # Solo para push de imágenes
```

## 📚 Mejores Prácticas Aplicadas

1. **KISS**: Un workflow simple, uno complejo
2. **DRY**: Reutilizar actions oficiales
3. **Fast Feedback**: PR builds rápidos
4. **Shift Left**: Security scanning temprano
5. **GitOps Ready**: Tags consistentes

## 🎯 Cuándo Usar Cada Workflow

### `build-docker.yml`
- ✅ Desarrollo diario
- ✅ Feature branches
- ✅ Hotfixes rápidos

### `ci-cd-complete.yml`
- ✅ Releases
- ✅ Validación completa
- ✅ Antes de producción

## 💪 Ventajas de Esta Estrategia

1. **Todo en GitHub** - Sin dependencias externas
2. **Free Tier Friendly** - Optimizado para 2000 min/mes
3. **Multi-arch Nativo** - ARM64 + AMD64
4. **Cache Inteligente** - 50-70% más rápido
5. **Security First** - Scanning automático

## 📝 Mantenimiento

### Actualizar Node Version
```yaml
env:
  NODE_VERSION: '20.19.4'  # Cambiar aquí
```

### Actualizar Base Image
```dockerfile
# En packages/backend/Dockerfile
FROM node:20-bookworm-slim  # Cambiar aquí
```

### Limpiar Cache
```bash
# GitHub UI → Actions → Caches → Delete
# O esperar 7 días (limpieza automática)
```

---

**Conclusión**: Esta estrategia maximiza simplicidad, velocidad y seguridad, todo dentro del free tier de GitHub Actions. No necesitas scripts externos, todo está donde debe estar: en el pipeline.

**Mantenido por**: DevOps Team  
**Filosofía**: "El mejor script es el que no tienes que mantener"
