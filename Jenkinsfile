pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "OMPMAVEN"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/oppandey/mavenskillraryrepo.git'

                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                 bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    archiveArtifacts 'target/*.war'
                    deploy adapters: [tomcat9(credentialsId: 'ff95f430-c275-44c0-93e8-a314c433b7ba', path: '', url: 'http://localhost:8080')], contextPath: 'ompwebapp', war: '**/*.war'
                }
            }
        }
    }
}
