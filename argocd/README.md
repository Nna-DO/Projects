These are screenshots of steps taken to bootstrap EKS cluster with ArgoCD using terraform.

Step 1: Create and Instance, ssh into the said instance, perform updates, install necessary tools such as Helm, Terraform, Git, Docker. Verify they exist in the instance.
![image](https://github.com/user-attachments/assets/97d1322c-6c39-4352-b112-94bc1c9bd3c3)


Step 2: make a directory called “Project”, perform a “git init”, clone the repository with the code, git fetch your own repository, remove all unwanted folders (we are interested in the argocd folder), mv the folder to your own folder. 
Note: These steps can be found in the screenshots below.
![image](https://github.com/user-attachments/assets/7cea2398-06aa-4a6d-9905-92a1c98d5927)

![image](https://github.com/user-attachments/assets/bab48c60-5525-4d1c-a1d7-cb0cbcb3c246)


Step 3: Cd into argocd>terraform and run a “terraform init, terraform plan and terraform apply” to create the EKS cluster with all its resources.
![image](https://github.com/user-attachments/assets/ac09f23b-4246-4bf9-985c-b0c0ee65ec3e)

![image](https://github.com/user-attachments/assets/df7549a5-a735-4583-90a8-7608000c349e)

![image](https://github.com/user-attachments/assets/816e51cd-43e5-4896-87e4-388bb2575e08)

![image](https://github.com/user-attachments/assets/d7e1215e-b117-45a8-a81f-0014f4394d40)


Step 4: Change the NodePort to LoadBalancer in the app.yaml file
![image](https://github.com/user-attachments/assets/f76b4f20-2397-46d9-9d4d-e930b71b8060)

![image](https://github.com/user-attachments/assets/1550d67b-f1fa-43c6-aef1-3adfedffc864)

Step 5: Run a kubectl apply, then check for svc, pods etc as shown below.
![image](https://github.com/user-attachments/assets/6b0ba572-54fb-4e65-a909-e7c4d60f0ccf)

![image](https://github.com/user-attachments/assets/4042e5fe-0d9d-4491-a559-9fab7be85438)

Step 6: Do a portforward as shown, 
a.	Check if it is working with localhost:8080 on your browser
![image](https://github.com/user-attachments/assets/ad077113-2920-40df-b652-f470f2ae2b4d)

b.	“open a new terminal as the handling connection is prompting so you don’t kill it and run the argocd get secret a password.
c.	open another terminal and run the  “argocd login localhost:8080” and follow prompt as shown.
![image](https://github.com/user-attachments/assets/8448afce-b742-4104-9a04-d388b7b2e064)

![image](https://github.com/user-attachments/assets/0477ba1d-43d6-4002-abf9-aec0fc4f59b4)


Step 7: Get the context  do an argocd cluster add, argocd repo add.
![image](https://github.com/user-attachments/assets/7e2cfef7-bb33-446d-90f1-0bccfbf086e0)

Step 8: Edit below to create and sync your application.
argocd app create appname \
   --repo https://github.com/username/repourl \
   --path argocd \
   --dest-server https://kubernetes.default.svc \
   --dest-namespace argocd

![image](https://github.com/user-attachments/assets/ef1217fe-56e7-4874-a984-de6eb8004462)

Step 9: Sync your application with “ argocd app sync <app name>”
![image](https://github.com/user-attachments/assets/6862f598-8dbc-4d11-97e2-9501e8b7a64f)

a.	If it is successful it will display like this.
![image](https://github.com/user-attachments/assets/0133d716-e120-42e5-8db5-87eb01a36870)


Step 10: Once the sync is successful, you can log in to your ArgoCD via the browser to check it out.
![image](https://github.com/user-attachments/assets/9074adb7-ec3b-4366-843e-8cc03d0a3999)

Note: Don’t forget to destroy every resource created by terraform with a “terraform destroy –auto-approve”



