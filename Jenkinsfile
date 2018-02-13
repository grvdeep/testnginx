node ('master'){
    def app
        stage ('checkout') {
           }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
    app = docker.build("yogeshdeepti/nginxproject")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }    
    
    stage('Push image')
    { docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
        app.push("${env.BUILD_NUMBER}")
        app.push("latest")
    }
    
}
}
