pipeline {
    agent { label 'any' }
    triggers { pollSCM('* * * * *') }
    stages {
        stage('vcs') {
            steps {
                git branch: 'develop',
                    url: 'https://github.com/DevProjectsForDevOps/StudentCoursesRestAPI.git'
            }
        }
        stage('build and deploy') {
            steps {
                sh "docker image build -t qdevops.jfrog.io/docker/courses:develop-$env.BUILD_ID ."
                sh "docker image push qdevops.jfrog.io/docker/courses:develop-$env.BUILD_ID"
            }
        }
        /*stage('deploy') {
            steps {
                sh "cd deployments/courses/overlays/develop && kustomize edit set image courses=qdevops.jfrog.io/docker/courses:develop-$env.BUILD_ID"
                sh 'kubectl apply -k deployments/courses/overlays/develop'
            }
        }*/

    }
}