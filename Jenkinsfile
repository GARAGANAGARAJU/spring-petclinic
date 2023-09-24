pipeline {
    agent {
        label 'dev'
    }
    environment {
        PATH = "opt/maven3/bin:$PATH"
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
                sh "mv target/*.war target/myweb.war"
            }
        }
        stage ("deploy-dev") {
            steps {
                sshagent(['tomcat-new']) {
                    sh """ 
                        scp -o stricthostkeychecking=no target/myweb.war ubuntu@172.31.7.242:/home/ubuntu/apache-tomcat-10.1.13/webapps/
                        ssh ubuntu@172.31.7.242 /home/ubuntu/apache-tomcat-10.1.13/bin/shutdown.sh
                        ssh ubuntu@172.31.7.242 /home/ubuntu/apache-tomcat-10.1.13/bin/startup.sh
                       """
                }
            }
        }
    
    }

}
