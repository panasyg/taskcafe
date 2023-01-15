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
        sh 'go test ./...'
        } 
    }

    stage("build") 
    {
        echo 'BUILD EXECUTION STARTED'
        sh 'go version'
        sh 'go get ./...'
        sh 'go run cmd/mage/main.go install'
        sh 'go run cmd/mage/main.go build'
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