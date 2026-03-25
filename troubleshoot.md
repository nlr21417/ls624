# Website not loading

## 03-25-2026 
### My website at 35.192.178.142 is not loading

It's taking quite awhile to load my SSH, so maybe that is the problem. 

#### Error Note
Connection via Cloud Identity-Aware Proxy Failed
Code: 4003
Reason: failed to connect to backend

Connection to VM is refused.
Please ensure that:
- VM has a firewall rule that allows TCP ingress traffic from the IP range 35.235.240.0/20, port: 22
- SSH daemon on target VM is up and running

You may be able to connect without using the Cloud Identity-Aware Proxy.

#### Troubleshoot 
1. VM Status: OK
2. Network Status: Skipped
     A. Network Management API has not been used in project syslib-624-roberts before or it is disabled.
     B. Enable it by visiting https://console.developers.google.com/apis/api/networkmanagement.googleapis.com/overview?project=syslib-624-roberts then retry.
     C. If you enabled this API recently, wait a few minutes for the action to propagate to our systems and retry.
3. IAM Permissions: Skipped
     A. Cloud Identity-Aware Proxy API has not been used in project syslib-624-roberts before or it is disabled.
     B. Enable it by visiting https://console.developers.google.com/apis/api/iap.googleapis.com/overview?project=syslib-624-roberts then retry.
     C. If you enabled this API recently, wait a few minutes for the action to propagate to our systems and retry.
   After enabling both API I am trying to get into the SSH. All OK, but SSH still not loading. 
  
  #### RESOLVED
I ended up stopping the instance and restarting. That fixed the issue. 
