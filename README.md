**Summary of Issues Encountered and Solutions**
1. Initial Setup Challenges
Issue: Understanding how to set up the Docker container and deploy the Flask app.

Solution:
Identified the correct Dockerfile structure.
Used docker run with proper port mappings to expose the Flask app.

2. Running Docker Image
Issue: Docker container couldn’t bind to port 80 or 8080 as they were already in use.

Solution: Used sudo lsof -i :80 and sudo lsof -i :8080 to identify conflicting processes.
Stopped conflicting processes (e.g., other Docker containers using the ports) and freed up the ports.
Used alternative ports like 8081 when necessary.

3. Application Accessibility
Issue: Unable to access the application from the external IP, leading to ERR_CONNECTION_REFUSED.
Cause:
Misconfigured firewall rules.
Application not running correctly or on a non-mapped port.

Solution: Ensured the Docker container was running with the correct port mappings.
Updated Google Cloud firewall rules to allow traffic on the required ports (80, 8080, 8081).

4. Testing Routes in Flask Application
Issue: Flask app returned 404 for / because the route wasn’t defined.
Solution:
Reviewed main.py and identified key routes (/chat, /load_model, /ping).
Used /ping for connectivity checks and /chat for Retool integration.

5. External IP Visibility
Issue: Unable to access the Flask app from the external IP of the VM.

Cause:Firewall rules weren’t initially configured to allow external traffic.
Miscommunication between Docker’s internal and external port mappings.

Solution: Configured the VM’s firewall to allow traffic from all IPs (0.0.0.0/0) on specific ports.
Verified the external IP and port accessibility using browser and tools like curl.

6. Retool API Query Setup
Issue: Understanding how to connect Retool to the Flask application.

Solution: Created a REST API resource in Retool using the Flask app’s base URL (http://<VM_EXTERNAL_IP>:<PORT>).
Configured queries in Retool for /chat, /load_model, and `/ping


**Screenshots for the view of what I did**
**Virtual Machine**

![image](https://github.com/user-attachments/assets/f726f3c4-861c-4e87-a15f-61b5ec6401b6)

![image](https://github.com/user-attachments/assets/1540f10a-52f5-4cf4-aa9c-04f10157cf3b)

![image](https://github.com/user-attachments/assets/34222366-f42c-4a99-a56b-988f95ed7f10)

**Firewall Rules**
![image](https://github.com/user-attachments/assets/2ae43d7a-0736-4008-8c77-ef37359bd734)

![image](https://github.com/user-attachments/assets/6d84fafd-95ed-4b5f-9be5-f0b000fa40b3)

**Hugging Face Token**
![image](https://github.com/user-attachments/assets/79128930-0757-4235-ba27-2901d3b2da48)

**Image in Docker Hub**
![image](https://github.com/user-attachments/assets/60041de6-d643-4c31-aea7-df3cd205cd8f)

**Retool**

![image](https://github.com/user-attachments/assets/54e3f43e-e7ad-4a52-95f7-59f1fb78e353)
![image](https://github.com/user-attachments/assets/a4c4cab2-42b3-4dd2-bf61-b16182715927)
![image](https://github.com/user-attachments/assets/8c32a0ae-5ec2-4f8b-991a-0c943dfa47af)
![image](https://github.com/user-attachments/assets/baf83834-fbea-4669-bce6-5ccb4787b5af)
![image](https://github.com/user-attachments/assets/cdcfe0a2-1621-49f2-ad53-496ce5ac8876)
![image](https://github.com/user-attachments/assets/da7a6344-8c45-4f38-86ad-f86350a812b7)









