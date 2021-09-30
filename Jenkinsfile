pipeline {
    agent any
    tools { 
        maven 'MAVEN_3_6_3' 
        jdk 'JDK_1_12' 
    }
	
    stages {
        stage ('Compile Stage EasyStoryISW') {

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
                    bat 'mvn apigee-enterprise:deploy'
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
	    
	    def TomCatWeb = 'C:\\Users\\josep\\Documents\\apache-tomcat-9.0.53\\webapps'
	    
	
		 // Descomentar cuando se tenga instalado en Tomcat
		stage('Deploy tomcat') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL} direcion ${env.WORKSPACE}"	
                withMaven(maven : 'MAVEN_3_6_3') {
					/*bat '"C:\\Program Files\\Git\\mingw64\\bin\\curl.exe" -T ".\\target\\easystory_war.war" "http://tomcat:tomcat@localhost:9090/manager/text/deploy?path=/easystory&update=true"'*/
			bat "copy target\\easystory_war.war \"${TomCatWeb}\\easystory_war.war\""
                } 
            }
        }

    }
}
