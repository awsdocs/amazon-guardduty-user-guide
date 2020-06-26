# Generating Sample Findings in GuardDuty<a name="sample_findings"></a>

You can generate Sample findings with GuardDuty to help you visualize and understand the various finding types that GuardDuty can generate\. When you generate sample findings, GuardDuty populates your current findings list with one sample finding for each supported finding type\. The generated samples are approximations populated with preset dummy values, so they may look different from real findings for your environment, but they can be use to test various configurations of your GuardDuty such as your CloudWatch Events or filters\. For more information about GuardDuty finding types, see [Active Finding Types](guardduty_finding-types-active.md)\.

To generate some common findings based on simulated activity within your environment see [Automatically Generating Several Common GuardDuty Findings](#guardduty_findings-scripts) below\.

## Generating Sample Findings Through the GuardDuty Console<a name="sample_console"></a>

Use the following procedure to generate sample findings\.

****

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. In the navigation pane, under **Settings**, choose **General**\.

1. On the **Settings** page, under **Sample findings**, choose **Generate sample findings**\.

1. In the navigation pane, under **Findings**, choose **Current**\. The sample findings are displayed on the **Current findings** page\. The title of sample findings always begins with **\[SAMPLE\]**\. Choose a specific sample finding to view its details\.

## Automatically Generating Several Common GuardDuty Findings<a name="guardduty_findings-scripts"></a>

You can use the following [scripts](https://github.com/awslabs/amazon-guardduty-tester) to automatically generate several common GuardDuty findings\. **guardduty\-tester\.template** uses AWS CloudFormation to create an isolated environment with a bastion host, a tester EC2 instance that you can ssh into, and two target EC2 instances\. Then you can run **guardduty\_tester\.sh** that starts interaction between the tester EC2 instance and the target Windows EC2 instance and the target Linux EC2 instance to simulate five types of common attacks that GuardDuty is built to detect and notify you about with generated findings\.

1. As a prerequisite, you must enable GuardDuty in the same account and Region where you want to run the **guardduty\-tester\.template** and **guardduty\_tester\.sh**\. For more information about enabling GuardDuty, see [Setting Up GuardDuty](guardduty_settingup.md)\.

   You must also generate a new or use an existing EC2 key pair in each Region where you want to run these scripts\. This EC2 key pair is used as a parameter in the **guardduty\-tester\.template** script that you use to create a new CloudFormation stack\. For more information about generating key pairs, see [Amazon EC2 Key Pairs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)\.

1. Create a new CloudFormation stack using **guardduty\-tester\.template**\. For detailed instructions about creating a stack, see [Creating a Stack](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-create-stack.html)\. Before you run **guardduty\-tester\.template**, modify it with values for the following parameters: Stack Name to identify your new stack, Availability Zone where you want to run the stack, and Key Pair that you can use to launch the EC2 instances\. Then you can use the corresponding private key to SSH into the EC2 instances\.

   **guardduty\-tester\.template** takes around 10 minutes to run and complete\. It creates your environment and copies **guardduty\_tester\.sh** onto your tester EC2 instance\.

1. In the AWS CloudFormation console, choose the checkbox next to your new running AWS CloudFormation stack\. In the displayed set of tabs, select the **Output** tab\. Note the IP addresses assigned to the bastion host and the tester EC2 instance\. You need both of these IP addresses in order to ssh into the tester EC2 instance\.

1. Create the following entry in your \~/\.ssh/config file to login to your instance through the bastion host:

   ```
   Host bastion
           HostName {Elastic IP Address of Bastion}
           User ec2-user
           IdentityFile ~/.ssh/{your-ssh-key.pem}
           Host tester
           ForwardAgent yes
           HostName {Local IP Address of RedTeam Instance}
           User ec2-user
           IdentityFile ~/.ssh/{your-ssh-key.pem}
           ProxyCommand ssh bastion nc %h %p
           ServerAliveInterval 240
   ```

   Now you can call $ ssh tester to login to your target EC2 instance\. For more information about configuring and connecting to EC2 instances through bastion hosts, see [https://aws\.amazon\.com/blogs/security/securely\-connect\-to\-linux\-instances\-running\-in\-a\-private\-amazon\-vpc/](https://aws.amazon.com/blogs/security/securely-connect-to-linux-instances-running-in-a-private-amazon-vpc/)\. 

1. Once connected to the tester EC2 instance, run **guardduty\_tester\.sh** to initiate interaction between your tester and target EC2 instances, simulate attacks, and generate GuardDuty Findings\.