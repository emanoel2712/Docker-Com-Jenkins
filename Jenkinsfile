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
