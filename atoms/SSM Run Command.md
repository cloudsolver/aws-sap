#Question How can an administrator access EC2 nodes without SSH?

You must install [[SSM]] Agent on EC2. The ability to use an agent to log in to an [[EC2]] instance without enabling port 22 for [[SSH]] in [[SG | security group]] is available via SSM Run Command.

#Question How can commands be executed within EC2 instances?

SSM Run Command can run scripts on EC2 instances and on-premise nodes. 
No need for SSH. It runs through the agent, and command logs are sent to S3 or SNS for status. Integrated with CloudTrail. EventBridge is automated. Run via SSM agent.

![[SSM Run Command Architecture.png|384]]
**Fig. SSM Run Command integration from SSM**