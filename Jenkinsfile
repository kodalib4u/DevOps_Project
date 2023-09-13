pipeline
{
   agent{
          node {
               label 'maven'
              }
       }
   stages{
      stage("Clone Repository")
         {
           steps
             {
               git branch: 'main', url: 'https://github.com/kodalib4u/DevOps_Project.git'
             }
         }
    }
}
               
      
