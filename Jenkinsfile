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
                sh './mvnvw clean compile -e'
            }
        }
        stage('Sonarqube')
        {
            steps
            {
    		withSonarQubeEnv('sonar')
    		{
			sh './mvnvw org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
    		}
            }
	}
    }
}
