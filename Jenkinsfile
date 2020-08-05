node{
   stage('SCM Checkout'){
    git 'https://github.com/ravipatidar-github/mvnwebapp'
    }
    stage ('Compile-Package'){
      //Get maven home path
      def mvnHome = tool name: 'Maven 3.6.3', type: 'maven'
       mvn package
      }
   }
