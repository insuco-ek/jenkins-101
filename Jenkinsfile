pipeline {
    agent {
        docker {
            image 'python:3.11-slim'
            // Garde le workspace monté pour persister les fichiers
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
            
    // triggers {
    //     pollSCM '* * * * *'
    // }
    
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                cd myapp
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }
        
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                cd myapp
                python3 hello.py
                python3 hello.py --name=Brad
                '''
            }
        }
        
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline terminé'
        }
        success {
            echo 'Pipeline exécuté avec succès!'
        }
        failure {
            echo 'Le pipeline a échoué'
        }
    }
}
