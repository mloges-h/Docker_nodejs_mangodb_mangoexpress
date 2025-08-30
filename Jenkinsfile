node {
    stage('Checkout') {
        echo "Cloning GitHub repository..."
        git branch: 'main', url: 'https://github.com/mloges-h/Docker_nodejs_mangodb_mangoexpress.git'
    }

    stage('Build Docker Images') {
        echo "Building Docker images with Docker Compose..."
        sh '''
        docker compose build || docker-compose build
        '''
    }

    stage('Deploy Containers') {
        echo "Starting services with Docker Compose..."
        sh '''
        docker-compose -f docker-compose.yaml build && docker-compose -f docker-compose.yaml up -d
        '''
    }

    stage('Health Check') {
        echo "Checking if Node.js app is running..."
        sh '''
        sleep 15
        curl -f http://localhost:3000 || (echo "App is not responding on port 3000" && exit 1)
        '''
    }
}
