# Qwiklabs Back Build and Secure Networks in Google Cloud Challenge Lab
Step by Step guide to solve this challenge. Can refer my YouTube video for the same : 


# 1.Check the firewall rules. Remove the overly permissive rules.

Navigation menu ->VPC network->Firewall              
check open-access ->delete                     

# 2.Navigate to Compute Engine in the Cloud Console and identify the bastion host. The instance should be stopped. Start the instance.

Navigation menu->Compute Engine->VM Instances               
check bastion -> Start VM instance                     

# 3.The bastion host is the one machine authorized to receive external SSH traffic. Create a firewall rule that allows SSH (tcp/22) from the IAP service. The firewall rule should be enabled on bastion via a network tag.

Navigation menu->VPC network->Firewall->Create Firewall Rule               
Name - allow-ssh-from-iap             
Network - acme-vpc                   
Targets - Specified targets             
Target tags - bastion             
Source filter - IP ranges            
Source IP ranges - 35.235.240.0/20                                    
(Goto SSH (tcp/22) from the IAP service and copy Source Ip ranges.)                      
Protocols and ports - Specified protocols and ports                       
check tcp : type 22                     
Create                    

Navigation menu ->Compute Engine ->VM instances                         
Click on bastion ->Edit ->Network tags = bastion                               
Save                

# 4.The juice-shop server serves HTTP traffic. Create a firewall rule that allows traffic on HTTP (tcp/80) to any address. The firewall rule should be enabled on juice-shop via a network tag.
 
Navigation menu ->VPC network ->Firewall-> Create Firewall Rule                          
Name - allow-http-ingress         
Network - acme-vpc                
Targets - Specified target tags               
Target tags - allow-http             
Source filter - IP ranges             
Source IP ranges - 0.0.0.0/0                 
Protocols and ports - Specified protocols and ports                        
check tcp : type 80                 
Create               

Navigation menu ->Compute Engine ->VM Instances->Click on juice-shop->Edit                    
Network tags - allow-http             
Save                  

# 5.You need to connect to juice-shop from the bastion using SSH. Create a firewall rule that allows traffic on SSH (tcp/22) from acme-mgmt-subnet network address. The firewall rule should be enabled on juice-shop via a network tag.

Navigation menu ->Compute Engine ->VM Instances->Click on juice-shop->Edit              
Network tags - juice-shop             
Save               

Navigation menu ->VPC network ->Firewall-> Create Firewall Rule                    
Name - allow-ssh-for-acme-mgmt-subnet                  
Network - acme-vpc                    
Targets - Specified target tags                 
Target tags - bastion juice-shop                  
Source filter - IP ranges                         

Open VPC networks in the left menu  in new tab                        
Copy IP address of acme-mgmt-subnet                           

Source IP ranges - [paste IP address copied here]                   
Protocols and ports - Specified protocols and ports                      
check tcp : type 22                        
Create          

# 6.In the Compute Engine instances page, click the SSH button for the bastion host. Once connected, SSH to juice-shop.
Navigation menu ->Compute Engine ->VM instances                
Click SSH terminal of bastion            
-> ssh [IP of juice-shop]                  
-> yes if asked                       
->ls    

# Congratulations you have successfully completed your challenge lab. Don't forget to subscribe my channel.



