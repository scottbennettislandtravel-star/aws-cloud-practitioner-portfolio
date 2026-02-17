
## Debugging & Issue Resolution

### Issue Encountered
When attempting to access the static website endpoint, the following error was returned:

- 404 Not Found
- NoSuchKey: index.html

This indicated that Amazon S3 could not locate the specified object.

### Investigation Process
Initial checks confirmed:
- The file appeared to exist in the S3 console
- Static website hosting was enabled
- The correct index document was configured

To verify the actual state of the bucket, AWS CloudShell was used.

### CLI Verification
The following command was executed:

aws s3api head-object --bucket scott-s3-static-website-2026 --key index.html

This returned a 404 error, confirming that the object did not exist at the expected key.

### Resolution
The file was re-uploaded using the AWS CLI to ensure correct placement at the root of the bucket:

aws s3 cp index.html s3://scott-s3-static-website-2026/index.html --content-type text/html

After this, the object was successfully detected and the website loaded correctly.

### Key Learning
- The AWS Management Console may not always reflect the exact state of resources
- AWS CLI provides a more reliable and precise method for verifying resource existence
- S3 object keys must match exactly; even small differences result in errors
- Debugging in AWS should be based on verification, not assumptions
