pipeline {

  environment {
    imagename = "rapiscan/iam-server"
    registryCredential = 'docker'
    appTest = ''
    app = '' 
    // tag_regex = "^v([0-9]+)\.([0-9]+)\.([0-9]+)(?:-([0-9]+(?:\.[0-9-]+)*))?(?:\+[0-9]+)?$"
  }

  agent any
  
  stages {
 
    stage('Build Test Image') {
      steps {
        sh 'echo "Build test image"'
        // script {
        //   appTest = docker.build('iam-server-test', '-f ${WORKSPACE}/Dockerfile.dev ${WORKSPACE}')
        // }       
      }
    }
    
    stage('Test'){
      steps {
        sh 'echo "testing..."'
        // script {
        //   appTest.inside {
        //     sh 'yarn install --production=false'
        //     sh 'yarn test'
        //   }
        // }
      }
    }
    
    stage('Build App Image') {
      when { 
        tag pattern: "^v([0-9]+)\.([0-9]+)\.([0-9]+)(?:-([0-9]+(?:\.[0-9-]+)*))?(?:\+[0-9]+)?$", comparator: "REGEXP" 
        anyOf { branch 'main'; branch 'dev' } 
        }
      steps {
        sh 'echo "build app image..."'
        // script {
        //   app = docker.build(imagename)
        // }       
      }
    }
    
    stage('Publish App Image'){
      when { 
        tag pattern: "^v([0-9]+)\.([0-9]+)\.([0-9]+)(?:-([0-9]+(?:\.[0-9-]+)*))?(?:\+[0-9]+)?$", comparator: "REGEXP" 
        anyOf { branch 'main'; branch 'dev' } 
        }
      steps {
        sh 'echo "publishing..."'
        // script {
        //   docker.withRegistry( '', registryCredential ) {
        //     app.push("$BUILD_NUMBER")
        //     app.push('latest')
        //   }
        // }
      }
    }
    
  }
}
