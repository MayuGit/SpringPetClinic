pipeline{
    agent{label 'master'}
    tools{maven 'Maven3'}
    
    stages{
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/MayuGit/SpringPetClinic.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('Test'){
            steps{
                sh 'mvn test'
            }
        }
        stage('Package'){
            steps{
                sh 'mvn package'
            }
        }
        stage('Deploy'){
            steps{
                sh 'java -jar /var/jenkins_home/workspace/myrunpipeline/target/spring-petclinic-2.1.0.BUILD-SNAPSHOT.jar'
            }
        }
    }
    
}
