pipeline {
   agent any
	stages {
      stage('Git Checkout') {
         steps {
            git 'https://github.com/sri008/mediclaim.git'
		}
	}
	stage('Build') {
		steps {
			withSonarQubeEnv('sonar') {
				sh '/opt/maven/bin/mvn clean verify sonar:sonar -Dmaven.test.skip=true'
			}
		}
	}
	/*stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
       
	stage ('Deploy') {
		steps {
			sh '/opt/maven/bin/mvn clean deploy -Dmaven.test.skip=true'
		}
	}
	stage ('Release') {
		steps {
			sh 'export JENKINS_NODE_COOKIE=dontkillme ;nohup java -jar $WORKSPACE/target/*.jar &'
		}
	}*/
		
	stage ('DB migration') {
		steps {
			sh label: '', script: '''/opt/maven/bin/mvn clean flyway:migrate
if [ $? -eq 0 ]; then slackSend color: \'good\', message: \'Message from Jenkins Pipeline\' else slackSend color: \'bad\', message: \'Message from Jenkins Pipeline failed\' '''
		}
	}
}
	

}
