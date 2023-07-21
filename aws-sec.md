# AWS Sec

Some of the top things building blocks

Think in terms of capabilities

Core capabilities

Deploy stuff
Run things on Stuff

Governance
Some degree of control for security and regulatory requirements.

Be familiar with what you are trying to protect.

Where do I need boundaries, which things do I need to protect.


Have as many accounts as possible. - minimize cost of account lifecycle.

- Dedicated account for per incident. ensure fresh environment.


Avoid multiple AWS org. its very very messy. 

IR accounts usage volume of events is very low and thus is easy to audit.

OU as a policy enforcement 

Use of eventBridge to centralize all cloudwatch to security account and then use SCP to ensure no one is able to modify other than security team.

AuditTrail - who did what and when
visibility of workload - what apps are doing.

Be clear about your requirements.

stateless fim. based on osquery
s3 FIM?

Solve Compute, Network, Data and Identity.


