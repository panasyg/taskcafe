node("tc_ag") {
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

    // stage("build") 
    // {
    //     withEnv(["GOROOT=${root}", "PATH+GO=${root}/bin"]) {
       
    //     sh 'go version'
    //     echo 'BUILD EXECUTION STARTED'
    //     sh 'go version' 
    //     env.PATH="${env.NODEJS_HOME}/bin:${env.PATH}"
    //     sh 'go run cmd/mage/main.go install'
    //     sh 'go run cmd/mage/main.go build'
    //     } 
        
    // }

    stage('deploy') {
        sh "ssh  root@10.26.0.125 ps aux |grep taskcafe | awk {print \$2/} | xargs kill 2>/dev/null"
        sh "ssh  root@10.26.0.125 rm -rf /dist/taskcafe"
        sh "scp  /var/lib/jenkins/workspace/tc_piln/dist/taskcafe root@10.26.0.77:/dist/"
        sh 'ssh  root@10.26.0.125 /dist/taskcafe web --config /dist/cfg.toml > /dev/null 2>&1 & '

        sh "ssh  root@10.26.0.77 ps aux |grep taskcafe | awk {print \$2/} | xargs kill 2>/dev/null"
        sh "ssh  root@10.26.0.77 rm -rf /dist/taskcafe"
        sh "scp  /var/lib/jenkins/workspace/tc_piln/dist/taskcafe root@10.26.0.77:/dist/"
        sh 'ssh  root@10.26.0.77 /dist/taskcafe web --config /dist/cfg.toml > /dev/null 2>&1 & '
        }
    }
