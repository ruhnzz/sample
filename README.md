pipeline{
    agent any
    tools{
        maven 'MAVEN_HOME'
    }
    stages{
        stage('git repo & clean'){
            steps{
               // bat "rmdir /s /q javaMavenProject"
                bat "git clone https://github.com/ruhnzz/javaMavenProject.git"
                bat "mvn clean -f javaMavenProject"
            }
        }
        stage('install'){
                steps{
                    bat "mvn install -f javaMavenProject"
                }
            }
            stage('test'){
                steps{
                    bat "mvn test -f javaMavenProject"
                }
            }
            stage('package'){
                steps{
                    bat "mvn package -f javaMavenProject"
                }
            }
        }
    }
