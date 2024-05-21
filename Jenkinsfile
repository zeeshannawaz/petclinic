pipeline {
	agent {
		label 'docker-k8s'
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
            //def mvn = tool 'Default Maven';
            withSonarQubeEnv() {
            sh "./mvnw clean verify sonar:sonar -Dsonar.projectKey=petclinic"
    }
  }
		stage('PublishArtifact') {
			steps {
				archiveArtifacts artifacts: '**/target/*.jar'
			}
		}
	}
}
