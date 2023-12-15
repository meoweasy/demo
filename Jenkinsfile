pipeline {
    agent any
    
    stages {
        stage('Cloning Git') {
          steps {
              git([url: 'https://github.com/mlnrzm/sspr-lab4.git', branch: 'master'])
          }
        }
        stage('Build') {

			steps {
				bat 'docker build -t meowweasy/demo:latest .'
			}
		}

//         stage("Push Image To Docker Hub") {
//             steps {
//                 withCredentials([string(credentialsId: 'www392002*', variable: 'sspr4')]) {
//                     bat "docker login --username meowweasy --password ${sspr4}"
//                     bat 'docker push meowweasy/demo:latest'
//                 }
//             }
//         }
    }
    post {
		always {
			script {
				node {
					bat 'docker logout'
				}
            }
		}
	}
}
