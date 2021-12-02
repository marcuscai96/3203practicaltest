pipeline {
	agent none
	stages {
		stage('Integration UI Test') {
			parallel {
				stage('Deploy') {
					agent any
					steps {
						sh "chmod +x -R ${env.WORKSPACE}"
						sh '/usr/share/jenkins/3203practicaltest/deploy.sh'
						input message : 'finished'
						sh '/usr/share/jenkins/3203practicaltest/kill.sh'
						
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
						
					
					}
					post {
						always {
							echo 'sucess'
						}
					}
				}
			}
		}
	}
}
