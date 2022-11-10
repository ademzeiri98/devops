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
       
        stage('Testing maven') {
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
         stage('SonarQube analysis 1') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=enajawher98'
            }
        }
        stage('JUnit and Mockito Test'){
            steps{
                script
                {
                    if (isUnix())
                    {
                        sh 'mvn --batch-mode test'
                    }
                    else
                    {
                        bat 'mvn --batch-mode test'
                    }
                }
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
                sh 'echo $dockerhub_PSW | docker login -u jawherbalti -p dckr_pat_SQnD7G_8ehc8XlRnvF8ztfA_JMo'
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
        
       stage('Run app With DockerCompose') {
              steps {
                  sh "docker-compose -f docker-compose.yml up -d  "
              }
              }
        
       
       
    }
}