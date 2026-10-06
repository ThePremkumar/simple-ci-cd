pipeline{

    agent any
    stages{
        stage("Check out SCM"){
            steps{
                checkout scm
            }
        }
        stage("Build the application"){
            steps{
                sh 'docker build -t my-index-site .'
            }
        }
        stage("Testing"){
            steps{
                sh '''
                    docker run -d -p 80:80 --name text-index my-index-site 
                    sleep 3
                    curl -f http://localhost:80
                '''
            }
        }
        stage("Package"){
            steps{
                echo "Packaging complete!"
            }
        }
    }

    post {
        always{
            sh 'docker rm -f test-index  || true'
        }
    }
}