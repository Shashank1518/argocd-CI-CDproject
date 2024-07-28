pipeline{
  agent any
  environment{
    DOCKERHUB_USERNAME = "shashank1518"
    APP_NAME = "argocd-ci-cdproject"
    IMAGE_TAG = "${BUILD_NUMBER}"
    IMAGE_NAME = "${DOCKERHUB_USERNAME}"+ "/" +"${APP_NAME}"
    REGISTRY_CREDS = 'dockerhub'
  }
  stages{


    
      stage('Git checkout'){
        steps{
          script{
            git credentialsId: 'github', 
            branch: 'main', url: 'https://github.com/Shashank1518/argocd-CI-CDproject.git'  
          }
        }   
      }
    
      stage('Build Docker image'){
        steps{
          script{
            docker_image = docker.build "${IMAGE_NAME}"
          }
        }
      }
    
      stage('Push Docker image'){
        steps{
          script{
            docker.withRegistry('',REGISTRY_CREDS){
               docker_image.push("$BUILD_NUMBER")
               docker_image.push('latest')
            }
          }
        }
      }

     stage('Image name'){
        steps{
          script{
            sh """
            cat IMAGE_NAME
            """
          }
        }
      }
    
      stage('delete Docker Image'){
        steps{
          script{
            sh "docker rmi ${IMAGE_NAME}:${IMAGE_TAG}"
            sh "docker rmi ${IMAGE_NAME}:latest"
          }
        }
      }
    
    stage('Trigger CD pipeline'){
      steps{
        script{
          sh "curl -v -k -user shashanklm:1174916737108e20a5e9a64d56d815d9ed -X POST -H 'cache-control: no-cache' -H 'content-type: application/x-www-form-urlencoded' -data 'IMAGE_TAG=${IMAGE_TAG}' 'http://3.89.3.215:8080/job/argo-ci-cdproject-CD/buildWithParameters?token=argo-ci-cdproject'"
        }
      }
    }
















        
      
    }
}
