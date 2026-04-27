node('built-in') 
{
    stage('Continuous Download') {

        git branch: 'main', url: 'https://github.com/RamNaresh-java/Maven.git'

    try 
    {
        sh 'mvn package'
    } catch(Exception e)
    {
        echo "Build is failed now"
        //Email Notification
        mail bcc: '', body: 'CI CD and CD failed', cc: 'rama.ayanavilli@gmail.com', from: '', replyTo: '', subject: 'CI CD Process', to: 'naresh.ayanavilli@gmail.com'
        exit(1)
    }
      //  git branch: 'main', url: 'https://github.com/RamNaresh-java/Maven.git'
    }
    
    //stage('Continuous Build') {
    //    sh 'mvn package'
    //}
    
    stage('Continuous Delivery') {
         deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat9', path: '', url: 'http://172.31.74.194:8080')], contextPath: 'testingapp', war: '**/*.war'
    }

    stage('Continuous Testing') {
         git branch: 'main', url: 'https://github.com/RamNaresh-java/Functional-Testing.git'

         sh 'java -jar /var/lib/jenkins/workspace/Declarative-pipeline/testing.jar'
    }

    stage('Continuous Deploy') {
         deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcatprod', path: '', url: 'http://172.31.66.18:8080')], contextPath: 'prodapp', war: '**/*.war'
     }
}