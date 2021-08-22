# S3

## What is Amazon S3?

* Amazon Simple Storage Service (Amazon S3) is storage for the Internet. It is designed to make web-scale computing easier.
* Amazon S3 has a simple web services interface that you can use to store and retrieve any amount of data, at any time, from anywhere on the web.

***Advantages of using Amazon S3***

1. Creating buckets – Create and name a bucket that stores data. Buckets are the fundamental containers in Amazon S3 for data storage.
2. Storing data – Store an infinite amount of data in a bucket. Upload as many objects as you like into an Amazon S3 bucket.
3. Downloading data – Download your data or enable others to do so.
4. Permissions – Grant or deny access to others who want to upload or download data into your Amazon S3 bucket.
5. Standard interfaces – Use standards-based REST and SOAP interfaces designed to work with any internet-development toolkit.

***Amazon S3 concepts***

1. Buckets :

* A bucket is a container for objects stored in Amazon S3.
* Every object is contained in a bucket.

* Buckets serve several purposes:
  * They organize the Amazon S3 namespace at the highest level.
  * They identify the account responsible for storage and data transfer charges.
  * They play a role in access control.
  * They serve as the unit of aggregation for usage reporting.

2. Objects

* Objects are the fundamental entities stored in Amazon S3.
* Objects consist of object data and metadata. The data portion is opaque to Amazon S3.

3. Keys

* A key is the unique identifier for an object within a bucket.
* Every object in a bucket has exactly one key.

4. Regions

* You can choose the geographical AWS Region where Amazon S3 will store the buckets that you create.

***Amazon S3 data consistency model***

* Amazon S3 provides strong read-after-write consistency for PUTs and DELETEs of objects in your Amazon S3 bucket in all AWS Regions.
* Updates to a single key are atomic.
* Amazon S3 achieves high availability by replicating data across multiple servers within AWS data centers. If a PUT request is successful, your data is safely stored.

***Amazon S3 features***

1. Storage classes

* Amazon S3 offers a range of storage classes designed for different use cases.

2. Bucket policies

* Bucket policies provide centralized access control to buckets and objects based on a variety of conditions, including Amazon S3 operations, requesters, resources, and aspects of the request (for example, IP address).
* The policies are expressed in the access policy language and enable centralized management of permissions.
* Only the bucket owner is allowed to associate a policy with a bucket.

3. AWS Identity and Access Management

* You can use AWS Identity and Access Management (IAM) to manage access to your Amazon S3 resources.

4. Access control lists

* You can control access to each of your buckets and objects using an access control list (ACL).

5. Versioning

* You can use versioning to keep multiple versions of an object in the same bucket.

6. Operations

* Following are the most common operations that you'll run through the API.

* Common operations : 

1. Create a bucket – Create and name your own bucket in which to store your objects.
2. Write an object – Store data by creating or overwriting an object. When you write an object, you specify a unique key in the namespace of your bucket.
3. Read an object – Read data back. You can download the data via HTTP.
4. Delete an object – Delete some of your data.
5. List keys – List the keys contained in one of your buckets. You can filter the key list based on a prefix.

***Amazon S3 application programming interfaces (API)***

* The Amazon S3 architecture is designed to be programming language-neutral, using AWS Supported interfaces to store and retrieve objects.
* Amazon S3 provides a REST and a SOAP interface.
* They are similar, but there are some differences.

***The REST interface***

* The REST API is an HTTP interface to Amazon S3. Using REST, you use standard HTTP requests to create, fetch, and delete buckets and objects.
* You can use any toolkit that supports HTTP to use the REST API. You can even use a browser to fetch objects, as long as they are anonymously readable.

***The SOAP interface***

* The SOAP API provides a SOAP 1.1 interface using document literal encoding. The most common way to use SOAP is to download the WSDL.

## implementation for S3

* execute the command:  ***amplify add storage***
* then ***amplify push***

***require dependencies***

```
 implementation 'com.amplifyframework:aws-storage-s3:1.24.0'
 implementation 'com.amplifyframework:aws-auth-cognito:1.24.0'
```

***Initialize Amplify Storage***

```
Amplify.addPlugin(new AWSCognitoAuthPlugin());
Amplify.addPlugin(new AWSS3StoragePlugin());
```

***Uploading data to your bucket***

```
private void uploadFile() {
    File exampleFile = new File(getApplicationContext().getFilesDir(), "ExampleKey");

    try {
        BufferedWriter writer = new BufferedWriter(new FileWriter(exampleFile));
        writer.append("Example file contents");
        writer.close();
    } catch (Exception exception) {
        Log.e("MyAmplifyApp", "Upload failed", exception);
    }

    Amplify.Storage.uploadFile(
            "ExampleKey",
            exampleFile,
            result -> Log.i("MyAmplifyApp", "Successfully uploaded: " + result.getKey()),
            storageFailure -> Log.e("MyAmplifyApp", "Upload failed", storageFailure)
    );
}
```
