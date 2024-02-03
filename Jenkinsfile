pipeline {
  agent {
    node {
      label 'test'
    }

  }
  stages {
    stage('petclinic') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('StaticAnalysis') {
      steps {
        sh './mvnw sonar:sonar -Dsonar.host.url=http://172.31.22.207:9000/ -Dsonar.projectKey=petclinic -Dsonar.login=sqp_5d8dc511eb5f85ab66aa22a1ce4cfec6a3dbb1f8'
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
        junit '**/target/surefire-reports/TEST-*.xml'
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package -DskipTests=true'
      }
    }

    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            sh './mvnw spring-boot:run </dev/null &>/dev/null &'
          }
        }

        stage('Integration and Performance Tests') {
          steps {
            sh './mvnw verify'
          }
        }

      }
    }

  }
}