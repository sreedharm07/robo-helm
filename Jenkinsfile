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

       stage('get code'){
         steps{
           dir ('APP'){
             git branch: 'main', url: 'https://github.com/sreedharm07/a-${APPNAME}.git'
            }
           dir ('CHART'){
              git branch: 'main', url: 'https://github.com/sreedharm07/robo-helm.git'
            }
            sh 'pwd'
          }
       }

      stage('installing component'){
             steps{
            sh ' helm upgrade -i ${APPNAME} ./CHART  -f APP/helm/${ENV}.yaml '
                  }
              }
    }
 }