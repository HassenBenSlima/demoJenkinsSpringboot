pipeline {
  
          agent any

          tools {
            maven 'maven'
          }

          environment {
            DOCKERHUB_CREDENTIALS = credentials('hassenbenslima-lab-jenkins-spring')
           }


          stages{

           // Create a new .jar file 

            stage('Create a new .jar') {

                steps {
                    
                   sh 'mvn clean install -DskipTests'
                
                      }

          
            }

            // Create a docker image

            stage('Création d"une image docker') {

                steps {
                    
                   sh 'docker build -t spring_app_july2023_hassen_benslima .'
                
                      }

            }

            // Push docker image to dockerhub

            stage('Push image to dockerhub') {

                 steps {

                  sh 'docker tag spring_app_july2023_hassen_benslima hassenbenslima/spring_app_july2023_hassen_benslima'

                  sh 'echo $DOCKERHUB_CREDENTIALS_PSW \
                  | docker login -u $DOCKERHUB_CREDENTIALS_USR \
                  --password-stdin'

                  sh 'docker push hassenbenslima/spring_app_july2023_hassen_benslima'

                       }
                
                post {

                  always {

                  sh 'docker logout'

                         }

                     }

            }

            // Run Docker-compose

             stage('Docker-compose') {

                steps {

                sh 'docker-compose up -d'

                      }

              }

          }
   

     }




