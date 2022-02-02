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
  
stage('SonarQube analysis') {

def scannerHome = tool 'sonar';

withSonarQubeEnv('my_sonar') {

sh "${scannerHome}/bin/sonar-scanner \
-D sonar.login=admin \
-D sonar.password=admin \
-D sonar.projectKey=test \
-D sonar.exclusions=vendor/**,resources/**,**/*.java \
-D sonar.host.url=http://172.31.9.9:9000/"

}

}
  



  stage('creating war file') {

steps {

sh 'cp /root/.jenkins/workspace/mmsonartest/target/*.war /opt/tomcat/webapps'

}

}


}

}
