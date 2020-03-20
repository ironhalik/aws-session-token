# aws-session-token
A (relatively) simple Bash function for getting AWS session tokens when using aws cli with MFA.

## In short
```
$ aws s3 ls
Unable to locate credentials. You can configure credentials by running "aws configure".
$ AWS_PROFILE=some-aws-account aws s3 ls
An error occurred (AccessDenied) when calling the ListBuckets operation: Access Denied
$ aws-session-token --profile some-aws-account --token 883759 # see usage
Session with some-aws-account opened.
$ aws s3 ls
2020-02-11 11:36:35 some-some-aws-account-bucket
[...]
$ aws-session-token some-other-aws-account 642453
Session with some-other-aws-account opened.
```

The function exports following variables to your shell (some of which are sensitive):
- `AWS_PROFILE`
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_SESSION_TOKEN`

## Installation
Add the contents of aws-session-token to your .bashrc (or source it however you want :))

## Usage
```
Generates and sets AWS session token when using awscli with MFA.
You need to provide AWS profile name (as defined in ~/.aws/config)
and OTP token generated by your MFA device.

Usage:
  aws-session-token --profile <aws-profile> --token <token>
  aws-session-token --profile <aws-profile> <token>
  aws-session-token <aws-profile> <token>
  AWS_PROFILE=<aws-profile> aws-session-token --token <token>
  AWS_PROFILE=<aws-profile> aws-session-token <token>
```
