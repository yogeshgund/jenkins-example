pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/yogeshgund/jenkins-example/'
        }
  }
    {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn install'
                }
            }
        }

         stage ('deploy to tomcat') {
             steps {
                 sshagent(['c4314358-27ee-4704-859a-44ddcb0fc88b']) {
                 sh 'scp -o StrictHostKeyChecking=no target/*.jar ec2-user@172.31.21.148:/var/lib/tomcat/webapps/'
      }
             }
   }
}
}
