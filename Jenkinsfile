pipeline {
    agent none
            
    // triggers {
    //     pollSCM '* * * * *'
    // }
    
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'python:3.11'
                    reuseNode true
                }
            }
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
            agent {
                docker {
                    image 'python:3.11'
                    reuseNode true
                }
            }
            steps {
                echo "Testing.."
                sh '''
                cd myapp
                pip install --upgrade pip
                pip install -r requirements.txt
                python3 hello.py
                python3 hello.py --name=Brad
                '''
            }
        }
        
        stage('Deliver') {
            agent any
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
