pipeline{
    agent any 
    stages{
        stage('git checkout'){

            steps{

                script {

                    git 'https://github.com/Shadab-inzu/inzu_java_application.git'
                }
            }

        }
        stage('Unit Test Maven'){

            steps{

                script {

                    sh 'mvn test'
                }
            }

        }
        stage('Integration Test Maven'){

            steps{

                script {

                    sh 'mvn verify -DskipUnitTests'
                }
            }

        }

    }
}