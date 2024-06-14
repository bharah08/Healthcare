pipeline{
    agent any
     tools{
         maven 'maven'
     }
     
    stages{
       stage('unit-testing'){
           steps{
               sh 'mvn test'
           }
       } 
        
       stage('build'){
           steps{
               sh 'mvn clean install'
           }
       } 
       stage('docker-mage build'){
         steps{
           sh 'docker build -t bharath0812/java:7.0 .'
         }
       }
         stage('deploy'){
         steps{
   withDockerRegistry(credentialsId: 'dockerhub') {
    sh 'docker push bharath0812/java:7.0'
}
         }
       }
        stage('deploy-k8s'){
            steps{
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'my-eks', contextName: '', credentialsId: 'eks-jenkins', namespace: '', serverUrl: 'https://72315A3A81F6E4C9C2B5AE2E6499E99D.gr7.ap-south-1.eks.amazonaws.com']]) {
    sh 'kubectl apply -f de.yml'
}
            }
        }


    }
}
