pipeline
{
    agent any
    environment
    {
        MAVEN_HOME = '/usr/share/maven/bin'
        scannerHome = tool 'SonarQubeScanner'
    }
    stages
    {
        stage('Compile')
        {
            steps
            {
             echo 'Compile Code ...'
             sh 'mvn clean compile -e'
            }
        }
        stage('Test')
        {
            steps
            {   
                echo 'Test Code ...'
                sh 'mvn clean test -e'
            }
        }
        stage('Jar')
        {
            steps
            {
                echo 'Jar Code ...'
                sh 'mvn clean package -e'
            }
        }
        stage('Run')
        {
            steps
            {
                echo 'Run Jar ...'
                sh 'nohup bash mvn spring-boot:run &'
            }
        }
        stage('Sonar')
        {
            steps
            {
                withSonarQubeEnv('Sonarqube') {
                sh 'mvn clean package sonar:sonar'
            }
        }
        stage('Build')
        {
            steps
            {
                git 'https://github.com/DonCarlosRiveros/ejemplo-maven.git'
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('TestApp')
        {
            steps
            {
                echo 'Testing Application ...'
                sh 'curl -X GET http://localhost:8081/rest/mscovid/test?msg=testing'
            }
        }
    }
