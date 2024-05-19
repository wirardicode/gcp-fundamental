# create your cloud
this is useful for storage

create bucket
--
`gsutil mb -l <<region>> gs://<<bucket-name>>`

# try to save file into bucket

upload file
--
open cloud edior then click upload file, choose some file or img

sent it to bucket
--
`gsutil cp <<file_name>> gs://<<bucket_name>>`

make it public
--
`gsutil acl ch -u AllUsers:R gs://<<bucket_name>>/<<file_name>>`

# optional
 if you want to save file with same name and type you must use object versioning

 copy this command
 --
 `gsutil versioning set on gs://<<bucket_name>>`
<br>
to make it turn off: `gsutil versioning set off gs://<<bucket_name>>`
