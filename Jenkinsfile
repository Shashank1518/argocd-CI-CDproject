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
    
      stage('SonarQube Code quality'){
        steps{
          bat '''
            sonar-scanner.bat -D"sonar.projectKey=argocd" -D"sonar.sources=." -D"sonar.host.url=http://localhost:9000" -D"sonar.token=sqp_e5750e6fc984c10ef7100d81b908b6c904a68849"
            '''
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

     stage('Image Name'){
        steps{
          script{
            echo "Image name: ${IMAGE_TAG}"
          }
        }
      }
    /*
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
          sh "curl -v -k -user shashank1518:11166b25e5ada9f7ffda8f381886a91cb9 -X POST -H 'cache-control: no-cache' -H 'content-type: application/x-www-form-urlencoded' -data 'IMAGE_TAG=${IMAGE_TAG}' 'http://localhost:8080/job/argocd-cd-project/buildWithParameters?token=argo-ci-cdproject'"
        }
      }
    }
*/














        
      
    }
}
