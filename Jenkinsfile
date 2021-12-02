pipeline {
	agent none
	stages {
		stage('Integration UI Test') {
			parallel {
				stage('Deploy') {
					agent any
					steps {
						sh "git url: 'https://github.com/marcuscai96/JenkinsDependencyCheckTest/blob/master/deploy.sh'"
						sh "git url: 'https://github.com/marcuscai96/JenkinsDependencyCheckTest/blob/master/kill.sh'"
						
					}
				}
				stage('Headless Browser Test') {
					agent {
						docker {
							image 'maven:3-alpine' 
							args '-v /root/.m2:/root/.m2' 
						}
					}
					steps {
						sh 'mvn -B -DskipTests clean package'
						sh 'mvn test'
						sh '--log-junit logs/unitreport.xml'
					
					}
					post {
						always {
							junit 'target/surefire-reports/*.xml'
						}
					}
				}
			}
		}
	}
}
