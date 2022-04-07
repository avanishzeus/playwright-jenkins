pipeline {
  agent { 
    node {
      label 'jenkins-agent'
    }
  }
  stages {
    stage('install playwright') {
      steps {
        sh '''
          npm i
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
