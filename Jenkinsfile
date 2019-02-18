pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
  
            stage('List root files') {
         steps {
         sh 'ls -lah'
         sh 'pwd'
        }
  }
     
    stage('Download Shiftleft') {
         steps {
         sh 'curl https://www.shiftleft.io/download/sl-latest-linux-x64.tar.gz | tar xvz -C /usr/local/bin'
        }
  }
    stage('RunShiftLeft') {
         steps {
         sh '/usr/local/bin/sl auth --org "bbb8d600-1752-4dd6-9716-1627650a9034" --token "eyJhbGciOiJSUzUxMiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1ODEwOTE0OTcsImlzcyI6IlNoaWZ0TGVmdCIsIm9yZ0lEIjoiYmJiOGQ2MDAtMTc1Mi00ZGQ2LTk3MTYtMTYyNzY1MGE5MDM0Iiwic2NvcGVzIjpbImFwaTp2MiIsInVwbG9hZHM6d3JpdGUiLCJsb2c6d3JpdGUiLCJwaXBlbGluZXN0YXR1czpyZWFkIiwibG9nOndyaXRlIiwicG9saWNpZXM6cmVhZCJdfQ.A7phmbwIHWog-YpfiRat74lHoKllCeCw0CHph93Z9bJt8M_Yjnq0G5y04B4VNH8nk-DN0JJ1ZszmxE6JNSWKjIgGjKto7JCP_Ev7UI2qydfv0dOPZyyp6d6eLoN08RA6c9ey56nfX9O2p3GIADf08C2PyhUool2HGQxWsIz-Avon8vWF8sGkgpr4wbExzJkgv3ZL8iFdCZTOSUWNjcpUnN6fguHD0o7coEke1iNCDSm7PBqOk7Qza3hqJNkf-tGNZSZuqtmSZ6w0lnvtnEms9dO_0N_vPbYov1E8fxzQGJpCZavMOBCxH_tZcpue8j0MAcUgNNjBlHYaBx7fIaaG0A"'
        }
  }
    stage('Test') {
         steps {
         sh 'mvn test'
        }
    post {
          always {
          junit 'target/surefire-reports/*.xml'
                }
            }
        }
     stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}

