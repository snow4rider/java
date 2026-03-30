# ☕ Java Dev Container

A ready-to-use development container for Java projects, powered by [Dev Containers](https://containers.dev/).

---

## 📦 What's Included

| Tool | Version | Purpose |
|------|---------|---------|
| Java (JDK) | 25 (LTS) | Core runtime & compiler |
| Maven | Latest | Build & dependency management |
| Gradle | Latest | Alternative build tool |
| Git | Latest | Version control |
| VS Code Extensions | See below | IDE tooling |

### VS Code Extensions (auto-installed)

- **Extension Pack for Java** (`vscjava.vscode-java-pack`) — IntelliSense, debugging, testing
- **Spring Boot Extension Pack** (`vmware.vscode-boot-dev-pack`) — Spring Boot support
- **Gradle for Java** (`vscjava.vscode-gradle`) — Gradle task runner
- **GitLens** (`eamodio.gitlens`) — Enhanced Git integration
- **SonarLint** (`SonarSource.sonarlint-vscode`) — Real-time code quality

---

## 🚀 Getting Started

### Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (running)
- [VS Code](https://code.visualstudio.com/) with the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Open in Dev Container

1. Clone this repository:
   ```bash
   git clone <your-repo-url>
   cd <your-repo>
   ```

2. Open in VS Code:
   ```bash
   code .
   ```

3. When prompted, click **"Reopen in Container"** — or open the Command Palette (`Cmd/Ctrl+Shift+P`) and run:
   ```
   Dev Containers: Reopen in Container
   ```

4. Wait for the container to build (first time only, ~2–5 minutes).

You're in! The terminal inside VS Code is now running inside the container.

---

## 📁 Project Structure

```
.
├── .devcontainer/
│   ├── devcontainer.json   # Container configuration
│   └── Dockerfile          # (optional) Custom image definition
├── src/
│   ├── main/java/          # Application source code
│   └── test/java/          # Test source code
├── pom.xml                 # Maven build file (or build.gradle)
└── README.md
```

---

## 🛠️ Common Tasks

### Compile

```bash
# Maven
mvn compile

# Gradle
./gradlew compileJava
```

### Run Tests

```bash
# Maven
mvn test

# Gradle
./gradlew test
```

### Build & Package

```bash
# Maven — produces target/*.jar
mvn package

# Gradle — produces build/libs/*.jar
./gradlew build
```

### Run the Application

```bash
# Maven (Spring Boot)
mvn spring-boot:run

# Gradle (Spring Boot)
./gradlew bootRun

# Plain Java jar
java -jar target/your-app.jar
```

---

## ⚙️ Configuration

### `devcontainer.json` Overview

```jsonc
{
  "name": "Java",
  "image": "mcr.microsoft.com/devcontainers/java:21",
  "features": {
    "ghcr.io/devcontainers/features/java:1": {
      "version": "21",
      "installMaven": true,
      "installGradle": true
    }
  },
  "customizations": {
    "vscode": {
      "extensions": [
        "vscjava.vscode-java-pack",
        "vmware.vscode-boot-dev-pack"
      ],
      "settings": {
        "java.configuration.updateBuildConfiguration": "automatic",
        "editor.formatOnSave": true
      }
    }
  },
  "forwardPorts": [8080],
  "postCreateCommand": "mvn --version && java --version"
}
```

### Changing the Java Version

Edit `devcontainer.json` and update the `version` field under `features`:

```jsonc
"ghcr.io/devcontainers/features/java:1": {
  "version": "17"   // or 11, 21, etc.
}
```

Then rebuild the container: **Command Palette → Dev Containers: Rebuild Container**.

---

## 🔌 Port Forwarding

By default, port **8080** is forwarded to your local machine. To change or add ports, edit the `forwardPorts` array in `devcontainer.json`:

```jsonc
"forwardPorts": [8080, 8443, 5005]  // 5005 = remote debug port
```

---

## 🐛 Debugging

The container supports remote debugging on port **5005**.

Start your app with the debug agent:
```bash
java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005 -jar target/your-app.jar
```

Then attach VS Code's debugger using the **"Attach to Remote JVM"** launch configuration.

---

## 🧹 Tips & Troubleshooting

| Issue | Fix |
|-------|-----|
| Container fails to build | Ensure Docker Desktop is running and has sufficient memory (≥4 GB recommended) |
| Extensions not loading | Run **Dev Containers: Rebuild Container** from the Command Palette |
| Maven/Gradle not found | Check the `features` block in `devcontainer.json` includes the install flags |
| Port already in use | Change `forwardPorts` or stop the local process using that port |
| Slow first startup | Normal — subsequent starts use cached layers and are much faster |

---

## 📚 Resources

- [Dev Containers specification](https://containers.dev/)
- [Available Dev Container Features](https://containers.dev/features)
- [VS Code Java in Containers guide](https://code.visualstudio.com/docs/devcontainers/containers)
- [Microsoft Java Dev Container images](https://mcr.microsoft.com/en-us/artifact/mar/devcontainers/java)

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
