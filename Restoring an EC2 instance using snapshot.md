# :signal_strength:Restoring an EC2 instance using snapshot

### :floppy_disk: What is a Snapshot?

### Following are the ways to Restore an EC2 instance using snapshot:
<ol>
  <li>Create a new EBS volume from the snapshot and attach to an existing instance.</li>
  :link: https://www.youtube.com/watch?v=85djWS1rDyE -> fix for mounting issue in the above step.<br>
  :link: https://docs.aws.amazon.com/ebs/latest/userguide/ebs-snapshots.html -> AWS documentation on snapshots.
  <li>Replace the root volume of an existing EC2 instance with a new volume created from the snapshot.</li>
  <li>Copy snapshot to another region and restore an EC2 instance.</li>
  <li>Automate EC2 recovery using AWS Backup.</li>
  <li>Create a new AMI from the snapshot and launch a new instance.</li>
  current issue i'm facing on this-> files are not being restored to the newly created EC2.
</ol>

### Method 1: Create a new EBS volume from the snapshot and attach to an existing instance.

Step 1: Login to ${\color{red}AWS \space Management \space Console}$ and navigate to EC2 dashboard. Then click on ${\color{red} Launch \space Instances}$ button. <br>
![EC2 dashboard](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%201.png)<br>
Step 2: Fill in the EC2 instance name and leave the rest of the details as it is and click on ${\color{red} Launch \space Instances}$ button. <br>
![Fill_details_Launch_Instance](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%202.png)
