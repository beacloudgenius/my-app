pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh script: '''
        git checkout master
        npm install
        npm run build
       ''', label: "Building production"
      }
    }

    stage('Deploy') {
      steps {
        sh script: '''
        aws s3 sync build/ s3://thecloudseminar.com --acl public-read --delete
        ''', label: "Deploying to https://thecloudseminar.com"
      }
    }
  }
  post {
        always {
            echo 'This will always run'
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
