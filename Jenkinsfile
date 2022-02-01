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

sh 'echo compile completed'

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

stage('package') {

steps {

sh 'mvn package'

}

}

stage('Unit test') {

steps {

sh 'mvn test'

}

}
stage('Deployment') {

steps {

sh 'cp /root/.jenkins/workspace/done/target/*.war /opt/tomcat/webapps'

}

}

stage('installing webapp') {

steps {

sh '/opt/tomcat/bin/startup.sh'

}

}


}

}
