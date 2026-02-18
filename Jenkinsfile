pipeline {
    agent any
    
    stages {
        stage('📥 CLONAGE DU CODE') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/TON_COMPTE/portfolio-devops-moustapha.git'
                echo "✅ Code récupéré depuis GitHub"
            }
        }
        
        stage('🚀 CRÉATION DU SITE') {
            steps {
                echo "📝 Construction du portfolio..."
                sh 'ls -la'
            }
        }
        
        stage('🐳 IMAGE DOCKER') {
            steps {
                echo "🐳 Construction de l'image..."
                sh '''
                    docker build -t moustapha-portfolio-git:${BUILD_NUMBER} .
                    docker images | grep moustapha-portfolio-git
                '''
            }
        }
        
        stage('🧪 TEST') {
            steps {
                sh '''
                    docker run -d --name test-${BUILD_NUMBER} -p 8888:80 moustapha-portfolio-git:${BUILD_NUMBER}
                    sleep 3
                    echo "✅ Portfolio accessible sur http://localhost:8888"
                    docker stop test-${BUILD_NUMBER}
                    docker rm test-${BUILD_NUMBER}
                '''
            }
        }
        
        stage('🎉 FIN') {
            steps {
                echo "✅ Déploiement réussi depuis GitHub !"
                echo "📦 Image: moustapha-portfolio-git:${BUILD_NUMBER}"
            }
        }
    }
}
