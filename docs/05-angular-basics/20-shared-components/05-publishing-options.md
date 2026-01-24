# 🚀 Options for Publishing Angular Libraries

### 1. **Publish to npm (Public or Private Registry)**

### 2. **Private npm Registry (Verdaccio, GitHub Packages, Azure Artifacts)**
- Instead of publishing to the public npm registry, you can host your own.
- Example: GitHub Packages
  - Add `.npmrc` with:
    ```
    @neutral-00:registry=https://npm.pkg.github.com
    ```
  - Publish with:
    ```bash
    npm publish
    ```
- Other projects can install with:
  ```bash
  npm install @neutral-00/lousing-components
  ```
 Check the below config
 ```
 "publishConfig":{"registry":"http://my-internal-registry.local"}
 ```
👉 Best for: Enterprise setups where you want control over distribution.

---

### 3. **Direct GitHub Install**
- You can skip npm and install directly from GitHub:
  ```bash
  npm install neutral-00/lousing-workspace#main
  ```
- This pulls the repo and uses the library code.
- Not as clean as npm (no versioning, heavier installs).

👉 Best for: Quick sharing between trusted projects.

---

### 4. **Tarball Distribution**
- Build the library:
  ```bash
  nx build lousing-components
  ```
- Create a tarball:
  ```bash
  npm pack
  ```
- Share the `.tgz` file with teammates.
- Install in another project:
  ```bash
  npm install ./lousing-components-1.0.0.tgz
  ```

👉 Best for: Offline sharing or one-off installs.
---

