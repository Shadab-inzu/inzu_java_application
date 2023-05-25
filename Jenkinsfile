pipeline{
    agent any 

    parameters{
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose Create/Destroy')
    }
    stages{
        stage('git checkout'){

            when { expression { params.action == 'create'} }
            
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
        when { expression { params.action == 'create'} }
            steps{

                script {

                    sh 'mvn verify -DskipUnitTests'
                }
            }

        }
        stage('Static code analysis'){
        when { expression { params.action == 'create'} }
            steps{

                script {
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                    // some block
                    sh 'mvn clean package sonar:sonar'
                    
                }
                    
                }
            }

        }
        stage('Quality Gate Status'){
        when { expression { params.action == 'create'} }
            steps{

                script {
                    
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
                }
                    
                }
            }
        stage('maven build'){
        when { expression { params.action == 'create'} }
            steps{

                script {
                    
                    sh 'mvn clean install'
                }
                    
                }
            }
        stage('Docker Image build'){
        when { expression { params.action == 'create'} }
            steps{

                script {
                    
                    sh """
                    docker build -t java-app .
                   
                     """
                }
                    
                }
            }

        


    }
}