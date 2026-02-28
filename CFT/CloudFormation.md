# Cloud Formation Templates (AWS)
>> https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html


## How to write perfect template?
* Follow the Template formats to get used to it.
* Also checkout Template anotomy for clear understanding.
* Even though if you don't follow rules to organise template is valid for other details, descriptions, metadata, and etc.
* But Resources section should be must, becuase we are using CFT to create resources right.


## A Sample template to create EC2 Instance:

```
AWSTemplateFormatVersion: 2010-09-09
Description: A sample CloudFormation template with YAML comments.
# Resources section
Resources:
  MyEC2Instance: 
    Type: AWS::EC2::Instance
    Properties: 
      # Linux AMI
      ImageId: ami-1234567890abcdef0 
      InstanceType: t2.micro
      KeyName: MyKey
      BlockDeviceMappings:
        - DeviceName: /dev/sdm
          Ebs:
            VolumeType: io1
            Iops: 200
            DeleteOnTermination: false
            VolumeSize: 20
```