pipeline{
    agent{label 'prod'}
    stages{
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/chia5/Hello_Python_App.git'
            }
        }
        
        stage('Build'){
            steps{
                app = docker.build('chash07/helloapp')
            }
        }
        
        stage('Test Image'){
            steps{
                echo "Test Successfull"
        
            }        
        }
        
        stage('Push Image'){
            steps{
                docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                    app.push('${env.BUILD_NUMBER}')
                }
            }
        }
        
        stage('Trigger ManifestUpdate'){
            steps{
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
            }
        }
    }
}
