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
            }
        }
   stage ("deploy-devv") {
            steps {
                sshagent(['ubuntu']) {
                    sh """ 
                        scp -o stricthostkeychecking=no target/spring-petclinic-2.6.0-SNAPSHOT.jar ubuntu@3.16.68.70:/home/ubuntu/apache-tomcat-10.1.13/webapps/
                        ssh ubuntu@3.16.68.70 /home/ubuntu/apache-tomcat-10.1.13/bin/shutdown.sh
                        ssh ubuntu@3.16.68.70 /home/ubuntu/apache-tomcat-10.1.13/bin/startup.sh
                       """
                }
            }
        }
}
}


    
        


