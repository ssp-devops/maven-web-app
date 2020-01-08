node {

  stage('Checkout SCM') {
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'adsspgithub', url: 'https://github.com/ssp-devops/maven-web-app.git']]])    
  }
  stage('Package') {
    sh "/usr/local/src/apache-maven/bin/mvn package"
  }
  stage('Deploy War file') {
      //sh "cd $WORKSPACE/target"
      sh "cp $WORKSPACE/target/*.war /opt/apache-tomcat-9.0.30/webapps/ssp-webapps-${BUILD_NUMBER}.war"
  }
stage('Notify') {
  slackSend channel: 'jenkins-notify', color: 'good', message: "Success ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", teamDomain: 'sspcloudpro', tokenCredentialId: 'sspcloudslacktoken', username: 'jenkins'
}
}

