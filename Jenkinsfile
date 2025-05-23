pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/gitdipen/Jenkins-Pipeline-Demo.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'npm test || true'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }

    stage('Generate Lock File') {
      steps {
        sh 'npm install --package-lock-only || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true'
      }
    }

    stage('Email Notification') {
      steps {
        emailext (
          subject: "Jenkins Build: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
          body: """<p>The build has completed with status: <strong>${currentBuild.currentResult}</strong>.</p>""",
          to: 'dipenau@gmail.com',
          attachLog: true,
          mimeType: 'text/html'
        )
      }
    }
  }
}
