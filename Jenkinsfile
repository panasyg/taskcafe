node("tc_agent") {
    def app
    def root = tool type: 'go', name: '1.15.1'
    withEnv(["GOROOT=${root}", "PATH+GO=${root}/bin"]) {
        // Output will be something like "go version go1.19 darwin/arm64"
        sh 'go version'
    }

    stage('clone repository') {   checkout scm   }

    
    stage('unit tests') 
    {
       withEnv(["GOROOT=${root}", "PATH+GO=${root}/bin"]) {
        sh 'go version'
        } 
    }

    stage('Pre-build') 
    {
        sh "sudo yum install curl -y"
        sh "curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash " 
        sh "source ~/.bashrc"
        sh "chmod u+x ~/.nvm/nvm.sh"
        sh "~/.nvm/nvm.sh"
        sh "chmod u+x ~/.bashrc"
        sh "sudo ~/.bashrc"
        sh "~/.nvm/nvm.sh install 14.9.0"
        sh "~/.nvm/nvm.sh use 14.9.0"
        sh "npm install -g yarn"
    }

    stage("build") 
    {
        withEnv(["GOROOT=${root}", "PATH+GO=${root}/bin"]) {
        sh 'go version'
        echo 'BUILD EXECUTION STARTED'
        sh 'go version'
        sh 'go run cmd/mage/main.go install'
        sh 'go run cmd/mage/main.go build'
        } 
        
    }


    // stage('deploy') {
    //     sh "ssh jenkins@10.26.0.57 rm -rf /home/jenkins/gogs/gogs"
    //     sh "scp gogs jenkins@10.26.0.57:/home/jenkins/gogs/gogs"
    //     sh 'ssh jenkins@10.26.0.57 /home/jenkins/gogs/gogs web > /dev/null 2>&1 & '

    //     sh "ssh jenkins@10.26.0.71 rm -rf /home/jenkins/gogs/gogs"
    //     sh "scp gogs jenkins@10.26.0.71:/home/jenkins/gogs/gogs"
    //     sh 'ssh jenkins@10.26.0.71 /home/jenkins/gogs/gogs web > /dev/null 2>&1 & '
    //     }
    }