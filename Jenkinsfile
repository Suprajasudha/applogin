pipeline {
    agent {label "my-agent"}
    stages {
        stage ("git clone") {
            steps {
                git url: 'https://github.com/tejesh555/applogin.git'
            }
        }
        stage ("build") {
            steps {
                sh "mvn clean install"
            }
        }
        stage ("test") {
            steps {
                println "test"
            }
        }
        stage ("publish") {
            steps {
                script {
                    rtUpload (
                        serverId: 'my-jfrog',
                        spec: '''
                            {
                                "files": [
                                    {
                                        "pattern": "target/*.war",
                                        "target": "applogin"
                                    }
                                ]
                            }
                        ''',
                        buildName: "${JOB_NAME}",
                        buildNumber: "${BUILD_NUMBER}"
                    )
                }
            }
        }
    }
}

