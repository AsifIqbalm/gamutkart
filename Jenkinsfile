pipeline {
    agent any

    stages {
        stage('Clone-Repo') {
	    	steps {
	        	checkout scm
	    	}
        }
	stage('Build') {
		steps {
			withMaven(maven: 'mvn'){
			sh 'mvn install'
		}
	}	
	}	
	stage ('Compile'){
	        steps { 
			withMaven(maven: 'mvn'){
			sh 'mvn clean compile'
                }
	}
	}

	stage('Run Tests') {
	    steps {
		    withMaven(maven: 'mvn'){
	       sh 'mvn test'
	    }
	}
	}

        stage('Package as WAR') {
            steps {
		    withMaven(maven: 'mvn'){
                sh 'mvn package'
            }
        }
	}
	stage('Deployment') {
	   steps {
		sh 'sshpass -p staragile scp target/gamutkart.war staragile@172.31.44.167:/home/staragile/apache-tomcat-9.0.85/webapps/'
	}
    }
}
}
