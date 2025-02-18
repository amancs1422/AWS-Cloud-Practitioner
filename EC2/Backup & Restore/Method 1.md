### Method 1: Create a new EBS volume from the snapshot and attach to an existing instance.

Step 1: Login to ${\color{red}AWS \space Management \space Console}$ and navigate to EC2 dashboard. Then click on ${\color{red} Launch \space Instances}$ button. <br>
![EC2 dashboard](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%201.png)<br>
Step 2: Fill in the EC2 instance name and leave the rest of the details as it is and click on ${\color{red} Launch \space Instances}$ button. <br>
![Fill_details_Launch_Instance](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%202.png)<br>
Step 3: Select your instance and click on Connect button.<br>
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%203.png)<br>
Step 4: You can execute the below commands to capture the EC2 details pre-restore.<br>
```
 lsblk
```
```
 df -h
```
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%204.png)<br>
Step 5: Now let’s create some files to be stored in our EC2 instance using below command.<br>
```
vi test.txt
```
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%205.png)<br>
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%206.png)<br>
You can view the file using the below cat command.
```
cat test.txt
```
You can also copy the first file into several others using the below cp command.
```
cp test.txt test1.txt
```
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%207.png)<br>
Step 6: Navigate to the Volumes section in EC2 dashboard and select the volume attached to your EC2 instance.<br>
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%208.png)<br>
Step 7: Dropdown the actions section and click on Create snapshot.<br>
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%209.png)<br>
Step 8: Provide a description for the snapshot and click on Create Snapshot button. <br>
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2010.png)<br>
Step 9: Navigate to the Snapshots section in the EC2 dashboard and you will find the snapshot you have just created. <br>
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2011.png)<br>
Step 10: Select the snapshot and dropdown on Actions section and select Create volume from snapshot. <br>
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2012.png)<br>
Note: Make sure to check that the Availability Zone of the volume created is same as the EC2 instance you want to restore.<br>
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2013.png)<br>
Our backup has been complete since we have created files in our EC2 instance and we have taken a point-in-time copy of the EC2 instance, let’s go ahead and delete the files so we can restore them back using volume created from snapshot above.<br>
<br>
Step 12: Use the below command to delete the files in your EC2 instance.<br>
```
rm test.txt test1.txt test2.txt test3.txt test4.txt 
```
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2014.png)<br>
Step 13: Select the newly created volume (I have named it as Restore_volume) and dropdown on the Actions button and select Attach volume.<br>
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2015.png)<br>
Step 14: Select the instance you want to restore and choose the device name (I have chosen /dev/sdf here) and click on Attach volume button.<br>
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2016.png)<br>
Step 15: To make sure that the restore volume is attached to your EC2 instance select your EC2 instance in Instances section of EC2 dashboard and navigate to storage section, you will see the volume attached there.<br>
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2017.png)<br>
Step 16: Execute the below command to check and make sure that your volume is attached to your EC2 instance.<br>
```
lsblk
```
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2018.png)<br>
Step 17: Even though the volume is attached to your EC2 instance, we still need to mount it for the files to be restored.<br>
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2019.png)<br>
Step 18: Use the following mount command to mount the volume to your EC2 instance.
```
mount /dev/xvdf1 /root/newvolume 
```
You will see a very common error you might face while mounting the new volume to your existing instance.<br>
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2020.png)<br>
Take below steps to resolve the error.<br>
Step 19: Execute the below command to see the exact filesystem of the restore volume.<br>
```
sudo lsblk –output NAME,TYPE,SIZE,FSTYPE,MOUNTPOINT,LABEL
```
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2021.png)<br>
Step 20: Execute the command below to specify the filesystem of your restore volume while mounting.<br>
```
mount /dev/xvdf1 /root/newvolume -t xfs 
```
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2022.png)<br>
We still get the wrong fs type error. To resolve do the following:<br>
<br>
Step 21: Execute the command below to see the latest error logs. You will see the "Filesystem has duplicate UUID error".<br>
```
dmesg | tail 
```
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2023.png)<br>
Step 22: To bypass the above error, execute the command:<br>
```
sudo mount -o nouuid /dev/xvdf1 /mnt/
```
Navigate to your mount location using below command.<br>
```
cd /mnt/home/ec2-user/.
```
Then execute ls command to see all the files restored back to your EC2 instance. <br>
```
ls 
```
![](https://github.com/amancs1422/AWS-Cloud-Practitioner/blob/main/Images/BKP_Restore%2024.png)<br>
