## Creating a user in IAM

Access your AWS management console and search for IAM.<br>
On the next screen, click on Users section. <br>
NOTE: Users in AWS have global scope.<br>
Click on create user button.<br>
Enter your desired username.<br>
You can provide the custom password and decide whether you want user to change password after first login. Click next,<br>
In the below screen you can decide to add user to a group in IAM or assign permissions/policies manually.<br>
If you don’t see a group on your screen in the user groups section, then you can create a group as below:<br>
Click on create group. Choose your desired permission policy and click on create user group.<br>
Now choose the group you want your user to be added in and click on Next.<br>
In the next screen you can review the permissions the user will have and add a tag to the user if desired.<br>
The next screen has several options to explore, you can choose to email the sign-in instructions to your desired email address. Or, you can also download a .csv file containing the credentials.<br>
Hit the button “Return to users list”<br>
And you can see your user “<username>” is created. <br>
And if you click on your user you will find it belongs to the group of your choice.<br>

## Policies in IAM
<br>
To view the policies in IAM please click on policies in the IAM screen.<br>
Click on create policy and you will find several options:<br>
If you’re unfamiliar with JSON, don’t panic AWS has a visual way of designing policies. Just pick and choose and AWS will spin its magic wand.<br>
Pick a service and you shall see several options:<br>
An example, here I have picked IAM as the service and the action chosen is all or (*) and I have chosen to deny all actions. <br>
Provide a policy name and click create policy button.<br>
Now let’s see the power of policies.<br>
I am going to add this policy to one of my users and we will see that the user will not be able to access IAM.<br>
Upon logging into my new user account, I will try and access IAM.<br>
And as expected access to IAM is denied for this user.<br>
