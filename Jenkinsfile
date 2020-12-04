pipeline
{
    agent any
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
    }
}
