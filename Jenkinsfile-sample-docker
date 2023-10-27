pipeline{
    agent any
    stages {
            stage('git-clone') {
                agent {
                    node {
                        label 'built-in'
                        customWorkspace '/root/demo'
                    }
                }
                    steps {
                        sh " rm -rf * "
                        sh " yum install git -y "
                        sh " git clone https://github.com/ashrayp18/sample-project1.git"
                    }
            }
            stage('git-clone-branches') {
                agent {
                    node {
                        label 'built-in'
                        customWorkspace '/root/demo'
                    }
                }
                    steps {
                     dir('/root/demo/branch1'){
                      sh " git clone --branch 22Q1 https://github.com/ashrayp18/sample-project1.git"
                     }
                    dir('/root/demo/branch2'){
                      sh " git clone --branch 22Q2 https://github.com/ashrayp18/sample-project1.git"
                     }
                      dir('/root/demo/branch3'){
                      sh " git clone --branch 22Q3 https://github.com/ashrayp18/sample-project1.git"
                     }
                    }
            }
            stage('docker-container-create') {
                steps{
                    sh " docker rm -f ashray1"
                    sh "sudo docker run -itdp 80:80 --name ashray1 httpd"
                    sh 'chmod 644 /root/demo/branch1/sample-project1/index.html'
                    sh " sudo docker cp /root/demo/branch1/sample-project1/index.html  ashray1:/usr/local/apache2/htdocs/"
                    
                    sh " docker rm -f ashray2"
                    sh "docker run -itdp 90:80 --name ashray2 httpd"
                    sh 'chmod 644 /root/demo/branch2/sample-project1/index.html'
                    sh " docker cp /root/demo/branch2/sample-project1/index.html  ashray2:/usr/local/apache2/htdocs/"
                    
                    sh " docker rm -f ashray3"
                    sh "docker run -itdp 100:80 --name ashray3 httpd"
                    sh 'chmod 644 /root/demo/branch3/sample-project1/index.html'
                    sh " docker cp /root/demo/branch3/sample-project1/index.html  ashray3:/usr/local/apache2/htdocs/"
                    
                }
               
                    }
            }
    }
    
