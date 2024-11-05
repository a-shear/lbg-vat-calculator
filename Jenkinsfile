pipeline {
	agent any

	stages {
		stage('Checkout'){
			steps {
				git branch: 'main', url: 'https://github.com/a-shear/lbg-vat-calculator.git'
			}
		}
		stage('Install'){
    			steps {
        			//Install the ReactJS dependencies
        			sh "npm install"
    			}
		}	
		stage('Test'){
    			steps{
        			//Run the ReactJS tests
        			sh "npm test"
    			}
		}		
		stage('SonarQube Analysis'){
			environment {
				scannerHome = tool 'sonarqube'
			}
				steps {
					withSonarQubeEnv('sonar-qube-1') {
						sh "${scannerHome}/bin/sonar-scanner"
					}
				
					timeout(time:10, unit: 'MINUTES'){
                    				waitForQualityGate abortPipeline: true
                			}
			}
		}
	}
}
