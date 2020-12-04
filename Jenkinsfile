2e8a2291994768467cb0f966b1c3c44813a5e076


pipeline
{
    agent any
    environment
    {
        MAVEN_HOME = '/usr/share/maven/bin'
        scannerHome = tool 'Sonarqube'
    }
    stages
    {
        stage('Compile')
        {
            steps
            {
                echo 'Compile Code ...'
                sh '$MAVEN_HOME/mvn clean compile -e'
            }
        }
        stage('Test')
        {
            steps
            {   
                echo 'Test Code ...'
                sh '$MAVEN_HOME/mvn clean test -e'
            }
        }
        stage('Jar')
        {
            steps
            {
                echo 'Jar Code ...'
                sh '$MAVEN_HOME/mvn clean package -e'
            }
        }
        stage('Sonarqube')
        {
            steps
            {
    			withSonarQubeEnv('sonar')
    			{
					sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
    			}
            }
        }
        stage('Run')
        {
            steps
            {
                echo 'Run Jar ...'
                sh 'nohup bash $MAVEN_HOME/mvn spring-boot:run &'
            }
        }
        stage('Build')
        {
            steps
            {
                git 'https://github.com/DonCarlosRiveros/ejemplo-maven.git'
                sh "$MAVEN_HOME/mvn -Dmaven.test.failure.ignore=true clean package"
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
