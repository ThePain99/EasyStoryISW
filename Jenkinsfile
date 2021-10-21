pipeline {
    agent any
    tools { 
        maven 'MAVEN_3_6_3' 
        jdk 'JDK_1_13' 
    }
	def tomcatWeb = 'C:\\Users\\josep\\Desktop\\Ciclo 2021-2\\Repositorio Apps\\EasyStoryISW\\.idea\\artifacts'
	def tomcatBin = 'C:\\Users\\josep\\Documents\\apache-tomcat-9.0.53\\bin'
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

	    stage('Deploy to Tomcat'){
             bat "copy target\\easystory_war.war \"${tomcatWeb}\\easystory_war.war\""
           }
              stage ('Start Tomcat Server') {
                 sleep(time:5,unit:"SECONDS")
                 bat "${tomcatBin}\\startup.bat"
                 sleep(time:100,unit:"SECONDS")
           }

		/* // Descomentar cuando se tenga instalado en Tomcat
		stage('Deploy tomcat') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL} direcion ${env.WORKSPACE}"	
                withMaven(maven : 'MAVEN_3_6_3') {
					bat '"C:\\Program Files\\Git\\mingw64\\bin\\curl.exe" -T ".\\target\\sistema-ventas-spring.war" "http://tomcat:tomcat@localhost:9090/manager/text/deploy?path=/sistema-ventas-spring&update=true"'
                } 
            }
        }*/

    }
}
