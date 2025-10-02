## [1.0.1](https://github.com/fede-r1c0/backstage/compare/v1.0.0...v1.0.1) (2025-10-02)

### ⚠ BREAKING CHANGES

* **ci:** none

### ♻️ Refactors

* **ci:** simplify Docker image tagging strategy ([da69f3f](https://github.com/fede-r1c0/backstage/commit/da69f3ff1f38379af818803694ea74f6ca1d76bc))

## 1.0.0 (2025-10-01)

### ⚠ BREAKING CHANGES

* **ci:** none
* **ci:** none
* **ci:** none
* **ci:** none
* **ci:** none
* **ci:** none
* **ci:** none
* **ci:** none
* **ci:** none
* **ci:** none
* **ci:** none

### ✨ Features

* add backstage dockerfile ([1ccf900](https://github.com/fede-r1c0/backstage/commit/1ccf9006ed09cb5adc89d3a44ae07bc98646d9fc))
* add github actions plugin ([5f901c9](https://github.com/fede-r1c0/backstage/commit/5f901c95363b238f4768bf3413bf419068b6b267))
* add yarn.lock and optimize CI/CD pipeline ([680b0df](https://github.com/fede-r1c0/backstage/commit/680b0df497fb5e6acfdb5a8b1886881de2a09401))
* backstage build app ([b5b7d7a](https://github.com/fede-r1c0/backstage/commit/b5b7d7aa5ffc7b71143c425adf2be546e27c9da2))
* **ci:** add CI-optimized test script ([6cc6aa5](https://github.com/fede-r1c0/backstage/commit/6cc6aa5efb62eed084254482006dd03fb3fcfb89))
* **ci:** add composite action for Node.js setup with caching ([1599dc9](https://github.com/fede-r1c0/backstage/commit/1599dc9f522eb7a6b2a42e97601bf912c70879f4))
* **ci:** add semantic release workflow ([3f95df0](https://github.com/fede-r1c0/backstage/commit/3f95df0782b42da8ed62dc8a770eb925abd6e872))
* **ci:** automate semantic-release on push to main and develop ([88d8c4f](https://github.com/fede-r1c0/backstage/commit/88d8c4fb3853d446f5ef877420b78e82bebaf42c))
* **ci:** consolidate build job using docker metadata-action ([08efc3d](https://github.com/fede-r1c0/backstage/commit/08efc3dbf2c7b1eb531b31e282807fedaf88c41a))
* **ci:** implement artifact sharing in validation jobs ([875e7ef](https://github.com/fede-r1c0/backstage/commit/875e7ef9810025287a3ffd8d5b2dcfbbdc810b3a))
* **ci:** integrate improved jobs in main pipeline ([e8140f4](https://github.com/fede-r1c0/backstage/commit/e8140f48997bd491a79d88a8d3b087f10be6e1a1))
* dependabot configs ([e6fd5ef](https://github.com/fede-r1c0/backstage/commit/e6fd5ef7c2b5456d2b70827ffe2bd13ef9e7f1af))
* optimized CI/CD pipeline with coherent workflows ([7c710c6](https://github.com/fede-r1c0/backstage/commit/7c710c6a57bf305b99b7077e2db6f36c9f033d85))
* semantic release integration ([d7d9eab](https://github.com/fede-r1c0/backstage/commit/d7d9eab0a113c1177136f84a7214f0c318681884))

### 🐛 Bug Fixes

* add checkout to security-scan job for SARIF upload ([d65d465](https://github.com/fede-r1c0/backstage/commit/d65d465f872837a1409f5d3f787b2311a89b407a))
* build tags ([e9ff6a4](https://github.com/fede-r1c0/backstage/commit/e9ff6a4d1494cae49091602cea4eaff6cafeb9c1))
* buildkit multi tags cache stuck ([7a023b0](https://github.com/fede-r1c0/backstage/commit/7a023b0b5ea2a0729d35c3d0f3a44ac84a981a94))
* ci build tags ([0086884](https://github.com/fede-r1c0/backstage/commit/00868840572cf9b8ba345ce79e22452c07c78231))
* **ci:** scan correct Docker image using digest in security job ([7cbd21e](https://github.com/fede-r1c0/backstage/commit/7cbd21edadca72bbfdd32f878852cca4d055b2cc))
* **ci:** use composite action instead of artifact sharing for validation jobs ([4b5f89f](https://github.com/fede-r1c0/backstage/commit/4b5f89f0ee4dd2c52f9069856efac892a65c2956))
* **ci:** use yarn tsc instead of npx in validation workflow ([38fb0b2](https://github.com/fede-r1c0/backstage/commit/38fb0b2ff89409754f1c62b77e688e49d9f54f42))
* dependencies check yarn.lock ([e074ff3](https://github.com/fede-r1c0/backstage/commit/e074ff371c70170a48631ef16fa15d7a09501d98))
* production backend listen port ([537d73f](https://github.com/fede-r1c0/backstage/commit/537d73f7a2b4fb1e1f3d2f20965415a944c43ea8))
* resolve security audit and SARIF upload issues ([ee9a5fc](https://github.com/fede-r1c0/backstage/commit/ee9a5fceae900b7a53d24a6f65009ea5e1bd5541))
* triggers and caching ([fe0392d](https://github.com/fede-r1c0/backstage/commit/fe0392db8ab3f848436c7eee4e3b4b096904ce8f))
* yarn cache ([49af643](https://github.com/fede-r1c0/backstage/commit/49af64304d53b1e0392b8aa54e4e1b86b2632a72))

### ♻️ Refactors

* **ci:** integrate semantic-release into centralized pipeline ([be397ae](https://github.com/fede-r1c0/backstage/commit/be397ae461f806299fe74928c1045d2f224bb109))
* remove performance test job from CI/CD pipeline ([6852775](https://github.com/fede-r1c0/backstage/commit/6852775cab983a617af26342b28885a52a2dea2e))

### 📚 Documentation

* add readme ([f1c95e5](https://github.com/fede-r1c0/backstage/commit/f1c95e5c3bd6b7f6cd73e79b62a82e731ccb3a55))
* add semantic-release doc ([95b86fb](https://github.com/fede-r1c0/backstage/commit/95b86fb6dc03e420ac30be487ee2cda67357f3b9))
* **ci:** update CI/CD documentation with v2.0 improvements ([5577ab1](https://github.com/fede-r1c0/backstage/commit/5577ab146f32c65079a8bd0421f2d9cb338977cc))
* consolidate ci/cd documentation ([a5e6e28](https://github.com/fede-r1c0/backstage/commit/a5e6e28db9dda9fcaddb0aef216c6bc4eaa66022))
* update - translate readme files ([ddd319f](https://github.com/fede-r1c0/backstage/commit/ddd319f1528803a0bc5da6ce560e0640693847a6))
* update ci cd documentation ([31bae11](https://github.com/fede-r1c0/backstage/commit/31bae110b9639109f33b934a655d7cd13e6c95b6))
* update readme info ([74dc4a7](https://github.com/fede-r1c0/backstage/commit/74dc4a713e0894895b0f2b659e8152647f0bc464))

# Changelog

All notable changes to this project will be documented in this file.

This project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

This changelog is automatically generated by [semantic-release](https://github.com/semantic-release/semantic-release).
