node {

  // Get Code from Github
  stage('Preparation') {
    git 'https://github.com/itstayyab/SpringMVCHibernate2.git'
  }
  
  // Build the Code using mvn  
  stage('Build') {
    // Run maven build unix
    if (isUnix()) {
      sh "mvn clean package"
    } 
    // Run maven build on windows
    else {
      bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
    }
  }
  
  stage('Results') {
    archiveArtifacts 'target/*.war'
  }

  stage('Deploy Containers') {
    sh 'if [ `/usr/local/bin/docker-compose ps | grep -i "UP" | wc -l` -ge 1 ]; then /usr/local/bin/docker-compose stop -t 10 app; /usr/local/bin/docker-compose start app; else /usr/local/bin/docker-compose up -d; fi;'
  }

}