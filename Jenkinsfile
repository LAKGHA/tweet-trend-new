pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.5/bin:$PATH"
}
    stages {
        stage('build') {
            steps {

                echo "------Build started----"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "------Build ended----"
            }
        }
        stage("test") {
            steps {
                  echo "------Unit test started----"
                 sh 'mvn surefire-report:report'
                 echo "------Unit test ended----"
            }
        }
           

        stage('SonarQube analysis') {
    environment {
      scannerHome = tool 'Valaxy-Sonar-Scanner'
    }
    steps{
    withSonarQubeEnv('Valaxy-Sonarqube-Server')

     { // If you have configured more than one global server connection, you can specify its name
      sh "${scannerHome}/bin/sonar-scanner"
    }
    }
    }
    }
}