aws-secrets
===========

Synopsis
========

Set up AWS resources:
```
./init-resources myapp
```

Make some secrets, send them to the cloud:
```
echo "export SECRET=xyzzy" > aws-secrets
./send-aws-secrets myapp aws-secrets
```

Now retrieve the secrets:

```
./aws-retrieve-secrets myapp
```

The last one can be run by:
  - users in the `myapp-manage-secrets` group
  - instances which have been started with the `myapp-secrets` iam profile
  e.g. `aws ec2 run-instances ...--iam-instance-profile Name=myapp-secrets`

Description
===========

`init-resources` creates the following aws resources:

- A customer master key
- An alias for the key
- An S3 bucket
- A few roles to be used by an instance profile: one for S3 access, one for decryption
- A group
- An access policy for the group to get and put the key to S3.
- An access policy for the group to encrypt keys

Notes
======

- Images must have the AWS CLI installed on them.  Also they will need to have the region set,
  by setting AWS_DEFAULT_REGION



References
==========

https://www.promptworks.com/blog/handling-environment-secrets-in-docker-on-the-aws-container-service

