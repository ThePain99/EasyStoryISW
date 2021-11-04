pipeline {
    agent any
    tools { 
        maven 'MAVEN_3_6_3' 
        jdk 'JDK_1_13' 
    }
    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'MAVEN_3_6_3') {
                    bat 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'MAVEN_3_6_3') {
                    bat 'mvn test'
                }
            }
        }

	
	/*stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'MAVEN_3_6_3') {
                    bat 'mvn deploy'
                }
            }
        }*/

        stage ('package Stage') {
            steps {
                withMaven(maven : 'MAVEN_3_6_3') {
                    bat 'mvn package'
                }
            }
        }
	    
		 // Descomentar cuando se tenga instalado en Tomcat
		stage('Deploy tomcat') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL} direction ${env.WORKSPACE}"
                withMaven(maven : 'MAVEN_3_6_3') {
					bat '"C:\\Program Files\\Git\\mingw64\\bin\\curl.exe" -T ".\\target\\easystory-0.0.1-SNAPSHOT.war" "http://tomcat:tomcat@localhost:9090/manager/text/deploy?path=/EasyStoryISW&update=true"'
                } 
            }
        }

    }
}
