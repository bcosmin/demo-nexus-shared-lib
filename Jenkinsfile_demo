// Demo pipeline showcasing a production-grade configuration of the nexusPipeline from the 'nexus-shared-lib' Jenkins shared library.

@Library('nexus-shared-lib@main') _ 

// This Jenkinsfile demonstrates the full capabilities of the nexusPipeline
// provided by the 'nexus-shared-lib', incorporating security guards, containerization,
// Artifactory integration, Kubernetes deployment, multi-channel notifications,
// and custom extension hooks for lifecycle management.

nexusPipeline(
    // --- Project Metadata ---
    projectName: 'nexus-demo', // Custom project name for display and logging
    environment: 'demo',                 // Target deployment environment

    // --- Feature Toggles ---
    runSecurityScan: false,
    runAdvancedSecurityGuard: false,
    buildAndPushDocker: false,
    uploadToArtifactory: false,
    deployToK8s: false,

    // --- Docker Configuration ---
    dockerRegistry: 'registry.company.io',
    dockerImageName: 'nexus/enterprise-microservice',
    dockerCredentialsId: 'docker-registry-credentials',

    // --- JFrog Artifactory Configuration ---
    artifactoryServerId: 'my-jfrog-server',        // JFrog server ID
    artifactoryTargetRepo: 'libs-release-local',   // Target repository
    artifactoryCredentialsId: 'my-jfrog-creds',    // Jenkins credential ID

    // --- Kubernetes / Helm Deployment ---
    helmReleaseName: 'enterprise-microservice',
    helmChartPath: './charts/enterprise-microservice',
    helmNamespace: 'production',

    // --- Multi-Channel Notifications ---
    sendEmailNotifications: false,
    notificationEmail: '',

    sendSlackNotification: false,
    slackChannel: '',

    sendTeamsNotification: false,
    teamsWebhookUrl: '',

    // --- Security Whitelist Configuration ---
    // List of CVE IDs or secret hashes to be ignored by the SecurityGuard
    securityWhitelist: [
        'CVE-2023-12345',
        'sh-abcdef1234567890'
    ],

    // --- Extension Points (Closures for custom lifecycle hooks) ---
    beforeBuild: {
        echo "--> Custom step [beforeBuild]: Setting up private NPM registries and downloading secure dependencies..."
        // sh 'npm ci'
    },

    afterBuild: {
        echo "--> Custom step [afterBuild]: Archiving test results and running custom static analysis..."
        // junit 'build/test-results/**/*.xml'
    },

    beforeDeploy: {
        echo "--> Custom step [beforeDeploy]: Validating Kubernetes cluster health and database migration status..."
        // sh 'kubectl cluster-info'
    },

    afterDeploy: {
        echo "--> Custom step [afterDeploy]: Running end-to-end smoke tests and triggering cache invalidation..."
        // sh 'curl -f https://api.company.io/healthz || error "Health check failed post-deployment!"'
    }
)
