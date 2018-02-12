# S3

## S3 Examples
1. Create Bucket with `Node JS`
```typescript
import * as AWS from 'aws-sdk';

const myBucket = 'new-test-bucket';
const accessKeyId = 'accessKeyId';
const secretAccessKey = 'secretAccessKey';
const region = 'ap-northeast-2';

const s3 = new AWS.S3({ accessKeyId, secretAccessKey, region });
s3.createBucket({
  Bucket: myBucket,
}, (err, data) => {
  if (err) {
    console.log(err);
  } else {
    const params = { Bucket: myBucket, Key: accessKeyId, Body: 'Hello S3!!' };
    s3.putObject(params, () => {
      if (err) {
        console.log(err);
      } else {
        console.log('Successfully Uploaded data to myBuket/myKey');
      }
    });
  }
});
```

2. Put Objects with `AWS Command`
```bash
aws s3 sync ./out-storybook s3://$BUCKET_NAME/$DATE/$CURRENT_BRANCH_NAME --profile hunseol

```

3. Delete Objects with `AWS Command`
```bash
aws s3 rm s3://$BUCKET_NAME/$DATE/$CURRENT_BRANCH_NAME --profile hunseol
```

## References
- [AWS Official Commands](https://docs.aws.amazon.com/cli/latest/index.html)
- [AWS Command Line Interface에서 상위 수준 s3 명령 사용](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/using-s3-commands.html)
- [S3 Basic command](https://aws.amazon.com/ko/getting-started/tutorials/backup-to-s3-cli/)
