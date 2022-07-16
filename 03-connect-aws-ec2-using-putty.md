## Good Day Everyone

Hope you all are doing well.

With this post, I'd like to share my learning on how to connect to your AWS EC2 instance using Windows SSH Client i.e. "Putty".
Though, there are several articles describing the steps, I'd like to share mine what I experienced during the task. 

This experience arose from the exercise that I was doing for installting gitlab-runner rpm on my AWS EC2 instance running with AWS AMI.
During the creation of the EC2 instance, I generated the keypair with the .pem extension whhich is to be used with Open SSH. There is already an option to generate the keypair with .ppk extension which compatible to use with Putty, but I skipped to check it.
Once the EC2 instance came up, I tried connecting to EC2 instance using SSH client i.e. Putty installed on my Windows machine.

However, when I configured the SSH connection in Putty with the key (.pem) download from AWS, it didn't work and prompted me to use a key with .ppk extension.
It prompted me to look through and execute the steps that are required to connect to EC2 instance successfully

## Steps Involved
- Setup AWS EC2 instance with a public IP address and keypair (.pem)

```
Name: example-vm
Application and OS Image: Amazon Linux
```
![vm-name](images/03-connect-ec2-vm-using-putty/example-vm-1.png)

```
Instance Type: t2.micro (which is available for free in free tier account)
Key pair (login): Click on "create a new key pair"
```
![instance-type](images/03-connect-ec2-vm-using-putty/example-vm-2.png)

```
Key pair name: example-vm-keypair
Key pair type: RSA
Private key file format: .pem
```
![key-pair](images/03-connect-ec2-vm-using-putty/example-vm-5.png)

```
Network Settings
```
![network-settings](images/03-connect-ec2-vm-using-putty/example-vm-3.png)

Click on Launch Instance
Once the instane is UP, it will be shown as below.

```
Instances
```
![instances](images/03-connect-ec2-vm-using-putty/example-vm-4.png)


- Install PuTTy and PuTTYgen

If Putty is not installed on your Windows machine, you can refer the [link](https://www.putty.org/) to download the executable.
Once the Putty is installed, you'll also notice that there is another utility named "PuTTygen" is also installed.

![puttygen1](images/03-connect-ec2-vm-using-putty/example-vm-6.png)

- Configure PuTTYgen

Load an existing private key file. Click on Load and browse to the keypair file with .pem extension
![puttygen2](images/03-connect-ec2-vm-using-putty/example-vm-7.png)

As soon as you select the .pem file, it gets loaded into PuTTygen

Click on Save private key and select "yes" when prompted to save the file without passphrase. Save the file to a safe location on your machine.

![puttygen2](images/03-connect-ec2-vm-using-putty/example-vm-8.png)

- Configure PuTTy

It is time to configure PuTTy to be able to connect to EC2 instance using the keypair with .ppk extension you just generated.

Open the AWS console and navigate to the running instance. Click on the instance.
Copy either Public IPv4 address or Public IPv4 DNS Name.

![instance-details](images/03-connect-ec2-vm-using-putty/example-vm-9.png)

Open PuTTy on your Windows machine and configure new session for EC2 instance

```
Host Name (or IP Address): Public IPv4 Address or Public IPv4 DNS Name
Port: 22
Saved Session: example-vm
```

![puttysession1](images/03-connect-ec2-vm-using-putty/example-vm-10.png)

Navigate to Connection --> SSH --> Auth --> Private key file for authentication --> Browse and select the keypair file with .ppk extension

```
Private key file for authentication: example-vm-keypair.ppk
```

![puttysession2](images/03-connect-ec2-vm-using-putty/example-vm-11.png)

Navigate to Session and click Save to save the newly created session. Click on Open.

![puttysession3](images/03-connect-ec2-vm-using-putty/example-vm-12.png)

A new PuTTy window opens up and asks for your confirmation to save the key in PuTTy cache. Click Yes.

![puttysession4](images/03-connect-ec2-vm-using-putty/example-vm-13.png)

It will ask you the username. Once entered, you are logged into the AWS EC2 machine.

```
login as: ec2-user
```

![puttysession5](images/03-connect-ec2-vm-using-putty/example-vm-14.png)

That is all Folks for now. I'll keep sharing my learnings. If my posts sound interesting to you, following are the places, where I can be reached.

Like, Share, Follow, Comment.

| [LinkedIn](https://www.linkedin.com/in/prabhatsingh/) | [Dev](https://dev.to/prabhatsingh014) | [Medium](https://medium.com/@prabhatsingh014) |
| ------ | ------ | ------ |
