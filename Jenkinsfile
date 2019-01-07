/**
 * This pipeline will execute a simple Maven build
 */

def label = "maven-${UUID.randomUUID().toString()}"

podTemplate(label: label, containers: [
  containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat')
  ]) {

  node(label) {
      
    stage('build with maven') {
        
      //git 'https://github.com/jenkinsci/kubernetes-plugin.git'
      def scmVars
      scmVars = checkout scm
        
      container('maven') {
          // Run Build
          sh '_JAVA_OPTIONS=-Djdk.net.URLClassPath.disableClassPathURLCheck=true mvn clean install'
      }
    }
    
    stage('deploy to QA') {
       
      container('maven') {
          // Push Build
          echo "Done!" > result.txt
      }
        
    }
  }
}

