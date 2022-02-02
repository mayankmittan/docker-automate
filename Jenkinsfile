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
stage ('Test') {
steps {
sh 'cd /root/.jenkins/workspace/mmsonartest/ && touch test-results-unit.xml'
sh 'mvn test'
}
post {
always {
junit '**/test-results-unit.xml'
}
}
}
  



stage('creating war file')

steps {

sh 'cp /root/.jenkins/workspace/mmsonartest/target/*.war /opt/tomcat/webapps'

}

}


}

}
