pipeline{
    agent any 

    parameters{
        choice(name:'action', choices:'create\delete', description: 'choose create/destroy')
    }
    stages{
        stage('git checkout'){

            when { expression { param.action=='create'}}
            
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
        stage('Static code analysis'){

            steps{

                script {

                    sh 'mvn clean package sonar:sonar'
                }
            }

        }

    }
}