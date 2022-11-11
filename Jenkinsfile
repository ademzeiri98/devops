pipeline {

        agent any
        stages {
                stage('Checkout Git'){
                   
                steps{
                        echo 'Pulling...';
                        git branch: 'jawhar',
                        url : 'https://github.com/ademzeiri98/devops.git';
                    }
                }
       
        stage(' maven test') {
            steps {
                sh """mvn -version"""
                 
            }
        }
       
        stage('Mvn Clean') {
            steps {
                sh 'mvn clean'
                 
            }
        }
        stage('Mvn Compile') {
            steps {
                sh 'mvn compile'
                 
            }
        }
         stage('SonarQube ') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=enajawher98'
            }
        }
        
        stage('Docker build')
        {
            steps {
                 sh 'docker build -t jawherbalti/devops  .'
            }
        }
        stage('Docker login')
        {
            steps {
                sh 'echo $dockerhub_PSW | docker login -u jawherbalti -p dckr_pat_JicCkO5pA_74j9UVigYMA_2UDLo'
            }    
       
        }
      stage('Push') {

			steps {
				sh 'docker push jawherbalti/devops'
			}
		}
		
		stage('NEXUS') {
            steps {
                sh 'mvn deploy -DskipTests -e'
                  
            }
        }
        
       stage('Run  DockerCompose') {
              steps {
                  sh "docker-compose -f docker-compose.yml up -d  "
              }
              }
        
       
       
    }
}