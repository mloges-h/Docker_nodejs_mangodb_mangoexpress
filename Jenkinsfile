node {
    stage('Install Docker & Compose') {
        echo "Checking and installing Docker & Docker Compose if not present..."
        sh '''
        # Install Docker if not installed
        if ! command -v docker >/dev/null 2>&1; then
            echo "Installing Docker..."
            sudo apt-get update -y
            sudo apt-get install -y docker.io
            sudo systemctl start docker
            sudo systemctl enable docker
            sudo usermod -aG docker jenkins
        else
            echo "Docker already installed"
        fi

        # Install Docker Compose if not installed
        if ! command -v docker compose >/dev/null 2>&1; then
            echo "Installing Docker Compose..."
            sudo apt-get install -y docker-compose
        else
            echo "Docker Compose already installed"
        fi

        docker --version
        docker compose version || docker-compose --version
        '''
    }

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

    stage('Run Containers') {
        echo "Starting services with Docker Compose..."
        sh '''
        docker compose up -d || docker-compose up -d
        '''
    }

    stage('Test Application') {
        echo "Running health check..."
        sh '''
        sleep 15
        curl -f http://localhost:3000 || (echo "App not responding on port 3000" && exit 1)
        '''
    }

    stage('Cleanup') {
        echo "Stopping and removing containers..."
        sh '''
        docker compose down || docker-compose down
        '''
    }
}
