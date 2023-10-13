pipeline{

     agent any

   parameters{
     string(name: 'ENV', defaultValue: 'prod', description: 'which environemnt to run ')
     string(name: 'APPNAME', defaultValue: '', description: 'which environemnt to run ')
       }

  stages{
       stage('update kubectl'){
         steps{
           sh 'aws eks update-kubeconfig --name ${ENV}-roboshop'
           }
       }

       stage('get code '){
         steps{
           dir ('APP'){
             git branch: 'main', url: 'https://github.com/sreedharm07/a-${APPNAME}.git'
            }
           dir ('CHART'){
              git branch: 'main', url: 'https://github.com/sreedharm07/robo-helm.git'
                 }
           }
        }

        stage('update kubectl'){
           steps{
            sh ' helm install ${APPNAME} ./CHART  --set component=${APPNAME} '
                  }
              }

        }
 }