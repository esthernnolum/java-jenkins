pipeline {
    agent any
    environment {
        APP = "simple-webapp"
    }
    tools {
       // tools already available on the jenkins server and added to global tools
        maven 'mvn339'
        jdk 'jdk17'
    }
    stages {
        stage ('Initialize') {
            steps {
                deleteDir()
            }   
        }
        stage ('Clean WorkSpace') {
            steps {
                checkout scm
            }  
        }
        stage ('Build') {
            steps {
                script {
                            env.OLD_VERSION = sh(returnStdout: true, script: 'mvn help:evaluate -Dexpression=project.version -q -DforceStdout')
                            env.VERSION = env.OLD_VERSION + '-' + env.BUILD_NUMBER
                        }
                sh 'mvn clean package'
                echo 'Running build automation'
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
                  }
               }
        
        stage('SonarCloud analysis') {
                tools {
                    jdk 'jdk17' 
                }
                
            steps {
                withSonarQubeEnv('SonarCloud') {
                    sh 'mvn sonar:sonar ' + 
                    '-Dproject.settings=./sonar-project.properties'
                    }
                }
            }
        
        stage("deploy") {
                steps {
                    build job: 'simple-webapp-deploy',
                        parameters: [
                            string(name: 'ENVIRONMENT', value: 'test'),
                            string(name: 'JENKINS_JOB', value: 'simple-webapp'),
                            string(name: 'INSTANCE', value: 'test-service'),
                            string(name: 'CURRENT_COMPONENT', value: 'test-service'),
                            string(name: 'SERVICE', value: 'tagging-service')
                        ]
                }
            }
        
        }
}
