node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/shaikapsar/cucumber-jvm-maven.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
      
   }
   stage('Build') {
       
      withMaven(
      maven: 'M3',
      mavenSettingsConfig: '1647b207-6381-4c1c-bb2c-2ae717dda657'){
      // Run the maven build.
      if (isUnix()) {
        // sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
        sh "mvn -Dmaven.test.failure.ignore clean package"
      } else {
       //  bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
    }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
      step([$class: 'CucumberReportPublisher', jsonReportDirectory: "target/cucumber/", jenkinsBasePath: '', fileIncludePattern: 'cucumber.json'])
   }
   
}
