node {
    stage('Checkout') {
        git branch: 'main', url: 'https://github.com/mloges-h/Docker_nodejs_mangodb_mangoexpress.git'
    }

    stage('Build Docker Images') {
        sh "docker compose build || docker-compose build"
    }

    stage('Run Containers') {
        sh "docker compose up -d || docker-compose up -d"
    }

    stage('Test Application') {
        sh '''
        sleep 15
        curl -f http://localhost:3000 || (echo "App not responding" && exit 1)
        '''
    }

    stage('Cleanup') {
        sh "docker compose down || docker-compose down"
    }
}
