# AWS Basic Command

## Credential
1. aws configure
2. aws configure --profile hunseol

## S3
3. aws s3 sync ./.out-storybook s3://$BUCKET_NAME/$DATE/$CURRENT_BRANCH_NAME --profile hunseol
4. aws s3 ls s3://$BUCKET_NAME --profile hunseol

## References
[S3 Basic command](https://aws.amazon.com/ko/getting-started/tutorials/backup-to-s3-cli/)