
# Cloudfront
TODO
- What is Clooudfront: CDN distrubution, cache resource in egde location
- Use case
- work as CDN for S3 Hosting static

- Can restrict to specified region
- Can configure cache rule for specified object
- Can custom CNAME
- Can create invalidation



Lamda@Edge
- intercept request and response
- authorization and authenication
- redirect request

Tips
- To forward all request of cloudfront to S3 Hosting Static, you need to custom error 401 and 403 to redirect Default root object of s3