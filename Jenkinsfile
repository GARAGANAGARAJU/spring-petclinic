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
                        scp -o stricthostkeychecking=no target/myweb.war ec2-user@172.31.82.58:/home/ec2-user/apache-tomcat-10.0.23/webapps/
                        ssh ec2-user@172.31.82.58 /home/ec2-user/apache-tomcat-10.0.23/bin/shutdown.sh
                        ssh ec2-user@172.31.82.58 /home/ec2-user/apache-tomcat-10.0.23/bin/startup.sh
                       """
                }
            }
        }
}
}


    
        


