**Currently AWS CLI doesn’t provide support for UNIX wildcards in a command’s “path” argument. However, it is quite easy to replicate this functionality using the `--exclude` and `--include` parameters available on several aws s3 commands.**

The wildcards available for use are:
- `"*"` – Matches everything
- `"?"` – Matches any single character
- `"[]"` – Matches any single character between the brackets
- `"[!]"` – Matches any single character not between the brackets

A few things to remember about using `--include` and `--exclude` with the `aws s3` command:You may use any number of `--include` and `--exclude` parameters.Parameters passed later take precedence over parameters passed earlier (in the same command). All files and objects are “included” by default, so in order to include only certain files you must use “exclude” then “include”. `--recursive` must be used in conjunction with `--include` and `--exclude` or else commands will only perform single file/object operations.

#### Examples: ####


#Copy all files from working directory to the temp-bucket1 bucket:
```aws
aws s3 cp ./ s3://temp-bucket1/ --recursive
```
 
#Delete all ".json" files from the temp-bucket1 bucket:
```aws
aws s3 rm s3://temp-bucket1/ --recursive --exclude "*" --include "*.json"
```
 
#Delete all files in the temp-bucket1 bucket with a file extension beginning #with "c" or "t" (".txt", ".config" etc.):
```aws
aws s3 rm s3://temp-bucket1/ --recursive --exclude "*" --include "*.[ct]*"
```
 
#Copy ".txt" and ".csv" files from temp-bucket1 S3 bucket to local working directory:
```aws
aws s3 cp s3://temp-bucket1/ . --recursive --exclude "*" --include "*.txt" --include "*.csv"
```
