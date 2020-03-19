---
title: "Nextfow and AWS Batch Tutorial"
date: 2020-03-18T22:48:37Z
draft: false
---


Amazon Web Services Batch is a service that allows users to submit jobs to job queues while specifying the application to be run and compute resources that are needed by the job. Working in concert with Nextflow, AWS Batch can be configured to run Nextflow processes in defined compute environments minimizing the cost of cloud resources.

## Useful Resources

This tutorial was written using [Alex Peltzer's guide](https://apeltzer.github.io/post/01-aws-nfcore/) and [Anthony Underwood's guide](https://antunderwood.gitlab.io/bioinformant-blog/posts/running_nextflow_on_aws_batch/) as resources. In addition there are several other resources that you might find helpful when setting this up.
* [Nextflow AWS Batch Blog Post](https://www.nextflow.io/blog/2017/scaling-with-aws-batch.html)
* [Nextflow AWS Batch Documentation](https://www.nextflow.io/docs/latest/awscloud.html#aws-batch)
* [List of Nextflow pipelines and Tutorial's](https://github.com/nextflow-io/awesome-nextflow#tutorials)
* [Nextflow Gitter Chat](https://gitter.im/nextflow-io/nextflow)

## Table of Contents

* [Setting up a programmatic user with IAM](#setting-up-a-nextflow-user)
* [Creating a custom Amazon Machine Image (AMI)](#creating-a-custom-ami)
* [Creating an AWS Batch compute environment](#create-aws-batch-compute-environment)
* [Creating an AWS Batch Job queue](#creating-an-aws-batch-job-queue)
* [Setting up an S3 Bucket](#setting-up-an-s3-bucket)
* [Configuring Nextflow to use AWS Batch](#configuring-nextflow-to-use-aws-batch)
* [Tips and Tricks](#tips-and-tricks)

## Setting up a Nextflow User
You may be tempted to skip this step if you already have a user with programmatic access to AWS. However, it is best practice to have a separate user account that only has the needed access credentials. This step is also valuable in understanding and setting up the access policies that both Nextflow and AWS Batch need in order to operate.

#### Step 1: Add a user
Navigate to the IAM Service and click on Users. Then click **Add user** and in the **User name** box add the user name that you would like, here I used `nextflow-programmatic-access`. Then select the box for **Prgrammatic access**. When you've finished click the **Next: Permissions** button.

![add user](/resources/imgs/001.PNG)

#### Step 2: Create a group for the user
Next we need to create a group for this user to be a part of. We will later add policies to this group specific to Netflow. Click on the **Create Group** button.

![create group](/resources/imgs/002.PNG)
In the **Group name** box add the name of the group here I used `nextflow-group`. Then click the **Create group** button.

![name group](/resources/imgs/003.PNG)

After adding the group click the **Next: Tags**.

#### Step 3: Tags and Review
This page will allow you to add any extra tags to the account to assign metadata. These are optional, after you've completed click **Next: Review**. Here you should be presented with a screen that looks similar to below. Click **Create user** to finish the user creation.

![review screen](/resources/imgs/004.PNG)

#### Step 4: User Creation
After user creation there will be a page that provides the security credentials for using the new Nextflow user. This includes the **Access Key ID** and **Secret access key**. These are crucial and are only generated once at this step. If they are lost you will have to delete and create a new user using the steps above. Click the **Download .csv** button and keep the file in a safe and secure location. These access credentials will be needed later.

![user creation success](/resources/imgs/005.PNG)

#### Step 5: Attach policies to new group
From the IAM user panel click **Groups** and click on the nextflow group created above, here we used `nextflow-group`. Then click on the **Attach Policy** button.

![attach policy screen](/resources/imgs/007.PNG)

From here we will add the following 3 policies:
* **AmazonEC2FullAccess**
* **AmazonS3FullAccess**
* **AWSBatchFullAccess**

You can find these by typing them into the Filter box.

![final roles](/resources/imgs/011.PNG)

#### Step 6: Create Roles for running AWS Batch
From the IAM user panel click the **Roles** button. Here we will create a role for running EC2 Spot Instances. If you would rather create on-demand instances only you can skip this step, however you can achieve significant cost savings using Spot Instances. Click the **Create role** button.

![create role](/resources/imgs/011a.PNG)

On the create role page scroll down and find and click on **EC2**.

![create role page](/resources/imgs/011b.PNG)
![ec2 on role page](/resources/imgs/011c.PNG)

Then select the **EC2 - Spot Fleet Tagging** use case and click the **Next: Permissions** button you should see the screen below.

![ec2 role](/resources/imgs/011d.PNG)

Click the **Next: Tags** button add any additional metadata tags you would like then click the **Next: Review** button. Then fill out the **Role name** box with the name for this Role, here I used `AmazonEC2SpotFleetRole`.

![create role final](/resources/imgs/011e.PNG)

Once finished click the **Create role** button.

## Creating a custom AMI
When using Nextflow with Docker and AWS Batch there are a few special requirements for the instances that will be hosting the images and running the processes. The images require a specific configuration to use Amazon's Elastic Container Service (ECS), which allows the use of Docker in the Amazon environment.

#### Step 1: Starting a virtual machine
To create the AMI we need the first step is to startup a virtual machine running the base image we need. To start goto the **EC2** Service in the AWS management console. Then click **Instances** and **Launch Instance**. The first step in launching an instance is selecting the AMI. In the search box type `ECS` and select the **Amazon ECS-Optimized Amazon Linux AMI** image under the **AWS Marketplace**.

![select ami](/resources/imgs/012.PNG)

A window will pop-up displaying the pricing information for using the AMI. Select **Continue**. The next step is to choose an instance type. Since we are creating this instance to customize the AMI we can select a small instance. Here I chose the t2.medium.

![choose instance type](/resources/imgs/014.PNG)

The next step is configuring the instance details which can be configured to how you would normally set up an instance for interactive access. Here I use the default settings.

![configure instance details](/resources/imgs/015.PNG)

In the add storage step we have an option to update the space available to the Docker container. By default the space is set to **22 GB**. This is the allowed space for use by each job that is submitted. Here we need to update the storage space for the needs of our pipeline. I choose to set it to `100` GB, which provides enough space for all the reads from a typical MiSeq run to fit in a single job with a bit of room to spare. You can change this to any amount you think is necessary for your pipeline. However, keep in mind that you will be paying for the cost of the snapshots. This cost is usually minimal (a few dollars a month) and can be tracked under the **AWS Cost Management**, **Cost Explorer**.

![add storage](/resources/imgs/017.PNG)

Once the instance storage is configured click the **Next: Add Tags** button and add the metadata tags you see fit. Once finished click the **Next: Configure Security Group**. Configure the instance so you can access it interactively. Once you have finished click the **Review and Launch**.

#### Step 2: Install dependencies
Once the instance is up an running login into the instance using the credentials you selected using the `ec2-user` account. Once logged in you should see a screen similar to below.

![ec2-user login](/resources/imgs/018.PNG)

The first step is to adjust the size of the docker storage device to match the updated size. If you use the command `docker info` you'll notice the `Base Device Size: 10.74GB`. We need to update this by editing the docker configuration file in `/etc/sysconfig/docker-storage`. Using `sudo vi` open the file and add `--storage-opt dm.basesize=100GB` adjusting the 100GB to reflect the size you picked above. The file should look something like this:
```
DOCKER_STORAGE_OPTIONS="--storage-driver devicemapper --storage-opt dm.thinpooldev=/dev/mapper/docker-docker--pool --storage-opt dm.use_deferred_removal=true --storage-opt dm.use_deferred_deletion=true --storage-opt dm.fs=ext4 --storage-opt dm.use_deferred_deletion=true --storage-opt dm.basesize=100GB"
```
To verify the changes use the command `sudo service docker restart` and see the changes with `docker info`.

After configuring docker the next step is to install AWS-CLI. This is needed by Nextflow to send data from each step. The easiest way is to install via miniconda with the commands below:
```
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86\_64.sh
bash Miniconda3-latest-Linux-x86\_64.sh -p /home/ec2-user/miniconda
/home/ec2-user/miniconda/bin/conda install -c conda-forge awscli
/home/ec2-user/miniconda/bin/aws --version
```

#### Step 3: Save the image
Once AWS-CLI is installed you can save the image by choosing **Action Image -> Create Image** on the selected image. Give the image an appropriate name and when it has finished creating the image you can terminate the instance. Make note of the AMI `ami-01dec29g8b4d78253` this will be used later.

## Create AWS Batch compute environment
Next we have to configure the compute environment where the Nextflow jobs will run. Go to the Batch service in the AWS management console. If this is your first time using batch you will see a screen like below. Click the **Get Started** button.

![get started](/resources/imgs/021.PNG)

You will then see the setup wizard for AWS Batch. The wizard doesn't setup things the way we need so we will select the **Skip wizard** button shown below.

![skip wizard](/resources/imgs/022.PNG)

#### Step 1: Define compute environment name and roles

Once you are at the AWS Batch dashboard select **Compute environments** and **Create environment**.

![batch dashboard](/resources/imgs/023.PNG)

Then select the box for **Managed** in the compute environment type if not already selected and enter a name in the **Compute environment name**.

![create compute start](/resources/imgs/024.PNG)

Next select **Create new role** for both **Service role** and **Instance role**. AWS Batch will create roles with the needed permissions. However, we will need to add an aditional policy to the **ecsInstanceRole** later to use AWS S3. You may select an EC2 key pair to be able to ssh into the instance but this is optional.

#### Step 2: Define compute environment resources
Here we can define if we want to use On-Demand or Spot and how much we are willing to pay. If using On-Demand simply select **On-Demand** in the **Provisioning model** and define the **Allowed instance types** with instance types you wish to use i.e. **c4.xlarge** or **c5.4xlarge**. Set **Allocation strategy** to **BEST_FIT** and continue on to Step 3.

If you would like to use Spot instances, which can be run at a fraction of the price. Under **Provisioning model** select **Spot**. Then set the **Maximum Price** valued by the % of the On-demand price. Here I picked 50%, which works for most cases. You could also select 100% which means you are willing to go all the way to the On-demand price but if there is a lower price available you'll still get it. *Note if you find it taking awhile to create instances try raising this value*.

Then under the **Allocation strategy** select **BEST_FIT** and choose the **AmazonEC2SpotFleetRole** we created earlier. Finally under the **Allowed instance types** select instance types you wish to use i.e. **c4.xlarge** or **c5.4xlarge**. I usually use the c4 and c5 family of instance types but this should be tailored to your workflow.

![define compute](/resources/imgs/024a.PNG)

#### Step 3: Determine compute environment limits
Next you will see 3 options including **Minimum vCPUs**, **Desired vCPUs**, and **Maximum vCPUs**. These are used to define the amount of resources that can be used. **Note**: the values are vCPUs not number of instances, so if you only allow instances with 16 vCPUs to be used in your compute environment and you set the minimum vCPUs to 1. You will always have a 16vCPU instance running. The values are further defined as:
* **Minimum vCPUs** - The minimum number of virtual resources that must be kept running at all times. Setting this to 0 means all resources will be shutdown when not in use. 0 is recommended for cost savings.

* **Desired vCPUs** - This is how many vCPUs you would like to see used. Nextflow will dynamically change this value so we can leave it set to 0.

* **Maximum vCPUs** - This is the maximum number of vCPUs that could be running at any one time. I typically leave this set to `256` but you can alter it as you see fit.

Finally we need to select the AMI we created in the previous section. Check the box for **Enable user-specified AMI id** and enter the AMI from above then click **Validate AMI**.

![resource limits](/resources/imgs/026.PNG)

#### Step 3: Finish and create the compute environment
At the last step, define the subnet you would like your instances to run on (usually just default) and security group then click **Create**

#### Step 4: Update the ecsInstanceRole
We need to add the S3 role to the newly created ecsInstanceRole. Go to the IAM service as done in Step 6 in the [Setting up a programmatic user with IAM](#Setting-up-a-Nextflow-User) section. Under **Roles** enter `ecs` in the search box and click on the **ecsInstanceRole**. Click the **Attach policies** and enter `S3` in the filter box and select the **AmazonS3FullAccess**, then click **Attach policy**.

You should have both the **AmazonS3FullAccess** and the **AmazonEC2ContainerServiceforEC2Role** policies attached to this role.

## Creating an AWS Batch Job queue
Next we need to create a queue where Nextflow can submit jobs to the compute environment. Navigate to the Batch service on the AWS management console and select **Job queues** and **Create queue**.

Enter the name of the queue (this will be needed later in nextflow) and give it a priority. A priority of 1 means that jobs submitted to the compute environment via this queue will have priority over jobs submitted via a queue with a lower priority. This does not matter if you only have 1 queue using the compute environment but if you have multiple queues you can define their priorities. Finally in the dropdown box select the compute environment we created in the previous section and click **Create job queue**.

![create job queue](/resources/imgs/029.PNG)

## Setting up an S3 Bucket
Nextflow can use S3 buckets to store and access data. Go to the **S3** service under the AWS management console and select **Create bucket**. Name the bucket (will be used in the nextflow configuration) and select the appropriate region where you have configured everything else and select **Create bucket**. In the bucket create a folder `test_env` where Nextflow can work with files.

## Configuring Nextflow to use AWS Batch
In the final section of the guide there are a few parameters that need to be added to the Nextflow config in order to use the AWS Batch environment we created. There are a number of configuration variables that can be set ([more here](https://www.nextflow.io/docs/latest/awscloud.html#awscloud-batch-config)) but the basics are:
```
//indicate that we want to use awsbatch
process.executor = 'awsbatch'

//indicate the name of the AWS Batch job queue we want to use
process.queue = 'my-batch-queue'

//Name of the docker container we want to use, we can also specify a separate docker container for each process
process.container = 'quay.io/biocontainers/salmon'

//region where we want to run this in
aws.region = 'us-east-1'

//Important note!!! Since we created a custom AMI
//we need to specify the path to the aws cli tool
//if you followed the instructions above for custom AMI
//the path is:
aws.batch.cliPath = '/home/ec2-user/miniconda/bin/aws'

//Additionally if we want to use S3 to hold intermediate files we can specify the workdirectory
workDir = 's3://bucket_you_created/test_env/'
```

Finally, the last step is to setup your AWS-CLI and AWS user credentials. To install AWS-CLI on your host system you can follow these steps:
```
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86\_64.sh
bash Miniconda3-latest-Linux-x86\_64.sh -p /home/ec2-user/miniconda
/home/ec2-user/miniconda/bin/conda install -c conda-forge awscli
/home/ec2-user/miniconda/bin/aws --version
```
In the section [Setting up a programmatic user with IAM](#setting-up-a-nextflow-user) we created a user that would be able to access the AWS services and launch jobs. One option is to include the credentials in the configuration (**not recommended**):
```
aws {
    accessKey = '<YOUR S3 ACCESS KEY>'
    secretKey = '<YOUR S3 SECRET KEY>'
    region = '<REGION IDENTIFIER>'
}
```
 However, this is not recommended as the keys could be made acidentially public if you share your configuration file.

The best approach is to use the command `aws configure` and enter the security credentials. After setting these configuration parameters your Nextflow workflow is ready to use AWS Batch!!

## Tips and Tricks
AWS can be tricky to navigate if things aren't working. Here are some various places you can look if things aren't going as expected.

The biggest issue I've seen is jobs sitting in the **RUNNABLE** step in the AWS Batch Job queues and not moving to **STARTING** or **RUNNING**. This can be cause by a number of issues but it's best to first check the roles and policies created above. Here are the roles and polices you should have:

**Roles and respective policies for AWS Batch**

- AmazonEC2SpotFleetRole  
    * AmazonEC2SpotFleetTaggingRole

- ecsInstanceRole  
    * AmazonS3FullAccess
    * AmazonEC2ContainerServiceforEC2Role

- AWSBatchServiceRole  
    * AWSBatchServiceRole

Additionally, sometimes the jobs will move from **RUNNABLE** to **FAILED**. Clicking the number of jobs in the **FAILED** column will reveal the individual jobs and clicking on one might show the error message that caused it to fail via CloudWatch. That can often help diagnose issues in the compute environment.

Another location you may find error messages is under the EC2 service:  
* If you are running On-Demand in the **Launch Configurations** under the EC2 service will show the configurations launched by AWS Batch and any potentiall issues or errors encountered.
* If you are running Spot instances examining the **Spot Requests** is a good place to look for errors as well.
h
