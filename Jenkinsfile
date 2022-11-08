pipeline {
    agent any

    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Git') {
            steps {
                checkout([$class: 'GitSCM',
                    userRemoteConfigs: [[url: 'https://github.com/testaccount123412/test.git']]])
            }
        }
        stage('Check') {
            steps {
                 dependencyCheck additionalArguments: ''' 
                    -o "./" 
                    -s "./"
                    -f "ALL" 
                    --prettyPrint''', odcInstallation: 'SCAChecker'
                    
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
                
            }
        }
    }
	post {
        always {
            echo 'This will always run2'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}