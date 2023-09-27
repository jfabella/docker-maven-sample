pipeline {
    agent { label 'slave-1' }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                // docker create image
                sh "docker build . && docker ps"
            }
        }

        stage('Upload') {
            steps { 
                // docker push to nexus
                sh "echo Uploading to Nexus"
            }
        }
    }
}
