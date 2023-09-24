pipeline {
    agent {
        label 'dev'
    }
    environment {
        PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
    }
    stages {
        stage ("Git Checkout") {
            steps {
               git branch: 'main', url: 'https://github.com/GARAGANAGARAJU/spring-petclinic.git'
            }
        }
        stage ("Maven Build") {
            steps {
                sh "mvn clean package"
                sh "mv target/*.spring-petclinic-2.6.0-SNAPSHOT.jar target/spring-petclinic-2.6.0-SNAPSHOT.jar"
            }
        }
        stage ("deploy-dev") {
            steps {
                sshagent(['tomcat-new']) {
                    sh """ 
                        scp -o stricthostkeychecking=no target/spring-petclinic-2.6.0-SNAPSHOT.jar ubuntu@172.31.7.242:/home/ubuntu/apache-tomcat-10.1.13/webapps/
                        ssh ubuntu@172.31.7.242 /home/ubuntu/apache-tomcat-10.1.13/bin/shutdown.sh
                        ssh ubuntu@172.31.7.242 /home/ubuntu/apache-tomcat-10.1.13/bin/startup.sh
                       """
                }
            }
        }
    
    }

}
