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

                    sh 'mvn clean compile -Dmaven.compiler.args="--add-opens com.sun.tools.javac.processing=ALL-UNNAMED"'
                }
            }

        }

    }
}