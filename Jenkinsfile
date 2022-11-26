pipeline{
    agent any
    stages{
        stage('git checkout'){
            steps{
                git credentialsId: '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',url:'https://github.com/orandri/simple-java-maven-app'
            }
        }
        
        stage('Build the application'){
            steps{
                bat 'mvn clean install'
            }
        }
        
        stage('Unit Test Execution') {
            steps{
                bat 'mvn test'
            }
        }
        
        stage('build docker image'){
            steps{
                bat 'docker build -t orandri91/java-hello-world .'
            }
        }
        
        stage('push docker image'){
            steps{
                withCredentials([usernamePassword(credentialsId: '9aa7b8d4-c9a9-457f-91a4-18fdc01cdb1c', usernameVariable:'dockerHubUser',passwordVariable:'dockerHubPass')]) {
                    bat "docker login -u$dockerHubUser -p$dockerHubPass"
                }
                bat 'docker push orandri91/java-hello-world'
            }
        }
        
        

    }
}

