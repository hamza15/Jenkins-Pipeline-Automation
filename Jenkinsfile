node('master') {
    def app

    stage('Clone repository') {

        checkout scm
    }

    stage('Build image') {
        /*  builds the actual image */
        sh 'export DOCKER_HOST=tcp://172.17.0.3:2375'
        app = docker.build("hellonode")
    }

    stage('Test image') {
        /* Test framework here */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* push the image with two tags:
         * Adds incremental build number from Jenkins
         * Adds the 'latest' tag. */
         
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
