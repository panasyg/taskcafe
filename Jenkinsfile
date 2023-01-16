node("tc_agent") {
    def app
    def root = tool type: 'go', name: '1.15.1'
    withEnv(["GOROOT=${root}", "PATH+GO=${root}/bin"]) {
        sh 'go version'
    }
    env.NODEJS_HOME = "${tool 'node14.9.0'}"
        env.PATH="${env.NODEJS_HOME}/bin:${env.PATH}"
        sh 'npm --version'
        sh 'npm install -g yarn'
        sh 'yarn install'

    stage('clone repository') {   checkout scm   }
   
    stage('unit tests') 
    {
       withEnv(["GOROOT=${root}", "PATH+GO=${root}/bin"]) {
        sh 'go version'
        } 
    }

    stage("build") 
    {
        withEnv(["GOROOT=${root}", "PATH+GO=${root}/bin"]) {
       
        sh 'go version'
        echo 'BUILD EXECUTION STARTED'
        sh 'go version' 
        env.PATH="${env.NODEJS_HOME}/bin:${env.PATH}"
        sh 'go run cmd/mage/main.go install'
        sh 'go run cmd/mage/main.go build'
        } 
        
    }

    stage('deploy') {
        sh "ssh root@10.26.0.125 rm -rf /dist/taskcafe"
        sh "scp /var jenkins@10.26.0.57:/home/jenkins/gogs/gogs"
        sh 'ssh jenkins@10.26.0.57 /home/jenkins/gogs/gogs web > /dev/null 2>&1 & '

        sh "ssh root@10.26.0.77 rm -rf /dist/taskcafe"
        sh "scp gogs jenkins@10.26.0.71:/home/jenkins/gogs/gogs"
        sh 'ssh jenkins@10.26.0.71 /home/jenkins/gogs/gogs web > /dev/null 2>&1 & '
        }
    }