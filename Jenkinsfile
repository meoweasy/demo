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

        stage('Test') {
            steps {
				bat 'FOR /F "tokens=*" %%i IN (\'docker ps -a -q\') DO docker stop %%i'
				bat 'docker rm "test_sspr"'
				bat 'docker run -d --name "test_sspr" meowweasy/demo:latest bash'
				bat 'docker exec "test_sspr" sh -c "dotnet vstest TestProject.dll"'
				bat 'docker stop "test_sspr"'
            }
        }

        stage("Push Image To Docker Hub") {
            steps {
                withCredentials() {
                    bat "docker login --username meowweasy --password www392002*"
                    bat 'docker push mlnrzm/sspr4:latest'
                }
            }
        }
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
