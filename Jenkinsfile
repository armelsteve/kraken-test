//This Jenkinsfile build an image from a dockerfile
//push the image in dockerhub and deploy a kubernetes application using that image.

pipeline{
    options{
         buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
    }
    agent any
    stages{
       stage('Pull from scm'){
            steps{
                 git branch: 'master', credentialsId: 'myCreds', url: 'https://github.com/armelsteve/Devops-test'
            }
       }
       stage('build image'){
            steps{
                  sh 'docker build -t litecoin:latest .'
            }
       }
       stage('push image'){
            steps{
                  sh 'docker push litecoin:latest'
            }
       }
       stage('Deploy kubernetes app'){
            steps{
                  sh 'kubectl apply -f StatefulSet.yaml'
            }
       }
    }
    post{
        success{
            deleteDir()
        }
        failure{
            deleteDir()
        }
    }
}
