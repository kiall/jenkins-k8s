node ("linux") {
   // Mark the code checkout 'stage'....
   stage 'Checkout'

   // Get some code from a GitHub repository
   checkout scm
   
   // Mark the code build 'stage'....
   stage 'Build'
   
   // Run the container build
   sh "docker build ."
}
