# Open Bucket

<b>Severity</b>: <b><font color="#DB1E54">High</font></b><br>
<b>Test name</b>: Exposed AWS S3 Buckets Details

<table id="simple-table">
    <tr>
        <th><strong>Summary</strong></th>
    </tr>
</table>

Cloud storage services allow web applications and services to store and access objects on  the storage service.  Improper configuration of access control can lead to disclosure of sensitive information and unauthorized access. Different settings allow configuring access rights at different levels. At the same time, when granting public access to objects from the storage (or the entire storage), it is necessary to understand the possible effects. In most cases, public access to the storage is the result of misconfiguration.

By default, all Amazon S3 resources (buckets, objects and other) are private. Only the resource owner (the AWS account that created it) can access the resource. The resource owner can optionally grant public access to the bucket itself as well as to individual objects stored in that bucket. This can result in an unauthorized user being able to download new files, modify or read stored files.


<table id="simple-table">
    <tr>
        <th><strong>Impact</strong></th>
    </tr>
</table>

* Data leakage
* Access to unauthorized information


<table id="simple-table">
    <tr>
        <th><strong>Location</strong></th>
    </tr>
</table>

The issue can be found in the **cloud storage configuration**.

<table id="simple-table">
    <tr>
        <th><strong>Remedy suggestions</strong></th>
    </tr>
</table>

Amazon S3 provides a number of security features to consider as you develop and implement your own security policies. Because the following  recommendations might not be appropriate or sufficient for your environment, treat them as helpful considerations rather than prescriptions.
* Ensure that your Amazon S3 buckets use the correct policies and are not publicly accessible. Unless you explicitly require anyone on the Internet to be able to read or write to your S3 bucket, you should ensure that your S3 bucket is not public. 
* Implement least privilege access. When granting permissions, you decide who is getting what permissions to which Amazon S3 resources. You enable specific actions that you want to allow on those resources. Therefore, you should grant only the permissions that are required to perform a task. 
* Use IAM roles for applications and AWS services that require Amazon S3 access. For applications on Amazon EC2 or other AWS services to access Amazon S3 resources, they must include valid AWS credentials in their AWS API requests. You should not store AWS credentials directly in the application or Amazon EC2 instance. You should use an IAM role to manage temporary credentials for applications or services that need to access Amazon S3.
* Enable multi-factor authentication (MFA) Delete. MFA Delete can help prevent accidental bucket deletions. If MFA Delete is not enabled, any user with the password of a sufficiently privileged root or IAM user could permanently delete an Amazon S3 object.




<table id="simple-table">
    <tr>
        <th><strong>Classification</strong></th>
    </tr>
</table>

* CWE-264
* CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N

<table id="simple-table">
    <tr>
        <th><strong>References</strong></th>
    </tr>
</table>

* [https://cwe.mitre.org/data/definitions/264.html](https://cwe.mitre.org/data/definitions/264.html)
* [https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/11-Test_Cloud_Storage](https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/11-Test_Cloud_Storage)
* [https://aws.amazon.com/articles/amazon-s3-bucket-public-access-considerations/](https://aws.amazon.com/articles/amazon-s3-bucket-public-access-considerations/)
