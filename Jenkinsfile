pipeline {
  agent any
  options {
    disableConcurrentBuilds()
    timeout(time: 1, unit: 'HOURS')
    disableResume()
  }
  triggers {
    cron('H */4 * * 1-5')
  }

  parameters {
    string(name: 'STRING_VARIABLE', defaultValue: 'TestTrainer', description: 'Who should I say hello to?')
    text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
    booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
    choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
  }
  environment {
    def name = "my name"
    def pwdv = ""
  }
  stages {
    stage('Clean Workspace') {
      steps {
        cleanWs()
      }
    }
    stage('Validate') {
      /*  when {
          branch 'master'
        }*/
      steps {
        script {
          if ("${STRING_VARIABLE}" == "TestTrainer") {
            error 'Triggered error'
          } else {
            echo "The input was different from TestTrainer so proceeding"
          }
        }
      }
    }
    stage('GIt Clone Branch') {
      steps {
        git branch: 'main', url: 'https://github.com/Arvind9719/hello-world.git'
        dir('MOVE') {
          sh("touch test.txt")
          sh("cat test")
          readFile 'test'
        }
      }
    }
    stage('Gmkdir') {
      steps {
        sh "mkdir -p abc/ghi/xyz"
        // timeout(time: 10, unit: 'SECONDS') {
        //     sleep 20
        // }
      }
    }
    stage('Hello') {
      steps {
        dir('abc') {
          dir('ghi') {
            dir('xyz') {
              sh("touch fffffff.txt")
            }
          }
        }
        dir('abc/ghi/xyz') {
          sh("touch ttttttttttt.txt")
        }
        echo 'Hello World'
        dir('abc/ghi') {
          deleteDir()
        }
        timestamps {
          echo "asdasd"
        }
      }
    }
    stage('Trainer') {
      steps {
        script {
          sh("echo ${STRING_VARIABLE}")
        }
      }
    }
    stage('Variable Initialization') {
      steps {
        script {
          sh("echo ${name}")
          writeFile file: 'test-write-file', text: 'asdasdasdasdasd'
        }
      }
    }

    stage('Confirm button') {
      steps {
        input 'Please confirm'
        checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/shetdeekshitha/jenk.git']])
        sh("echo asdasdasd")
      }
    }

    stage('Child Jobs') {
      steps {
        build quietPeriod: 6, wait: true, job: 'job1'
        build quietPeriod: 6, wait: true, job: 'job1'
        build quietPeriod: 6, wait: false, job: 'job2'
        build quietPeriod: 6, wait: false, job: 'job2'
        build quietPeriod: 6, wait: false, job: 'job1'
      }
    }
    stage('Loop') {
      steps {
        echo 'Hello World'

        script {
          def browsers = ['chrome', 'firefox']
          for (int i = 0; i < browsers.size(); ++i) {
            echo "Testing the ${browsers[i]} browser"
          }
        }
      }
    }
    stage('Parallel Stage') {
      // when { branch 'master' }
      failFast true
      parallel {
        stage('Branch A') {
          /*agent {
              label "master"
          }*/
          steps {
            echo "On Branch A"
          }
        }
        stage('Branch B') {
          /* agent {
               label "master"
           }*/
          steps {
            echo "On Branch B"
          }
        }
      }
    }
  }
}
