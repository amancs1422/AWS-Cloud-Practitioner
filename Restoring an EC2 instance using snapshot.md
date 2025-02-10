# Restoring an EC2 instance using snapshot

### :milky_way: What is a Snapshot?

### Following are the ways to Restore an EC2 instance using snapshot:
<ol>
  <li>Create a new EBS volume from the snapshot and attach to an existing instance.</li>
  https://www.youtube.com/watch?v=85djWS1rDyE -> fix for mounting issue in the above step.
  <li>Replace the root volume of an existing EC2 instance with a new volume created from the snapshot.</li>
  <li>Copy snapshot to another region and restore an EC2 instance.</li>
  <li>Automate EC2 recovery using AWS Backup.</li>
  <li>Create a new AMI from the snapshot and launch a new instance.</li>
  current issue i'm facing on this-> files are not being restored to the newly created EC2.
</ol>
