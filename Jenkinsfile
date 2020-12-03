pipeline {
    agent any
	environment {
        MAVEN_HOME = '/usr/share/maven/bin'
    }
    stages {
        stage('Compile') {
            steps {
				dir('/HDD/Personales/Dip-DevOps/Unidad_3/Sesion_4/ejemplo-maven') {
                echo 'Compile Code ...'
                sh './mvnw clean compile -e'
				}
            }
        }
        stage('Test') {
            steps {	
				dir('/HDD/Personales/Dip-DevOps/Unidad_3/Sesion_4/ejemplo-maven') {
                echo 'Test Code ...'
                sh './mvnw clean test -e'
				}
            }
        }
        stage('Jar') {
            steps {
				dir('/HDD/Personales/Dip-DevOps/Unidad_3/Sesion_4/ejemplo-maven') {
                echo 'Jar Code ...'
                sh './mvnw clean package -e'
				}
            }
        }
        stage('Run') {
            steps {
				dir('/HDD/Personales/Dip-DevOps/Unidad_3/Sesion_4/ejemplo-maven') {
                echo 'Run Jar ...'
                sh 'nohup bash mvnw spring-boot:run &'
				}
            }
        }
        stage('TestApp') {
            steps {
				dir('/HDD/Personales/Dip-DevOps/Unidad_3/Sesion_4/ejemplo-maven') {
                echo 'Testing Application ...'
                sh 'curl -X GET http://localhost:8081/rest/mscovid/test?msg=testing'
				}
            }
        }
    }
 }	