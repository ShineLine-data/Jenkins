pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = 'MySonar'  // le nom que tu as donné à ton serveur dans Jenkins
        SONARQUBE_TOKEN = credentials('sonar-fil-rouge-token')  // le nom que tu as donné à ton serveur dans Jenkins

    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    script {
                        def scannerHome = tool 'LineSonar' // <= Ici on charge SonarScanner installer dans jenkins
                        sh '''
                            ${scannerHome}/bin/sonar-scanner \
                                -Dsonar.projectKey=sonar-project \
                                -Dsonar.sources=. \
                                -Dsonar.host.url=http://localhost:9000 \
                                -Dsonar.login=$SONARQUBE_TOKEN
                        '''
                    }
                    // sh 'sonar-scanner'
                }
            }
        }

        // stage('Quality Gate') {
        //     steps {
        //         timeout(time: 2, unit: 'MINUTES') {
        //             waitForQualityGate abortPipeline: true
        //         }
        //     }
        // }
    }

    post {
        success {
            echo '✅ Le pipeline s\'est terminé avec succès.'
        }
        failure {
            echo '❌ Le pipeline a échoué.'
        }
    }
}
