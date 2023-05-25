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

                    sh 'mvn clean install -DskipTests'
                }
            }

        }

    }
}