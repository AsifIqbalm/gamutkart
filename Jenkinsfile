pipeline {
    agent {
	    label "the-slave"
    }
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
		sh 'ssh scp target/gamutkart.war root@172.31.43.62:/home/jenkins/apache-tomcat-9.0.85/webapps/'
	}
    }

	
}
}
