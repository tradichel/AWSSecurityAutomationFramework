# README #
This code is old. I recommend checking out the 2sl-jobexecframework and related repositories.

### What is this repository for? ###
 
* Test environment for SANS Paper on automated intrusion detection & response

* This code installs a honeypot and some instances in a VPC with Flow Logs enabled.

* An AWS Lambda function automatically makes a snapshot and terminates instances that match  undesirable traffic patterns. 

* NOTE: This code is not production ready nor is it fully tested.

* Use at your own risk.

* The Honey VPC Network is wide open to the Internet but blocks traffic within the VPC. Do not deploy this and open rules in that network that expose your other networks within your account.

### How do I get set up? ###

* Create an AWS account: https://aws.amazon.com/getting-started/
 
* Install and configure the AWS CLI with your access key ID, secret key and region: http://docs.aws.amazon.com/cli/latest/userguide/installing.html

* You may or may not want to generate an AWS SSH Key (not required) to log into your instances: http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html

* Install git https://git-scm.com/

* Clone this repo: https://git-scm.com/docs/git-clone

	git clone https://github.com/tradichel/AWSSecurityAutomationFramework.git 

* Change the accountid value in run.sh to your AWS account id. This is used to generate unique resource names and some ARNs (Amazon's unique resource identifier) for some resources that require it.

* To run the stack execute this code once. Then follow the instructions (wait and run again after logs appear)

	./run.sh CREATE [optional AWS SSH key name, without .pem at the end]

* To delete the stack execute:

	./run.sh DELETE
	
* To run a ping test that generates a REJECT and terminates instance execute:

	./run.sh PINGTEST

* The scripts are re-runnable. If something fails to create due to dependency issue you can typically just run it again.

* The reason you have to run it twice is because I didn't want to sit waiting for the logs to show up. It can take some time. 


### Known Issues ###

* Need to only create one snap then stop if it exists (tag).
* Need to delete snapshot + all logs in DELETE mode.

### Who do I talk to? ###

* @teriradichel

### Resources ###

Subscriptions - to copy data from CloudWatch to Lambda
http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/Subscriptions.html

Lookup latest AMI with lambda function
http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/walkthrough-custom-resources-lambda-lookup-amiids.html

Terminate EC2 instances:
https://github.com/raweng/Builtio-DevOps/blob/master/scale-down-poc-with-lambda/second-lambda.js

Launch an instance with AWS CLI
http://docs.aws.amazon.com/AWSEC2/latest/CommandLineReference/ec2-cli-launch-instance.html

Making requests to AWS APIs using node.js
http://docs.aws.amazon.com/AWSJavaScriptSDK/guide/node-making-requests.html

Node.js callbacks in loops
http://www.richardrodger.com/2011/04/21/node-js-how-to-write-a-for-loop-with-callbacks/#.Vsp_JpMrKqB

EC2 Node JS AWS SDK
http://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html

Traffic on port 0:
http://www.pcworld.com/article/2061080/spike-in-traffic-with-tcp-source-port-zero-has-some-researchers-worried.html

Some NTP info
http://koltsoff.com/pub/securing-centos/

Flow Log Reocords
http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/flow-logs.html#flow-log-records

AWS IP ranges - JSON
https://ip-ranges.amazonaws.com/ip-ranges.json

