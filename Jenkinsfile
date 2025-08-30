node {
    stage('Checkout') {
        // Pull code from your GitHub repo
        git branch: 'main', url: 'https://github.com/mloges-h/Docker_nodejs_mangodb_mangoexpress.git'
    }

    stage('Build Docker Images') {
        echo "Building Docker images for Node.js app, MongoDB, and Mongo Express..."
        sh """
        docker compose build
        """
    }

    stage('Run Containers') {
        echo "Starting services using Docker Compose..."
        sh """
        docker compose up -d
        """
    }

    stage('Test Application') {
        echo "Running basic health checks..."
        // Example: check if Node.js app is running
        sh """
        sleep 10
        curl -f http://localhost:3000 || exit 1
        """
    }

    stage('Cleanup') {
        echo "Stopping and cleaning up Docker containers..."
        sh """
        docker compose down
        """
    }
}
