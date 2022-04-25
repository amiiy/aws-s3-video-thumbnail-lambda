## AWS create thumbnail for uploaded video on the S3

this is a sample ready to use code that created by (aws sam)[https://aws.amazon.com/serverless/sam/]
basically once you run `sam build` and `sam deploy` the (cloudFormation)[https://aws.amazon.com/cloudformation]will create do the following steps:

- create a lambda functino with prefix name: `aws-s3-thumbnail-S4VideoThumbnail-****` (you can specify `FunctionName in template.yml file)
- create a S3 bucket with specified parameter name: `AppBucketName` ( pass it using: `sam deploy --parameter-overrides AppBucketName=some-thing-unique-123`)
- create required IAM execution roles for the lambda
- grant read and write access for the lambda function to perform operation on that s3 bucket
- add an event trigger to lamba for putObject on S3
- add ffempeg lib layer to the lambda function, in order to do this, you need to first deploy (this)[https://serverlessrepo.aws.amazon.com/applications/us-east-1/145266761615/ffmpeg-lambda-layer] then add the layer Arn in the template.yml file

## NOTE

in the template I put event only on the `videos` directory and inside the lambda it will save the images in thumbnail folder in the same s3 bucket. if you write and read from same bucket without prefix or folder you may endup in infinit recursive lambda calls! its created millons of object for me in just couple of minutes!
