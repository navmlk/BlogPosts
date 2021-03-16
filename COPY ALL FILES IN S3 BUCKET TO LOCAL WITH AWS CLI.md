The AWS CLI makes working with files in S3 very easy. However, the file globbing available on most Unix/Linux systems is not quite as easy to use with the AWS CLI. 
_S3 doesn’t have folders, but it does use the concept of folders by using the “/” character in S3 object keys as a folder delimiter.

To copy all objects in an S3 bucket to your local machine simply use the `aws s3 cp command` with the `--recursive` option.

For example `aws s3 cp s3://temp-bucket/ ./ --recursive` will copy all files from the “big-datums-tmp” bucket to the current working directory on your local machine. If there are folders represented in the object keys (keys containing “/” characters), they will be downloaded as separate directories in the target location.

The command `aws s3 cp s3://temp-bucket/folder1/ ./ --recursive` is almost the same as the one above, but this command will only copy files from “myFolder” folder (objects with keys starting with “myFolder/”).

For using wildcards and patterns to copy only certain files, refer to [Using Wildcards with AWS CLI](https://sysadmindiary.co.uk/index.php/2020/01/06/using-unix-wildcards-with-aws-s3-aws-cli/) on how to correctly use the `--include` and `--exclude` options.
