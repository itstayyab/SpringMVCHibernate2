node {
   stage('Preparation') { 
      // Get some code from a GitHub repository
      git 'https://github.com/itstayyab/SpringMVCHibernate2.git'
      // Get the Maven tool.
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "mvn clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      archive 'target/*.jar'
   }
   
   stage('Copy Artifacts') {
       sh 'rm /vagrant/docker/java_app/conf/app/SpringMVCHibernate.war'
       sh 'cp "/var/lib/jenkins/workspace/SpringMVCHibernate Pipeline/target/SpringMVCHibernate.war" /vagrant/docker/java_app/conf/app/SpringMVCHibernate.war'
   }
   
   stage('Start Container') {
       sh 'cd /vagrant/docker/java_app; if [ `docker-compose ps | grep -i "UP" | wc -l` -ge 1 ]; then docker-compose stop -t 10 app; docker-compose start app; else docker-compose up -d; fi;'
   }

}