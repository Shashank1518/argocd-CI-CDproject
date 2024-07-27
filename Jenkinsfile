pipeline{
  agentany{
  environment{
    DOCKERHUB_USERNAME = "shashank1518"
    APP_NAME = "argocd-CI-CDproject"
    IMAGE_TAG = "${BUILD_NUMBER}"
    IMAGE_NAME = "${DOCKERHUB_USERNAME}"+ "/" +"${APP_NAME}"
    REGISTRY_CREDS = 'dockerhub'
  }
  stages{


    
      stage('Git checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/Shashank1518/argocd-CI-CDproject.git'  
        }   
      }
      stage('Build Docker image'){
        steps{
          sh "docker build -t "${IMAGE_NAME}"
        }
      }
      stage('Push Docker image'){
        steps{
          docker.withRegistry('',REGISTRY_CREDS){
            sh "docker push ${BUILD_NUMBER}"
            sh "docker push ('latest')"
          }
        }
      }

















        
      
    }
  }
}
