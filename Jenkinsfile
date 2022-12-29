// Define the pipeline
pipeline {
// Set the agent to run on a Kubernetes cluster
agent {
kubernetes {
// Set the label to use for the Jenkins agent pods
label 'jenkins-agent'
// Set the namespace to use for the Jenkins agent pods
namespace 'jenkins'
}
}
// Set the triggers to build the pipeline on new commits or pull request events
triggers {
githubPush()
githubPullRequest()
}
// Define the stages of the pipeline
stages {
// Define the build stage
stage('Build') {
// Run the build steps in a container
steps {
container('maven') {
// Run the Maven build
sh 'mvn clean package'
}
}
}
// Define the test stage
stage('Test') {
// Run the test steps in a container
steps {
container('openjdk') {
// Run the unit tests
sh 'mvn test'
}
}
}
// Define the deploy stage
stage('Deploy') {
// Run the deploy steps in a container
steps {
container('kubectl') {
// Set the environment variables for the Kubernetes deployment
withEnv(["NAMESPACE=production"]) {
// Deploy the application to the Kubernetes cluster
sh 'kubectl apply -f deploy/kubernetes/deployment.yml'
}
}
}
}
}
}
