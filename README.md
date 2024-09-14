# S3-Sys-Flows

This Mule Plugin contains sub-flows capable of performing Put, Get, List, Copy & Delete Object operations w.r.t. AWS S3. The intended use of this Plugin is to be added as a dependency in a Mule Project. Once added, its sub-flows can be used by the Mule Project as if they belonged to the Project itself.

One can replace small System APIs with Plugin(s) like this in their API Network and can save on Anypoint Platform costs (vCores, Workers, API Manager Instances, etc.).

## Publish To Exchange

Assuming that there is a Connected App configured in your Anypoint Platform with sufficient permissions (Scope), you'll only have to replace value of ```<groupId>``` tag with your Anypoint Platform's Org ID (or Business Group ID) in ```pom.xml```.

Then navigate to Maven settings in your AnypointStudio's Preferences and temporarily replace the existing ```Base command line for builds``` with the mvn deploy command. Example:

```
mvn clean deploy -e -Dconnectedapp_client_id=57d9208e02XXXXXXXXXXXX1fe0dbf5fe -Dconnectedapp_client_secret=Ed0C468D01XXXXXXXXXXXX66e9E23b30 -s settings.xml -DskipTests
```

## Using in Mule Project

Let's take a look at the flow variables and payload required by the sub-flows present in this Mule Plugin:

### put-object

```vars.s3Bucket``` - S3 Bucket name

```vars.s3ObjectKey``` - Object key (fully qualified file name)

```payload``` - File content

### fetch-object

```vars.s3Bucket``` - S3 Bucket name

```vars.s3ObjectKey``` - Object key (fully qualified file name)

### list-objects

```vars.s3Bucket``` - S3 Bucket name

### copy-object

```vars.s3SourceBucket``` - Source bucket name

```vars.s3SourceObjectKey``` - Source object key (fully qualified file name)

```vars.s3DestinationBucket``` - Destination bucket name

```vars.s3DestinationObjectKey``` - Destination object key (fully qualified file name)

### delete-object

```vars.s3Bucket``` - S3 Bucket name

```vars.s3ObjectKey``` - Object key (fully qualified file name)

## Note:

Some properties need to be provided by the Mule Project where this plugin is being used.

Example YAML snippet:

```
aws:
  s3:
    region: "dummy"
    role:
      arn: "dummy"
      duration: "3600" # in seconds
    accessKey: "dummy"
    secretKey: "dummy"
    connectionTimeout: "30" # in seconds
    responseTimeout: "30" # in seconds
    maxConnections: "-1"
    reconnection:
      frequency: "2000" # in milliseconds
      attempts: "2"
```

___

### Supporting links:

[Blog Article](https://www.loveleshkalonia.com/2024/09/reduce-anypoint-costs-use-shared-flows-instead-of-system-api.html)