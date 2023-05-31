pipeline {
    agent {
        docker {
            image 'cypress/base:12.16.1' 
            args '-p 3000:3000' 
        }
    }
    stages {
	       
	    stage('Check versions') {
	        steps {
	            echo '######## Check versions ########'
			    sh "node --version"
	            sh "cd cypress"

		    }
		}
	            
	    stage('Install dependencies') {
	        steps {
	            echo '######## Install dependencies ########'
	            sh "npm install"
	        }
	    }
	            
	    stage('client-e2e-testing') {
	        steps {
	            echo '######## Running cypress tests ########'
	            sh "npm run testsmokechrome"   // run the relevant script in package json
	        }
		
        post {
   		always {
      			publishHTML (target : [
			        allowMissing: true,
                    alwaysLinkToLastBuild: false,
                    keepAll: false,
                    reportDir: 'cypress',
                    reportFiles: 'mochawesome.html',
                    reportName: 'HTML Report',
                    reportTitles: 'HTML Report']) 
   			    }
           }
	    }
    }
}