pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Récupération du code depuis ton fork GitHub'
            }
        }

        stage('Build Maven') {               // si le projet est en Java/Maven
            steps {
                sh 'mvn clean package'       // ← cette ligne est souvent obligatoire
            }
        }

        stage('Docker Build') {              // ← C’EST L’ÉTAPE QUE TON PROF VEUT VOIR
            steps {
                sh 'docker build -t mon-app .'
                // ou parfois avec ton prénom/nom d’étudiant :
                // sh 'docker build -t prenom-nom-app .'
            }
        }

        stage('Docker Run (optionnel)') {    // certains profs le demandent, d’autres non
            steps {
                sh '''
                    docker stop mon-app || true
                    docker rm mon-app || true
                    docker run -d --name mon-app -p 8080:8080 mon-app
                '''
            }
        }
    }

    post {
        success {
            echo 'Docker build réussi ! Bravo, ton TP est validé !'
        }
        failure {
            echo 'Il y a une erreur, relis le console output'
        }
    }
}
