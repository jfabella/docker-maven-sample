pipeline {
    agent { label 'slave-1' }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                // Run Maven on a Unix agent.
                configFileProvider([configFile(fileId: '8bb165e6-8f28-4b61-a443-1dd118a53225', variable: 'settingsxml')]) {
                    withMaven(maven: 'M3') {
                        sh 'mvn -Dmaven.test.failure.ignore=true clean package -s $settingsxml'
                    }
                }
                // docker create image
                sh "docker build --tag jfabella.jfrog.io/docker/test:1.0.0 ."
            }
        }

        

        stage('Upload to JFrog') {
            steps { 
                // docker push to nexus
                sh "docker push jfabella.jfrog.io/docker/test:1.0.0"
            }
        }
    }
}
