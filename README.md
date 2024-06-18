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
  5. Set the deployment type to all at once or can change to any of the pre-configured deployment types according to your needs.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/6f04cb25-75fc-4d5f-80c1-f095c0346fca)
  6. You can enable the load balancing if you think you're going to get huge traffic, for this instance we are going to keep it disabled, and save the changes.
  7. You can check if your deployment is working fine as it will start the deployment for the fist time when you save it.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/347eceb9-ca4d-450e-82fc-1394bc3b073d)
  8. If everything goes fine, you can check your deployed website on the public ip of your ec2 instance. First Connect to your EC2 instance with cloud connect.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/33ca5468-67de-4a83-a3f9-a13c90c8cf31)
  9. Go to the public ip and open in new tab. You should see you webpage deployed there.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/f90c2cfe-5d88-426b-9497-6a7ecfc7d714)
  10. If you encounter any problems in the deployment phase you can check the logs of your EC2 instance for debugging using this command:

  `sudo tail -n 20 /var/log/aws/codedeploy-agent/codedeploy-agent.log`

  this should give your previous 20 logs, you can edit this command to get more.

## Create a new pipeline with AWS CodePipeline 
  1. Go to CodePipeline and create a new pipeline.
  2. Give the pipeline a Name and set the pipeline type as V2 so that it can take actions on new pull requests or new push to the repository.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/370721ca-2fdd-4b22-ac1f-55c3dc55d303)
  3. Add the source from where you'll be pulling in code from. In this case it is github, and give all the information related to the repository.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/c9f18679-2799-462a-a479-d5c72e24a11e)
  4. Add the CodeBuild project Name for the build stage.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/a90ee42f-e0d1-41c5-b74c-77402eb86a7f)
  5. Finally add the CodDeploy application name and deployment group name to the deploy stage and create the pipeline.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/c3bfc568-830b-415c-b7dc-164aa46d199d)
  6. This will trigger the pipeline and will build the project and dploy it on the EC2 seerver we created using Nginx. This should result in a successful deployment if everything is working as intended.
  ![image](https://github.com/Zatch07/Web-Deployment-CI-CD-Pipeline-using-AWS-and-Github/assets/56155256/7402d648-07c8-4171-81dc-c7336d1f766c)



