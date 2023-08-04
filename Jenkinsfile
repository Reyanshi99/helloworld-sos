pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Reyanshi99/helloworld-sos.git'
      }
    }
    stage('Pull Changes') {
      steps {
        sh 'git pull origin main'
      }
    }
    stage('Build') {
      steps {
        echo '<--------------- Building --------------->'
        sh 'printenv'
        sh '/opt/apache-maven-3.9.4/bin/mvn clean install'
        echo '<------------- Build completed --------------->'
      }
    }
    stage('Unit Test') {
      steps {
        echo '<--------------- Unit Testing started  --------------->'
        sh '/opt/apache-maven-3.9.4/bin/mvn surefire-report:report'
        echo '<------------- Unit Testing stopped  --------------->'
      }
    }
   stage("Scan") {
          steps {
              withSonarQubeEnv(installationName: 'sonarqube_token') {
                 sh '/opt/apache-maven-3.9.4/bin/mvn clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
              }
          }
      }

    
}
}
