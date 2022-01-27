//# mypipiline
//this is my new jenkins project
pipeline{
agent any
environment{
    PATH = "/opt/maven3/bin:$PATH"
    }
    stages{
    stage("GITCheckout"){
         steps{
           git cedentialsId: 'myhome',git credentialsId: 'myhome', url:'https://github.com/remo106/mypipiline.git'
    }
    }
     //sshagent(['myhomex']) {
           stages("Maven Build"){
           steps{
              sh "mvn clean packages"
              sh "mv target/".war target/myhome.war"
             // some block
             }
}
     stages("myhomex.dev"){
          steps{
          sshagent(['myhomex']){
          sh """
          
        scp -o StricHosky Checking=no target/myhome.war ec2-user10.1.2.229:/home/ec2-user/apache-tomcat-9.0.58/webapps/
          ssh ec2-user@10.1.2.229:/home/ec2-user/apache-tomcat-9.0.58/bin/shutdown.sh
          ssh ec2-user@10.1.2.229:/home/ec2-user/apache-tomcat-9.0.58/bin/startup.sh
          
                 """
          }
        }
          }
           }
          }

                                                                                    
          
