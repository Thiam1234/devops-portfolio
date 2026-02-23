pipeline {
    agent any
    
    stages {
        stage('📥 RÉCUPÉRATION CODE') {
            steps {
                echo 'Récupération du code depuis GitHub...'
                checkout scm
            }
        }
        
        stage('📝 INFOS') {
            steps {
                sh '''
                    echo "Build numéro: ${BUILD_NUMBER}"
                    echo "Révision Git: ${GIT_COMMIT}"
                    ls -la
                '''
            }
        }
        
        stage('🐳 BUILD DOCKER') {
            steps {
                sh '''
                    docker build -t moustapha-portfolio:${BUILD_NUMBER} .
                    docker images | grep moustapha-portfolio
                '''
            }
        }
        
        stage('✅ SUCCÈS') {
            steps {
                echo 'Pipeline GitHub → Jenkins → Docker réussi !'
            }
        }
    }
}
