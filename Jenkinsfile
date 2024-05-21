pipeline {
	agent {
		label 'maven'
	}
	stages {
		stage('Build') {
			steps {
				sh '''
					sh "./mvnw compile"
					sh "./mvnw package"
                                '''
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
		stage('PublishArtifact') {
			steps {
				archieveArtifacts artifacts: '**/target/*.jar'
			}
		}
	}
}
