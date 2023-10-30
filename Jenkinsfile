pipeline {
    agent any
    environment {
        // Ajouter la variable dh_cred comme variables d'authentification
        DOCKERHUB_CREDENTIALS = credentials('dh_cred')
    }
    triggers {
        pollSCM('*/5 * * * *') // Vérifier toutes les 5 minutes
        }
        stages {
            stage('Checkout'){
                agent any
                steps{
                    checkout scm
                    }
                    }
                    stage('Init'){
                        steps{
                            // Permet l'authentification
                            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                            }
                            }
                            stage('Build'){
                                steps {
                                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/express-sqlite-app:$BUILD_ID .'
                                    }
                                    }
                                    stage('Deliver'){
                                        steps {
                                            sh 'docker push $DOCKERHUB_CREDENTIALS_USR/express-sqlite-app:$BUILD_ID'
                                            }
                                            }
                                            stage('Cleanup'){
                                                steps {
                                                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/express-sqlite-app:$BUILD_ID'
                                                    sh 'docker logout'
                                                    }
        }
    }
}