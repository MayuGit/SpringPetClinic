pipeline{
     environment {
        registry = "mayupdocker/petclinic"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    agent{label 'master'}
    tools{maven 'Maven3'}
    
    stages{
        stage('App Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/MayuGit/spring-petclinic.git'
            }
        }
        stage(' App Build'){
            steps{
                sh 'mvn compile'
            }
        }
        //stage('App Run Test'){
        //    steps{
        //        sh 'mvn test'
        //    }
        //}
        stage('App Package'){
            steps{
                sh 'mvn clean package'
            }
        }
        //stage('Deploy'){
        //    steps{
        //        sh 'java -jar ${WORKSPACE}/target/*.jar'
        //    }
        //}
        stage('Building Docker image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Upload Image to DockerHUB') {
            steps {    
                script {
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                    }
                }
            }
        }
         
        stage('Deploy image on client') {
           steps {
               script{
                   sh 'cp /var/jenkins_home/playbooks/dockerlogin.yml ${WORKSPACE}/dockerlogin.yml'
               }
               ansiblePlaybook credentialsId: 'sshvagrant5', installation: 'myansible', playbook: '/var/jenkins_home/playbooks/dockerlogin.yml'
           }
        }
         
        
    }
    
}
