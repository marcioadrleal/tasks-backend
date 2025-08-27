pipeline{
   agent any
   stages{
      stage('Build BackEnd'){
        steps{
            bat 'mvn clean package -DskipTests=true'
        }
      }
      stage('Test Unit'){
        steps{
            bat 'mvn test'
        }
      }
      stage('Sonar Analysis'){
        environment{
            scannerHome = tool 'Sonar_Scanner'
        }
        steps{
            withSonarQubeEnv('SONAR_LOCAL'){
             bat "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DelployBack -Dsonar.host.url=http://localhost:9000 -Dsonar.token=sqp_b699c3aa30706e9ab6978ed855bcfdd6cea33623 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Application.java"
            }
        }
      }
      stage("Quality Gate"){
        steps{
          sleep(10)
          timeout(time: 2 , unit: 'MINUTES'){
            waitForQualityGate abortPipeline: true
          }
          

        }
      }  
     
   }

}


