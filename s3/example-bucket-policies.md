# AWS S3 - SITE PUBLIC

* https://docs.aws.amazon.com/es_es/AmazonS3/latest/dev/example-bucket-policies.html
* https://www.youtube.com/watch?v=uPnk8p3Glzg

```
{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Sid":"PublicRead",
      "Effect":"Allow",
      "Principal": "*",
      "Action":["s3:GetObject"],
      "Resource":["arn:aws:s3:::examplebucket/*"]
    }
  ]
}
```
