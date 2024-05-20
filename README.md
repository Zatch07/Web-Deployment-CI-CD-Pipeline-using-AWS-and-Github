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
