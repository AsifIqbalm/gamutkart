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
	stage('Package as WAR') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deployment') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '74a66a7e-ff19-4f54-b932-65a8a2c116f5', path: '', url: 'http://13.235.77.37:8081/')], contextPath: null, war: '**/*.war'
            }
        }
	
}
}
