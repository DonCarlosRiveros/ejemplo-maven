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
                sh '/usr/share/maven/bin/mvn clean compile -e'
            }
        }
        stage('Sonarqube')
        {
            steps
            {
    		withSonarQubeEnv('sonar')
    		{
			sh '/usr/share/maven/bin/mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
    		}
            }
	}
    }
}
