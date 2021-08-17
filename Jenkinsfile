pipeline {
    agent any
    stages {
        stage('Git-Check') {
            steps {
                    echo "Checking out from git repo!!";
                    git credentialsId: 'd92d3647-1b11-4827-a545-68e89ccfa8c5', url: 'https://github.com/wm2008/Pipeline_Script.git'
            }
        }

        stage('Build') {
            steps {
                echo "Build the CheckOut project !";
                sh "chmod +x -R ${env.WORKSPACE}";
                sh './Build.sh'
                
            }
        }
        stage ('Unit-Test') {
            steps {
                echo " Running Junit tests!!";
                sh "chmod +x -R ${env.WORKSPACE}";
                sh './Unit.sh'

            }
        }   

        stage ('Quality-Gate') {
            steps {
                echo "Verifying Quality Gates!";
                sh "chmod +x -R ${env.WORKSPACE}";
                sh './Quality.sh'

            }
        }
        
        stage ('Deploy') {
            steps {
                echo "Deploying to Stage Env for More testes!";
                sh "chmod +x -R ${env.WORKSPACE}";
                sh './Deploy.sh'

            }
        }
        
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Popeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now Successful'
        }
    }
}
