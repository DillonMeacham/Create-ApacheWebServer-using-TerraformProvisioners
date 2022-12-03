<h1>Using Terraform Provisioners to Set Up an Apache Web Server on AWS
</h1>

<h2>Description</h2>
Let's learn a little about Terraform Provisioners. Terraform Provisioners are used for executing scripts or shell commands on a local or remote machine as part of resource creation/deletion. They are similar to “EC2 instance user data” scripts that only run once on the creation and if it fails terraform marks it tainted.

<br />
<br />

In this project, we'll be using a Terraform provisioner to custom bootstrap a VM in AWS and install a webserver on it, and then test that the webserver is working as expected. Let's get started.

<br />

<img src="https://imgur.com/xnyVBli.png" height="70%" width="70%" />


<h2>Environments Used </h2>

- <b>Terraform</b>
- <b>Local Command Prompt</b>
- <b>Choice of Web Browser</b>

<h2>Project walk-through:</h2>


First we are going to examine our main.tf which houses the resources we are going to use to spin up this instance and utilize the provisioner to create a Apache webserver on it.
<br />
<br />
Let's examine the provisioner block in the code. The provisioner we are using is a 'Remote' provisioner which we can see is using the 'remote-exec' keyword. It is basically going to try to connect to the resources that is being spun up in our resource block, in this case is the AWS EC2 instance and execute the following commands located in the provisioner block.
 <br />
<br />
<img src="https://imgur.com/kXsJ3i8.png" height="85%" width="85%">
<br />
<br />
<img src="https://imgur.com/fwv8RPV.png" height="85%" width="85%">
<br />
<br />

The provisioner knows how to connect to the resource because of the connection block in the code. We are basically telling this provisioner we want it to connect using SSH, passing the username that is linked with the AWS instance which is 'ec2-user' as well as the private key and IP address it needs to connect to.
<br />
<br />

Now let's start deploying the code to access the bootstrapped webserver :)
<br />
<br />
Let's run the 'terraform init' command to Initialize the working directory and download the required providers.
<br />
<br />
<img src="https://imgur.com/Z7qnqKt.png" height="85%" width="85%">
<br />
<br />
Next we will run 'terraform validate' to ensure we do not have any syntactical issues with our code.
<br />
<br />
<img src="https://imgur.com/wVO9QY8.png" height="85%" width="85%">
<br />
<br />
Review the actions that will be performed when we deploy the code using the 'terraform plan' command. I forgot to grab a screenshot for this step, so sorry :(
<br />
<br />
Finally we can Deploy the code with the terraform apply command. I'm going to pass it the -auto-approve flag so it doesn't prompt me to confirm the action.
<br />
<br />
<img src="https://imgur.com/SJzbgay.png" height="85%" width="85%">
<br />
<br />
Navigate to the bootstrapped webserver's IP address, and validate that the provisioner worked as intended.
<br />
<br />
<img src="https://imgur.com/uift60s.png" height="85%" width="85%">
<br />
<br />
So now that we've come to an end, lets destroy the resources we just created using 'terraform destroy -auto-approve'
<br />
<br />
<img src="https://imgur.com/eKUznLw.png" height="85%" width="85%">
<br />
<br />
<h1>Thank you for reading :)<h1>


