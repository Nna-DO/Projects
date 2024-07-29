 These are screenshots of steps taken to create CI/CD pipeline that builds a Docker image, pushes to a container registry and deploy to EKS using helm and GitHub Actions.

Step 1: Create and Instance, ssh into the said instance, perform updates, install necessary tools such as Helm, Terraform, Git, Docker. Verify they exist in the instance.
![image](https://github.com/user-attachments/assets/8ff30f82-6bb8-4fe7-b60f-fb3608847845)


Step 2: Clone the repository to your local.
![image](https://github.com/user-attachments/assets/b5dd7a6b-b3c8-413e-b4cb-c345135a0118)


Step 3: Cd into the cloned folder (devops-project). Since we are working on the cicd_helm_eks folder. For me I deleted the helm-chart folder (not necessary)  and the Docker cicd folder (necessary) within it. I then proceed to create a helm-eks- chart folder, cd into it and run a “Helm create docker-cicd”
![image](https://github.com/user-attachments/assets/390e8453-1753-44c9-bb14-bc6a55d03bb2)


Step 4: cd into the docker-cicd chart and open the values.yaml file. Helm initializes a chart deploying nginx by default. 
![image](https://github.com/user-attachments/assets/c600a693-b069-4543-b22e-7728c9fe3bcc)


Step 5: Edit the values.yaml file in line 7 - 11 since we are using our own image.  Remove nginx image and replace it with username/imagename. The plan is to get the pipeline to automatically fill in the username, image name, and tag name without us manually keying them in.
![image](https://github.com/user-attachments/assets/d8103e47-b0da-48ef-b2e5-a9fc657f7541)


Step 6: Set up your access key for Docker and AWS on your github.
![image](https://github.com/user-attachments/assets/221fa792-f395-4b03-aa0d-e4a506549d0f)


Step 7: Cd into the terraform folder, initialize the terraform “terraform init” and create an EKS cluster using the “Terraform apply --auto-approve” command.
Ps:If you already have an EKS cluster running in AWS you can use, you can skip this part and jump straight to the GitHub actions section. 
![image](https://github.com/user-attachments/assets/2e7c1a84-d40e-4a96-8809-c4245d17ec3b)

Successfully Initialized Terraform.
![image](https://github.com/user-attachments/assets/d774d4bb-6732-4368-8505-ddb922d54c3e)

Terraform apply created all the necessary resources needed for the AWS EKS cluster.
![image](https://github.com/user-attachments/assets/f0111fb7-8386-4b18-8d1b-ce4ed2f0f502)

![image](https://github.com/user-attachments/assets/59bc7605-f27b-4c9f-b4b1-af8012bc144e)


Step 8: Create a .github/workflows directory and create a build.yaml file there (This step can be done in github too)
![image](https://github.com/user-attachments/assets/f682a3f7-8c29-4e08-8857-e0aff4d22152)

![image](https://github.com/user-attachments/assets/41e2b0b3-6c13-44af-80be-a88173702765)

Note: I had to edit line 58, 65, 66, 68 and 71 because I renamed my folder “helm-eks-chart” from the “helm-chart” that was there. See step 3 for proof.
![image](https://github.com/user-attachments/assets/4807aa34-1898-4f12-b862-de5f158c1f70)

![image](https://github.com/user-attachments/assets/0e52ddcf-3c47-45e0-b32f-f0a0bcf7f6c8)


Do a git push and a  deployment is triggered. 
![image](https://github.com/user-attachments/assets/74cf1358-d613-47ce-92ab-1bed44a6f0a5)


![image](https://github.com/user-attachments/assets/b6b99649-4961-4ed3-bd8e-29b8a2e428c6)


Step 9: Upon successful deployment, install kubectl in your terminal to interact with your EKS Cluster, a new context and interact with your Cluster, run a “kubectl get pods” and “kubectl get svc” to verify the creation of pod and service.
Note: The service type is Cluster IP and no external IP is found.
![image](https://github.com/user-attachments/assets/2b413af0-8bc4-49f4-b00f-6599ec0dec5b)


Step 10: Open your values.yaml file and edit line 43-44 from Cluster IP to loadBalancer and edit port. A new deployment is run and this time when you run a “Kubectl get svc” we notice  svc type is now loadbalancer  and an external IP address is created. 
![image](https://github.com/user-attachments/assets/1eeccdec-08f3-4c43-a18b-46572194b87c)

![image](https://github.com/user-attachments/assets/86d94c99-f0e4-4d2f-adec-88976833fc03)

Copy the external IP address and port number to your url and a page will be displayed.
![image](https://github.com/user-attachments/assets/5a475276-03d8-4dc8-88db-06a774836db5)


Note: Open your terraform folder and run a "terraform destroy --auto-approve" to destroy all the EKS resources created.








































































