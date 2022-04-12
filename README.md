# IAM policy for Start,stop and reboot EC2 instances based on tags


This example shows how you might create an identity-based policy that allows an IAM user to Start,stop ans reboot EC2 instances, but only if the instance tag Env has the value of the Dev. This policy defines permissions for programmatic and console access.

Here we have two EC2 instances with the "Name" tag as"webserver", one instance is used for production purposes and the other is for Development purposes. Here I'm using the project name or tag as "myproject". So here we are going to set the permission for a user to see all the instances and have the privilege to start, stop and reboot the instances with tags "Name" as "webserver",  "Project" as "myproject" and "env" as "dev".

## Prerequisites

- An IAM user on your AWS account that has "AWS Management Console access"
- Two EC2 instances:
     
      First instance with tags as:
          Name    : Webserver
          project : myproject
          env     : prod

      Second Instance with tags as:
          Name    : Webserver
          project : myproject
          env     : env
       

![image](https://user-images.githubusercontent.com/100775027/162905646-d73730fc-fd5d-4b82-9856-3e105934d44c.png)


## Add the IAM policy for the user

To add the policy for an already created user,  select the User name that you want to set the permission on the AWS Identity and Access Management (IAM) console and select the button "Add permissions". 
```bash
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:StartInstances",
                "ec2:StopInstances",
                "ec2:RebootInstances"
            ],
            "Resource": "arn:aws:ec2:<region>:<account-id>:instance/*",
            "Condition": {
                "StringEquals": {
                    "ec2:ResourceTag/Name": "Webserver",
                    "ec2:ResourceTag/project": "myproject",
                    "ec2:ResourceTag/env": "dev"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": "ec2:Describe*",
            "Resource": "*"
        }
    ]
}

```

Please replace <region> with you AWS region and <account-id> with your AWS account id.

## Conclusion

In this tutorial, we have discussed how to add an IAM policy to Start or stop EC2 instances based on tags. Please let me know when you encounter any difficult errors while using this.
Thanks!!!

 ### ⚙️ Connect with Me

<p align="center">
<a href="https://www.linkedin.com/in/radin-lawrence-8b3270102/"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/></a>
<a href="mailto:radin.lawrence@gmail.com"><img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white"/></a>
