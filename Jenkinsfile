pipeline {
    agent {
        label 'windows'
    }
    environment {
        PATH = "opt/maven3/bin:$PATH"
    }
    stages {
        stage ("Git Checkout") {
            steps {
                git credentialsid:  'javahome2', url :  'https://github.com/GARAGANAGARAJU/spring-petclinic.git'
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
                        scp -o stricthostkeychecking=no target/myweb.war ec2-user@172.31.82.58:/home/ec2-user/apache-tomcat-10.0.23/webapps/
                        ssh ec2-user@172.31.82.58 /home/ec2-user/apache-tomcat-10.0.23/bin/shutdown.sh
                        ssh ec2-user@172.31.82.58 /home/ec2-user/apache-tomcat-10.0.23/bin/startup.sh
                       """
                }
            }
        }
    
    }

}
