pipeline {
    agent any
	tools {
        maven 'maven4'
    }

    stages {
	 stage('Clone-Repo') {
	    	steps {
	        	checkout scm
	    	}
        }
	stage('Build') {
		steps {
			sh 'mvn install'
		}
	}	
 
	stage ('Compile'){
	        steps {
			sh 'mvn clean compile'
                }
	}

	stage('Run Tests') {
	    steps {
	       sh 'mvn test'
	    }
	}
	stage('Deployment') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Package as WAR') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '74a66a7e-ff19-4f54-b932-65a8a2c116f5', path: '', url: 'http://65.2.4.164:8081/')], contextPath: null, war: '**/*.war'
            }
        }
	
}
}
