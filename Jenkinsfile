pipeline {
  agent { 
    docker { 
      image 'mcr.microsoft.com/playwright:v1.17.2-focal'
      args  '-w /var/jenkins_home/workspace/test-pipeline -v //e/jenkins/workspace/test-pipeline:/var/jenkins_home/workspace/test-pipeline:rw,z'
    } 
  }
  stages {
    stage('install playwright') {
      steps {
        sh '''
          npm i
          npx playwright install
        '''
      }
    }
    stage('test') {
      steps {
        sh '''
          npx playwright test --list
          npx playwright test
        '''
      }
      post {
        success {
          archiveArtifacts(artifacts: 'homepage-*.png', followSymlinks: false)
          sh 'rm -rf *.png'
        }
      }
    }
    stage('cleanup') {
      steps{
        cleanWs()
      }
    }
  }
}
