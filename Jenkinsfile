pipeline{
    agent any
     environment{
        dockerhub_repo = "shivampateriyaknoldus/spring"
        dockerhub_creds = 'dockershivam'
        dockerImage = ''
     }
    tools { 
        maven 'maven3'
        // Docker 'docker'
    }
    stages
       {
            stage("clean")
            {
                steps{
                    sh "mvn clean"
                }
            }
            stage("Build")
            {
                steps{
                    sh "mvn compile"
                }
                
            }
             stage("TEST")
            {
                steps{
                    sh "mvn test"
                }
            } 
            stage("deploy")
            {
               steps{
                      withKubeConfig([credentialsId: 'kube']){ 
                       sh 'pwd && ls'   
                       sh 'kubectl get po'   
                    // sh 'pwd && ls'
                       sh 'kubectl apply -f app-deployment.yml'
                    // sh 'kubectl apply -f kubernetes/app/deployment.yml'
                    // sh 'kubectl apply -f kubernetes/app/nodeport.yml'
                    }

            }
            }
            //  stage("package")
            // {
            //     steps{
            //         sh "mvn package"
            //     }
            // } 
            //  stage("building docker image"){
            //         steps{
            //             script{
            //                 dockerImage = docker.build dockerhub_repo + ":$GIT_COMMIT-build-$BUILD_NUMBER"
            //             }
                       
            //          }    
            //     }
            // stage("Pushing the docker image"){
            //         steps{
            //             script {
            //                 docker.withRegistry('', dockerhub_creds){
            //                     dockerImage.push()
            //                     dockerImage.push('latest')
            //                     // dockerImage.push('v1')
            //                 }
            //             }
            //         }
            //     }    
        }
}      
