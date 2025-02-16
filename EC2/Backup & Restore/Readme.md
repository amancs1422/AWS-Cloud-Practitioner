# :signal_strength:Restoring an EC2 instance using snapshot

### :floppy_disk: What is a Snapshot?

### :page_with_curl: Following are the ways to Restore an EC2 instance using snapshot:

 :one:Create a new EBS volume from the snapshot and attach to an existing instance.<br>
  :two:Replace the root volume of an existing EC2 instance with a new volume created from the snapshot.<br>
  :three:Copy snapshot to another region and restore an EC2 instance.<br>
  :four:Automate EC2 recovery using AWS Backup.<br>
  :five:Create a new AMI from the snapshot and launch a new instance.<br>
  current issue i'm facing on this-> files are not being restored to the newly created EC2.

<details>
  <summary>Important Links</summary>
  :link: https://www.youtube.com/watch?v=85djWS1rDyE -> Fix for mounting issue in the Method 1<br>
  :link: https://docs.aws.amazon.com/ebs/latest/userguide/ebs-snapshots.html -> AWS Documentation on Snapshots.<br>
</details>
