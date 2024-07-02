pipeline
{
    agent any
    stages
    {
        stage('continousdownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('continousbuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('continousdeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'd7a36fdc-d7a4-45b1-8619-b77c1746e910', path: '', url: 'http://172.31.27.224:8080')], contextPath: 'myapp', war: '**/*.war'
            }
        }
        stage('continoustesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/pipeline02/testing.jar'
            }
        }
        stage('continousdelivery')
        {
            steps
            {
                input message: 'Need approval', submitter: 'user1'
                deploy adapters: [tomcat9(credentialsId: '2601629e-63f9-4cf3-ac26-ff1ce5ebd6e0', path: '', url: 'http://172.31.18.198:8080')], contextPath: 'myprodapp', war: '**/*.war'
            }
        }
        
    }
}
