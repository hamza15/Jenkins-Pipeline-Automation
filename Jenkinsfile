pipeline {
    agent {label 'master' }  
    stages {
        stage('build') {
            steps {
                sh '''
                	export DOCKER_HOST=tcp://172.17.0.3:2375
                	docker build -t hellonode .
                	docker images
                '''	
            }
        }
        stage('post build') {
            steps {
        		sh '''
                	docker ps
                '''	
        	}	
        }
    }
}
