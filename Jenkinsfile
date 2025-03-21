pipeline {
	agent { label 'tomcat' }
	stages {
		stage('git checkout') {
			steps {
			git clone checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Sreedhara1993/war-web-project-java.git']])
			}
		}
		stage('build') {
			steps {
				sh "mvn clean install"
			}
		}
		stage('sonarqube analysis') {
			steps {
				withSonarQubeEnv(sonar) {
                sh "mvn clean verify sonar:sonar -Dsonar.projectKey=sonar_project_1"
                }
            }
        }
		stage('deploy') {
			steps {
				sh "cp /home/ec2-user/war-web-project/target/wwp-1.0.0.war /opt/tomcat/webapps"
				}
			}
		}
	post actions {
			success {
				echo "CICD pipeline succeeded"
			}
	}
}
