pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Récupération du code source...'
                checkout scm
            }
        }
        
        stage('Setup Python Environment') {
            steps {
                echo 'Configuration de l\'environnement Python...'
                dir('myapp') {
                    // Créer un environnement virtuel
                    sh 'python3 -m venv venv'
                    
                    // Activer l'environnement et installer les dépendances
                    sh '''
                        . venv/bin/activate
                        pip install --upgrade pip
                        pip install -r requirements.txt
                    '''
                }
            }
        }
        
        stage('Test') {
            steps {
                echo 'Exécution des tests...'
                dir('myapp') {
                    sh '''
                        . venv/bin/activate
                        python -m pytest tests/ --junitxml=test-results.xml
                    '''
                }
            }
            post {
                always {
                    // Publication des résultats de tests
                    junit 'myapp/test-results.xml'
                }
            }
        }
        
        stage('Build/Package') {
            steps {
                echo 'Construction de l\'application...'
                dir('myapp') {
                    sh '''
                        . venv/bin/activate
                        python setup.py build
                        # ou python -m build pour les projets avec pyproject.toml
                    '''
                }
            }
        }
        
        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo 'Déploiement en cours...'
                dir('myapp') {
                    sh '''
                        . venv/bin/activate
                        # Commandes de déploiement
                        echo "Déploiement simulé"
                    '''
                }
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline terminé'
            cleanWs()
        }
        success {
            echo 'Pipeline exécuté avec succès!'
        }
        failure {
            echo 'Le pipeline a échoué'
        }
    }
}
