pipeline {
    agent any
 
    tools {
        maven 'localMaven'
    }
 
stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    junit(
                        allowEmptyResults: true,
                        testResults: '**/*.xml'
                    )
                    recordIssues(
                    enabledForFailure: true, aggregatingResults: true,
                    tools: [java(), checkStyle(pattern: '**/*.xml', reportEncoding: 'UTF-8'), findBugs(pattern: '**/*.xml')]
                    )
                }
            }
        }
    }
}