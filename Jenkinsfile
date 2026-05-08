pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Stage 1: Build'
        echo 'Task: Compiling source code and packaging into an executable JAR/WAR file.'
        echo 'Tool: Apache Maven'
      }
    }

    stage('Unit and Integration Tests') {
      steps {
        echo 'Stage 2: Unit and Integration Tests'
        echo 'Task: Running JUnit tests for logic validation and Mockito for component interaction.'
        echo 'Tools: JUnit 5, Mockito'
      }
      post {
        always {
          emailext (
            subject: "Status: ${currentBuild.fullDisplayName} - Test Stage",
            body: "The Test stage finished with status: ${currentBuild.currentResult}. Please find the build logs attached.",
            recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
            to: 's225706972@deakin.edu.au',
            attachLog: true
          )
        }
      }
    }

    stage('Code Analysis') {
      steps {
        echo 'Stage 3: Code Analysis'
        echo 'Task: Checking for code smells, bugs, and technical debt against industry standards.'
        echo 'Tool: SonarQube'
      }
    }

    stage('Security Scan') {
      steps {
        echo 'Stage 4: Security Scan'
        echo 'Task: Scanning code for known vulnerabilities (SAST) and checking dependencies.'
        echo 'Tool: Snyk'
      }
      post {
        always {
          emailext (
            subject: "Status: ${currentBuild.fullDisplayName} - Security Scan",
            body: "Security Scan complete. Status: ${currentBuild.currentResult}",
            recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
            to: 's225706972@deakin.edu.au',
            attachLog: true
          )
        }
      }
    }

    stage('Deploy to Staging') {
      steps {
        echo 'Stage 5: Deploy to Staging'
        echo 'Task: Deploying the artifact to an AWS EC2 instance in a staging environment.'
        echo 'Tools: AWS CLI, SSH'
      }
    }

    stage('Integration Tests on Staging') {
      steps {
        echo 'Stage 6: Integration Tests on Staging'
        echo 'Task: Performing end-to-end (E2E) testing in a production-like environment.'
        echo 'Tool: Selenium'
      }
    }

    stage('Deploy to Production') {
      steps {
        echo 'Stage 7: Deploy to Production'
        echo 'Task: Final deployment of the verified build to the live AWS EC2 production fleet.'
        echo 'Tools: AWS CodeDeploy, Terraform'
      }
    }
  }
}