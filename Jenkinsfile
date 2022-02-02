pipeline {

agent any

tools {

maven 'my_maven'

}

stages {

stage('Git Checkout') {

steps {

git branch: 'main',

credentialsId:'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',

url: 'https://github.com/mittanmayank/sonartest.git'

sh 'echo Git Checkout complete'

}

}

stage('compile') {

steps {

sh 'mvn clean install'


}

}
  
stage('package') {

steps {

sh 'mvn package'

}

}
  
stage('install') {

steps {

sh 'mvn install'

}

}
  
stage('Sonar Analysis') {
environment {
SCANNER_HOME = tool 'sonar'
PROJECT_NAME = "test"
}
steps {
withSonarQubeEnv('my_sonar') {
sh '''$SCANNER_HOME/bin/sonar-scanner \
-Dsonar.java.binaries=build/classes/java/ \
-Dsonar.projectKey=$PROJECT_NAME \
-Dsonar.sources=.'''
}
}
}
  
stage('Quality Gate') {
steps {
timeout(time: 1, unit: 'MINUTES') {
waitForQualityGate abortPipeline:true
}
}
}

  



  stage('creating war file') {

steps {

sh 'cp /root/.jenkins/workspace/mmsonartest/target/*.war /opt/tomcat/webapps'

}

}


}

}
