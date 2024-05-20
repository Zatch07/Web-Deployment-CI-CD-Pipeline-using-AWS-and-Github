# Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github

## Create a repository from which you want to import your code
  1. Create a repository that you want to create a CI/CD project on.
  2. Add the necessary files to your repository.
  3. In my case I'm using a repository from my GitHub profile.
  4. Be sure to include a buildspec.yml and an appspec.yml file, which will be required for code-build and code-deploy.

## Create a new build project in AWS CodeBuild
  1. Give your project a name.
  2. Set the source as from where you would like to import your code for build purposes.
  3. Give the necessary permissions for connecting to the repository and accessing the code.
  ![Screenshot 2024-05-19 172659](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/453b25a1-751f-4338-a9c0-ead66d8fe211)
  4. Set-up the environment in which your code will build on.
  ![Screenshot 2024-05-19 173018](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/f794197d-50e7-45fa-b1ec-4d06f7e52906)
  5. In the buildspec column insert your buildspec file name (No need if it is already in the repository as buildspec.yml) or create one using 'insert build commands'.
  ![Screenshot 2024-05-19 173351](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/29ab98a9-6f79-4d35-9005-7a4383d9cecc)
  6. After saving all the changes save the build project you can start the first build process.
  ![Screenshot 2024-05-19 190202](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/935849d6-4bed-4bc1-b6b5-d3b70c47c012)
  7. If you get any errors you can check phase details for which part is causing the build to fail.
  8. If it goes smoothly you are ready to go to the next phase.

## Create an EC2 machine to run your deployment instance.
  1. Create a new EC2 instance with whatever configuration you would like to run your appication on.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/16d5e225-65b9-4b93-a7a0-7be91f70c6a9)
  2. Create a new role for the EC2 service to be able to communicate with other service that are set up.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/68100c06-3f40-491f-87ac-f43e91f616d2)

## Create a Deployment group for the application
  1. Go to AWS CodeDeploy and create an application.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/5624a1c7-179f-477e-a6b8-cd7ef4714cb9)
  2. Under the application create a new deployment group and give it a name and add the service role with the following permissions.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/7c9be610-3a54-4f35-8834-234dbb2d44c8)
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/8e74d73e-a462-4b57-9a8a-d051d39100ed)
  3. Choose the type of deployment you would like, I'm chosing 'in place' for simple implementation.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/29cbd1e0-d98d-4bee-a2fe-a482a9cac7f4)
  4. Set up the environment configuration as Amazon EC2 Instances. Use the key as Name and add the name of the EC2 instance that we created before.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/c43bdbb4-a516-4400-bd76-fd18fceae8c1)
  5. 
