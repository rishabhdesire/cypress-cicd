pipeline {
   agent any
   options{
        ansiColor('xterm')
   }
   stages {
        stage('Build image') {
           steps {
               sh "docker build -t cypress-test ."
           }
        }
        stage('testing in chrome') {
           steps {
               sh "docker-compose run e2e-chrome"
               sh "docker ps"
           }
        }
        stage('Deploying') {
           steps {
               echo "Deploy the app"
           }
        }
        stage ('Report') {
            steps {
                  publishHTML(target: [allowMissing: false,
                  alwaysLinkToLastBuild: false,
                  keepAll: true,
                  reportDir: '/var/jenkins_home/workspace/cypess',
                  reportFiles: 'report.html',
                  reportName: 'ChromeReports',
                  reportTitles: 'jenkins-Chrome$BUILD_NUMBER'
                  ])
            }
        }
        stage('export') {
           steps {
               sh "cp -r /var/jenkins_home/jobs/cypress_cicd/builds/$BUILD_NUMBER/htmlreports/ChromeReports /home/hareesht/jenkins_home/workspace/$BUILD_NUMBER/htmlreports/ChromeReports"
           }
        }      
   }
}
