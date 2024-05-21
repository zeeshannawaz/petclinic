pipeline {
	agent {
		label 'maven'
	}
	environment {
	    scannerHome = tool 'SonarQubeScanner2'
	}
	stages {
		stage('checkout') {
			steps {
				git branch: 'main', credentialsId: 'zeeshan.nawaz275@gmail.com', url: 'https://github.com/zeeshannawaz/petclinic.git'
			}
		}
		stage('Build') {
			steps {
			    script {
					    sh "./mvnw compile"
					    sh "./mvnw package"
			    }
			}
		}
		stage('Tests') {
			steps {
				junit '**/target/surefire-reports/TEST*.xml'
			}
		}
		stage('CodeCoverage') {
			steps {
				jacoco()
			}
		}
		stage('SonarQube Analysis') {
		    steps{
                //def mvn = tool 'Default Maven';
                //def scannerHome = tool 'SonarQubeScanner2'
                withSonarQubeEnv('SonarQube') {
                    script {
                        //sh "${scannerHome}/bin/sonar-scanner"
                        //sh './mvnw clean verify sonar:sonar -Dsonar.projectKey=petclinic'
                        sh './mvnw clean verify sonar:sonar -Dsonar.projectKey=petclinic -Dsonar.host.url=http://localhost:30900 -Dsonar.login=sqp_e04528492196546998f65f83c5953d91d60efa29'
                    }
                }
		    }
        }
		stage('PublishArtifact') {
			steps {
				archiveArtifacts artifacts: '**/target/*.jar'
			}
		}
	}
}
