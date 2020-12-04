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
        stage('Test')
        {
            steps
            {   
                echo 'Test Code ...'
                sh '/usr/share/maven/bin/mvn clean test -e'
            }
        }
        stage('Jar')
        {
            steps
            {
                echo 'Jar Code ...'
                sh '/usr/share/maven/bin/mvn clean package -e'
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
        stage('Run')
        {
            steps
            {
                echo 'Run Jar ...'
                sh 'nohup bash /usr/share/maven/bin/mvn spring-boot:run &'
            }
        }
        stage('Build')
        {
            steps
            {
                git 'https://github.com/DonCarlosRiveros/ejemplo-maven.git'
                sh "/usr/share/maven/bin/mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
    }
}
