# demo-nexus-shared-lib

This is a demonstration repository that serves as an example for using the **Nexus Shared Library** in Jenkins. The project contains the basic Gradle configuration and a `Jenkinsfile` to validate integration with the shared library.

## 🚀 Project Structure

* **`Jenkinsfile`**: The main declarative pipeline that calls `nexusPipeline` from the shared library.
* **`build.gradle` & `settings.gradle`**: The minimum configuration required for Gradle to recognize the workspace as a valid project.

## 🛠 Prerequisites

To run this pipeline, ensure that in your Jenkins instance you have:

1. **Shared Library**: Configured `nexus-shared-lib` under *Manage Jenkins -> Configure System -> Global Pipeline Libraries*.
2. **Global Tool Configuration**: Configured a **Gradle** tool named `Default` (to match the fallback logic in the pipeline).
3. **Plugins**:
   * *Pipeline: Declarative*
   * *Git Plugin*
   * *Gradle Plugin*
   * *HTTP Request Plugin* (for Teams/Slack notifications)

## 📖 Usage

This pipeline is designed to be modular. You can enable or disable stages (Docker, S3, K8s, Security) directly from the `Jenkinsfile` by setting parameters:

```groovy
nexusPipeline(
    projectName: 'nexus-demo',
    environment: 'demo',
    runSecurityScan: false,
    buildAndPushDocker: false,
    deployToK8s: false
)
```
