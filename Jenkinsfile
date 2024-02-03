pipeline {
  agent any
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

  }
}