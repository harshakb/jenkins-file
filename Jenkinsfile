pipeline {
    agent any

	tools {
		maven 'maven3.6'
	}
//
//	environment {
//		M2_INSTALL = "/home/harshakb/softwares/apache-maven-3.6.1/bin/mvn"
//	}

    stages {
		stage('Clone-Repo') {
			steps {
				checkout scm
			}
		}
		stage('Build') {
	    	steps {
				sh 'mvn install -DskipTests'
			}
	    }
		stage('Unit Tests') {
			steps {
				sh 'mvn surefire:test'
			}
		}
		stage('Deployment') {
	    	steps {
				sh 'sshpass -p "khan" scp target/gamutkart.war harsha@172.17.0.2:/home/softwares/apache-tomcat-8.5.45/webapps'
				sh 'sshpass -p "khan" ssh harsha@172.17.0.2 "/home/softwares/apache-tomcat-8.5.45/bin/startup.sh"'
	    	}
		}
    }
}
