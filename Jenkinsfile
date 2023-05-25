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
                    docker build -t 9945917850/javapp .
                   
                     """
                }
                    
                }
            }
           stage('Trivy scan'){
        when { expression { params.action == 'create'} }
            steps{

                script {
                    
                    sh """
                    trivy image 9945917850/javapp >scan.txt
                    cat scan.txt
                   
                     """
                }
                    
                }
            }
        stage('Docker Push'){
        when { expression { params.action == 'create'} }
            steps{

                script {
                    
                    
                    withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                   sh """
                   docker login -u '$USER' -p '$PASS'
                   docker push 9945917850/javapp
                   """
                }
                   
                     
                }
                    
                }
            }
         stage('Docker Image cleanup'){
        when { expression { params.action == 'create'} }
            steps{

                script {
                    
                    sh """
                    docker rmi 9945917850/javapp 
                    docker rmi springboot/javapp
                    
                   
                     """
                }
                    
                }
            }       


    }
}