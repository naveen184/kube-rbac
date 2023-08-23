
Steps to create Kubernetes RBAC in a cluster 


Step 1: Clone the repository. 

Step 2: Create a namespace namespace-poc and set context using 

         kubectl config set-context --current --namespace=namespace-poc
  
Step 3: Create service.yaml, aws-auth.yaml, rbacuser-role.yaml, rbacuser-role-binding.yaml and adminclusterrole.yaml using below syntax                                              

        kubectl create -f filename.yaml

Step 4: Run below command to get all the roles created.

       kubectl get role
Output:

        NAME     CREATED AT
        dev      2023-08-23T14:31:52Z
        devops   2023-08-23T14:31:52Z
        qa       2023-08-23T14:31:52Z
        
Step 5: Run below command to get the binded roles. 

       kubectl get rolebinding
Output:
       
        NAME          ROLE          AGE
        dev_role      Role/dev      171m
        devops_role   Role/devops   171m
        qa_role       Role/qa       171m
        
Step 6: Run below command to get the admin role created.
          
          kubectl get clusterrole | grep 'adminpoc' 

Output:

           adminpoc      2023-08-23T14:33:50Z
        
Step 7: Run 

           kubectl get clusterrolebinding | grep 'adminpoc'
                    
         to get the binded role.

Output:

        global-access     ClusterRole/adminpoc     176

Step 8: Run 
              
            kubectl describe role

            kubectl describe rolebinding
            
            kubectl describe clusterrolebinding | grep 'adminpoc'
            
            kubectl describe clusterrolebinding | grep 'adminpoc'
            
        To describe role and to view all the users associated with the roles.


Step 9: To check the access of all the user use 
        
        kubectl auth can-i verbs resource --as=user

          # kubectl auth can-i get pods --as=naveen
          yes
          
          # kubectl auth can-i create pods --as=naveen
          no
          
          # kubectl auth can-i create pods --as=mavathurmahesh
          yes
          
          # kubectl auth can-i create pods --as=dev_user
          no
          
      Output: Yes - User has the access
      Output: No - User has no access
      
Step 10: To delete run 
              
          kubectl delete -f filename.yaml
            
