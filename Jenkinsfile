pipeline{
    agent any
    environment { 
                  registry1 = "519852036875.dkr.ecr.us-east-2.amazonaws.com/cloudjournee:${env.BUILD_NUMBER}"
                }
    tools {maven "MAVEN"}
    stages{
        stage('code checkout from GitHub'){
            steps{
                //check out code from the GitHub
                git branch: 'master', url: 'https://github.com/Abhilash-1201/CJP-Internal.git'
            }
        }
        //This stage gets all code Quality check from the GitHub Repository
        stage('Code Quality Check via SonarQube'){
            steps{
                script{
                    def scannerHome = tool 'sonarqube-scanner';
                    withSonarQubeEnv(credentialsId: 'sonarqube_access_token'){
                        if(fileExists("sonar-project.properties")) {
                         sh "${tool("sonarqube-scanner")}/bin/sonar-scanner"
                             
                         }  
                        
                    }
                }
            }
        }
#        stage('BUILDING ARTIFACT'){
#     			 steps{
#        			  echo 'build '
#                sh "mvn clean package"
#     			  }
#        }
#        stage('DOCKER IMAGE FOR DEV') 
#        {
#          steps{
#              script {
#                myImage = docker.build registry1
#              }
#           }
#        }
#       stage('PUSHING TO DEV ECR') {
#          steps{  
#          script {
##                 sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 519852036875.dkr.ecr.us-east-2.amazonaws.com'
#                 sh 'docker push ${registry1}'
#
#              }
#           }
#       }
#        //Deploy docker image in to dev eks 
#       stage (' DEV K8S Deploy') {
#       steps { 
#                kubernetesDeploy(
#                    configs: 'springboot.yaml',
#                    kubeconfigId: 'DEVK8',
#                    enableConfigSubstitution: true
#                    )               
#             }  
#         }
//         //Conformation to production after approval
//         stage('Prod Approval confirmation') {
//             agent { label 'login_page'}
//             steps{
//             script {
//                         env.RELEASE_TO_PROD = input message: 'Do you want to create prod build?',
//                             parameters: [choice(name: 'Promote to production', choices: 'No\nYes', description: 'Choose "yes" if you want to deploy this build in production')]
//                         milestone 1
//                     }
//             }

//         }
         // Build the docker image to store in to Prod ECR
#        stage('DOCKER IMAGE FOR PROD')  {
#         steps{
#           script{
#               dockerImage = docker.build registry1
#           }
#         }
#       }
#         // Push the docker image in to prod ECR
#       stage('PUSHING TO PROD-ECR') {
#        steps{  
#         script {
#                //sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 519852036875.dkr.ecr.us-east-2.amazonaws.com'
#                sh 'docker push ${registry1}'
#               }
#           }
#      
#        }  

        //Email notification after build get successful
#        stage('Build success email notification ') {
#          steps {
#            mail to: "digin@cloudjournee.com",
 #                cc: "nayab.s@cloudjournee.com",
#                subject: "SUCCESSFUL: Build ${env.JOB_NAME} ${env.BUILD_NUMBER}",
#                body: "Build Successful!! Build ${env.JOB_NAME} with ${env.BUILD_NUMBER}\n\n\nBuild Name:  ${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}\nJenkins URL: ${env.BUILD_URL}\n\nClick below link to proceed to prod environment\n\nhttp://18.223.203.85:8080/job/CJP-Internal-PROD/buildWithParameters?token=123456&BuildNumber=${env.BUILD_NUMBER}"
#            }
#        }     
    }
   
}
