These are screenshots of steps taken to create CI/CD pipeline using GitLab CI/CD on an AWS EC2 self-hosted runners.

Step 1:  Go to the GitLab Project > settings > CI/CD > Runners > expand 

![S1](https://github.com/user-attachments/assets/8b163ff1-2ab2-4c59-b99b-b37d11432006)

Step 2: Click on the “New project runner” Button.

![S2](https://github.com/user-attachments/assets/e3c67c75-fad7-42d1-bc7c-2b2893d1e02b)

Step 3: Check the “Run untagged jobs” – you can tag your jobs too, Add a “Runner description” for mine it was called “GitLab_Runner” and “maximum job timeout” was set to 1200. Click “Create Runner” button.

![S3](https://github.com/user-attachments/assets/517d9a57-08b2-4b1c-8806-c7ab68afc373)

![S3a](https://github.com/user-attachments/assets/d1a4bcc5-ceee-41a4-a7fa-d557ce459226)

Step 4: Select the Linux Operating system since we are going to use the AWS EC2 instance using Ubuntu Image.

![S4](https://github.com/user-attachments/assets/06acf596-e7fc-4358-aa16-795bdf550ec2)

Step 5: Create and AWS EC2 instance  using Ubuntu Image.
![S5](https://github.com/user-attachments/assets/dc004b3d-d69f-494b-9698-cea66b346ce8)

Step 6: On the EC2 Instance, Install Docker from their official documentation , Add and Install the official GitLab repository and runner from the official GitLab documentation

![S6](https://github.com/user-attachments/assets/727c935d-e0a7-4027-867e-3bf6f60f2914)

![S6a](https://github.com/user-attachments/assets/1d80d5f4-f10a-4508-99fa-55f34614244a)

Step 7: From the GitLab page, Register the Runner to the EC2 Instance with the information on the Runner webpage. You will be prompted to enter the GitLab instance URL, registration token, and an executor. Enter the URL  “https://gitlab.com/”, the registration token, and “shell” respectively as shown on the GitLab webpage, you can also name the Runner. The runner should be successfully registered. Go ahead and start the Runner with a “ gitlab-runner run”

![S7](https://github.com/user-attachments/assets/328bcf6a-24d0-4d2f-b51e-2c5dcf3c9aac)

![S7a](https://github.com/user-attachments/assets/ce8da3cf-7a7f-44e8-98c4-058bc3d43281)

Step 8: Exit the GitLab page to reveal the Assigned Runner.

![S8](https://github.com/user-attachments/assets/20dd0e9f-9caf-4d88-83b0-296fb01d2340)

Step 9: Create a “.gitlab-ci.yml” file and define your pipeline job. It is assumed that you already have the Source Code and dependencies in the project folder in GitLab. If you don’t go ahead and create each one – that is if you didn’t do a “git clone” to push to the GitLab repo. 

![S9a](https://github.com/user-attachments/assets/c732ca8c-59d2-45de-8a13-ff05fc03fa4e)

![S9a](https://github.com/user-attachments/assets/6dd3a72d-ea8f-4446-be1a-731f5119ad01)

Step 10: Add your variables from your “.gitlab-ci.yml” by defining them in the  setings > CI/CD > Variables.

![S10](https://github.com/user-attachments/assets/26b55dbb-4df6-4668-852f-bcf3d192953d)


Note: Our Runner automatically picks this information and starts building a Job in the pipeline. Select  Build > pipelines to see all the jobs, once it passes it shows like below.

The EC2 Instance
![S11](https://github.com/user-attachments/assets/ba0e4b37-0c68-478b-b039-733a175680c8)

The Job 
![S12](https://github.com/user-attachments/assets/b75439e7-b31b-44aa-86f5-57d0a3c34c99)


The Pipeline
![S13](https://github.com/user-attachments/assets/ed5f3e66-ac7f-4271-9e99-13c3d1c0d3a7)
