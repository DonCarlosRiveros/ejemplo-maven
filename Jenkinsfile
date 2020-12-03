pipeline
{
    agent any
    environment
    {
        MAVEN_HOME = '/usr/share/maven/bin'
    }
    stages
    {
        stage('Compile')
        {
            steps
            {
             echo 'Compile Code ...'
             sh './mvnw clean compile -e'
            }
        }
        stage('Test')
        {
            steps
            {   
                echo 'Test Code ...'
                sh './mvnw clean test -e'
            }
        }
        stage('Jar')
        {
            steps
            {
                echo 'Jar Code ...'
                sh './mvnw clean package -e'
            }
        }
        stage('Run')
        {
            steps
            {
                echo 'Run Jar ...'
                sh 'nohup bash mvnw spring-boot:run &'
            }
        }
        stage('Sonar')
        {
            environment
            {
                 scannerHome = tool 'SonarQubeScanner'
            }
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
                // Get some code from a GitHub repository
                git 'https://github.com/DonCarlosRiveros/ejemplo-maven.git'

                // Run Maven on a Unix agent.
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
 }
