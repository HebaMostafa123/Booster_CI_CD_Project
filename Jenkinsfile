pipeline {
    agent any
        stage('CI') {
            steps {
                // Get some code from a GitHub repository
                withCredentials([usernamePassword(credentialsId:"docker",usernameVariable:"username",passwordVariable:"pass")]){
                sh 'docker build . -t ${username}/jenkins:lts'
                sh 'docker login -u ${username} -p ${pass}'
                sh 'docker push ${username}/jenkins:lts'
                }
            }
        }  
        stage ('CD'){
            steps{
                withCredentials([usernamePassword(credentialsId:"test",usernameVariable:"username",passwordVariable:"pass")]){
                
                sh 'docker run -d -p 3000:3000 -d ${username}/jenkins:lts'
                }
            }
            
        }
    }
}
