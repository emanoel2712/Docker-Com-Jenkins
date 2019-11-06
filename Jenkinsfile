pipeline{
  agent{
    docker{
         image 'openjdk:11'
        args '-v /root/.m2:/root/.m2'
    }
  }
  options{
    skipStagesAfterUnstable()
  }
  stages{
    stage('Build'){
      steps{
        sh 'javac HelloWorld.java && java HelloWorld'

      }
    }
    
    stage('Results'){
      steps{
        script{
          def logz = currentBuild.rawBuild.getLog(1000);
          def result = logz.Find{it.contains('FAIL')
          if(Result){
            error('FAILING TO DUE' + result)    
          }
       }
    }
  }
} 
 
post {
        always {
            echo 'Jenkins - Email enviado apos o build'
          
            emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
          
        }
    }
  }
