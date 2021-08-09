def podTemplate = """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: maven
    image: maven:3.8.1-jdk-8
    command:
    - sleep
    args:
    - infinity
    securityContext:
      fsGroup: 1000
      runAsGroup: 1000
      runAsUser: 1000
"""


pipeline {
    agent none
    stages {
        stage ('maven') {
            agent { 
                kubernetes {
                    yaml podTemplate 
                    defaultContainer 'maven'
	            podRetention always()
                 } 
            }
            stages {
                stage('Nested 1') {                  
                    steps {
                        sh "touch Nested1 && mvn -version"
                    }
                }
                stage('Nested 2') {                  
                    steps {
                        sh "mvn -version 2 && touch Nested2 "
                    }
                }
            }
        }
    }
}
