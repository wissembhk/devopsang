pipeline 
{
    agent any
    environment {
        EMAIL_TO = 'wissem22111@gmail.com'
        registry='wissembhk/angular'
        registryCredential=''
        dockerImage=''
    }
    post{
         failure {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                    to: "${EMAIL_TO}", 
                    subject: 'Build failed in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        
    }
   
    stages
    {
        stage('git clone front')
        {
            steps
            {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/wissembhk/devopsang']]])
            }
            
        }
        


         stage('building docker image')
        {
            steps
            {
                script
                {
                   // dockerImage=docker.build registry+":$BUILD_NUMBER"
                   sh 'docker build -t wissembhk/angular .'
                }
            }
        }
   
        
        stage('image up')
        {
            steps{
                sh 'docker-compose up -d'
            }
        }
       
       
        
        
    }
}

