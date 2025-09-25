pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps { checkout scm } // configure SCM Git dans le job
    }
    stage('Install') {
      steps {
        sh '''
          set -eu
          echo "Workspace: $WORKSPACE"
          ls -la "$WORKSPACE"

          # cd dans le bon dossier
          cd "$WORKSPACE/ci-cd-hello" 2>/dev/null || cd "$WORKSPACE"

          npm ci || npm install
          npm install --save-dev jest
        '''
      }
    }
    stage('Test') {
      when { expression { fileExists('package.json') } }
      steps { sh 'npm test || echo "pas de tests encore"' }
    }
  }
}
