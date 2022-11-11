pipeline {

        agent any
        stages {
                stage('Checkout Git'){
                   
                steps{
                        echo 'Pulling...';
                        git branch: 'adem',
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
                sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=adem'
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
                 sh 'docker build -t adem011/devops  .'
            }
        }
        stage('Docker login')
        {
            steps {
                sh 'echo $dockerhub_PSW | docker login -u adem011 -p dckr_pat_1mAPIqQXEooRkqKnA-GDGxdiOOI'
            }    
       
        }
      stage('Push') {

			steps {
				sh 'docker push adem011/devops  '
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