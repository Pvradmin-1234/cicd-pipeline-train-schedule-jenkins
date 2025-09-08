pipeline {
  agent any

  tools {
    nodejs "node18"   // must match the Node.js name in Global Tool Configuration
  }

  stages {
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh 'npm test'
      }
    }

    stage('Deploy') {
      steps {
        // Ensure Jenkins can see pm2 (in /usr/local/bin usually)
        sh '''
          export PATH=$PATH:/usr/local/bin
          pm2 stop train-schedule || true
          pm2 delete train-schedule || true
          pm2 start app.js --name train-schedule
          pm2 save
        '''
      }
    }
  }

  post {
    success {
      echo '✅ Application deployed successfully and is accessible on port 3000'
    }
    failure {
      echo '❌ Build or deploy failed'
    }
  }
}
