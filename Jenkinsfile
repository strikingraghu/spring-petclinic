pipeline {
    
    agent any

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/spring-projects/spring-petclinic.git'
                git 'git remote prune origin --dry-run'

                // Run Maven on a Unix agent.
                sh "mvn clean -X"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
