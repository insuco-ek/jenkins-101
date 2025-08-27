pipeline {
    agent any
            
    // triggers {
    //     pollSCM '* * * * *'
    // }
    
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                # Installer python3-venv si nécessaire
                sudo apt update
                sudo apt install -y python3-venv python3-full
                
                cd myapp
                
                # Créer un environnement virtuel
                python3 -m venv venv
                
                # Activer l'environnement virtuel et installer les dépendances
                . venv/bin/activate
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
                
                # Activer l'environnement virtuel pour les tests
                . venv/bin/activate
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
            // Nettoyage optionnel
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
