pipeline {
  agent any
  stages {
    stage('build start') {
      steps {
        sh 'echo "build start"'
      }
    }

    stage('test') {
      steps {
        jacoco(buildOverBuild: true)
      }
    }

    stage('artifacts') {
      steps {
        archiveArtifacts './war'
      }
    }

    stage('dockerbuild') {
      steps {
        sh '''echo "from centos" > Dockerfile
echo "run yum install httpd -y" >> Dockerfile

docker build -t testbuild .'''
      }
    }

    stage('deployment') {
      steps {
        sh 'docker run -itd -p 99:80 --name testbuild1 testbuild '
      }
    }

  }
}