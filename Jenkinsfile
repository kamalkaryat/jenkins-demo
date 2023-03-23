def remote = [:]
remote.name = 'test'
remote.host = '65.0.12.63'			//EC2-PublicIP
remote.port = 22
remote.allowAnyHosts = true
pipeline {
    agent any
     stages {
        stage('Git Clone') {
            steps {
                // Get some code from a GitHub repository. 
		        // githubcreds: arbitary_name given while adding github credentials in jenkins
                git branch: 'main', credentialsId: 'githubcreds', url: 'https://github.com/kamalkaryat/jenkins-demo'
            }
        }
     stage('Deployment'){
        steps {
            script {
             // move the new changed 
             sh 'ls'
	         //	ubuntucred: arbitary_name given while adding vm/cloud-vm credentials in jenkins
             withCredentials([usernamePassword(credentialsId: 'instance-user-creds', passwordVariable: 'pass', usernameVariable: 'user')]) {
             remote.user = user
             remote.password = pass
             sshPut remote: remote, from: "index.html", into: "/var/www/html"
             sshCommand remote: remote, command: "ls /var/www/html"
             }
           }
          }
        }
      }
    }