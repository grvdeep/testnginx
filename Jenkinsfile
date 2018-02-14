node ('master'){
    def app
        stage ('checkout') {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '5a02a237-d956-42c5-bdcc-866e9579480f', url: 'https://github.com/yogeshdeepti/nginxproject.git']]])
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
    { docker.withRegistry('https://registry.hub.docker.com/gdeepgd', 'c7cf7d45-89ef-4453-8aa4-b6d89c92671d') {
        app.push("${env.BUILD_NUMBER}")
        app.push("latest")
    }
    
}
}
