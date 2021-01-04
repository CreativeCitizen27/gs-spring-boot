node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        //app = docker.build("getintodevops/hellonode")
        app = docker.build("test:0.3")
    }

    /*stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        /*app.inside {
        /*    sh 'echo "Tests passed"'
        /*}
    /*}*/

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('http://localhost:8081/repository/kobalti/', 'fa504b2e-f3b5-41d6-bb08-2a506e57d411') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}