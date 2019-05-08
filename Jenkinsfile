pipeline {
    agent any
    stages {
        stage ('Build Servlet Project') {
            steps {
                /*For windows machine */
               bat  'mvn clean package'

                /*For Mac & Linux machine */
               // sh  'mvn clean package'
            }

            post{
                success{
                    echo 'Now Archiving ....'

                    archiveArtifacts artifacts : '**/*.war'
                }
            }
        }

        stage ('Deploy Build in Staging Area'){
            steps{

                build job : 'Pipeline_Deploy_Stage_Area'

           }
        }

        stage ('Deploy to Production'){
            steps{
                timeout (time: 4, unit:'DAYS'){
                   input message: 'Approve PRODUCTION Manager?'
               }
               
                build job : 'Pipeline_Deploy_Production_Area'
            }

            post{
                success{
                    echo 'Deployment on PRODUCTION is Successful !!!!!!!!!!'
               }

                failure{
                   echo 'Deployement Failure on PRODUCTION !!!!!!!!!!'
               }
           }
        }
    }
}
