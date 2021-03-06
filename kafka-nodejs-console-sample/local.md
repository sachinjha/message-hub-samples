# IBM Message Hub Kafka Node.js console sample application: Local Development guide
As pushing the application into IBM Cloud® does not require you to build the application locally, this guide is here to guide you through the process, should you wish to build the application locally.

We will not discuss establishing a connection from your laptop to Message Hub. This is described in the [ connection guide](https://console.bluemix.net/docs/services/MessageHub/messagehub127.html#connect_messagehub).

## Prerequisites (Local deployment only, for macOS and Linux)
* [Node.js](https://nodejs.org/en/) 6.X LTS
* [node-gyp] (https://www.npmjs.com/package/node-gyp)

Node-rdkafka will build librdkafka automatically. You must ensure you have the dependencies listed below installed. For more details, see [librdakfka's instructions](../docs/librdkafka.md).

##### Linux
* openssl-dev
* libsasl2-dev
* libsasl2-modules
* C++ toolchain

##### macOS 
* [Brew](http://brew.sh/)
* [Apple Xcode command line tools](https://developer.apple.com/xcode/)
* `openssl` via Brew
* Export `CPPFLAGS=-I/usr/local/opt/openssl/include` and `LDFLAGS=-L/usr/local/opt/openssl/lib`
* Open Keychain Access, export all certificates in System Roots to a single .pem file

## Installing dependencies (Local)
Run the following commands on your local machine, after the prerequisites for your environment have been completed:
```shell
npm install
```

## Running the Sample (Local - macOS and Linux only)
Once built, to run the sample, execute the following command:
```shell
node app.js <kafka_brokers_sasl> <kafka_admin_url> <api_key> <ca_location>
```

To find the values for `<kafka_brokers_sasl>`, `<kafka_admin_url>` and `<api_key>`, access your Message Hub instance in IBM Cloud®, go to the `Service Credentials` tab and select the `Credentials` you want to use.  If your user value is `token`, specify that with the password seperated by a `:`.

`<ca_location>` is the path where the trusted SSL certificates are stored on your machine and is therefore system dependent. 
For example:
* Ubuntu: /etc/ssl/certs
* RedHat: /etc/pki/tls/cert.pem
* macOS: The .pem file you created in the prerequisite section

__Note__: `<kafka_brokers_sasl>` must be a single string enclosed in quotes. For example: `"host1:port1,host2:port2"`. We recommend using all the Kafka hosts listed in the `Credentials` you selected.

Alternatively, you can run only the producer or only the consumer by respectively appending the switches `-producer` or `-consumer`  to the command above.

The sample will run indefinitely until interrupted. To stop the process, use `Ctrl+C`, for example.

## Sample Output
Below is a snippet of the output generated by the sample:

```
Topic mh-nodejs-console-sample-topic created
Existing topics:
[ { name: 'mh-nodejs-console-sample-topic',
    partitions: 1,
    retentionMs: '86400000',
    markedForDeletion: false } ]
The consumer has started
The producer has started
Topic object created with opts {"request.required.acks":-1}
Consumer obtained metadata: {"orig_broker_id":0,"orig_broker_name":"sasl_ssl://kafka01-prod01.messagehub.services.us-south.bluemix.net:9093/0","topics":[{"name":"mh-nodejs-console-sample-topic","partitions":[{"id":0,"leader":0,"replicas":[0,1,4],"isrs":[null,null,null,1]}]}],"brokers":[{"id":2,"host":"kafka03-prod01.messagehub.services.us-south.bluemix.net","port":9093},{"id":4,"host":"kafka05-prod01.messagehub.services.us-south.bluemix.net","port":9093},{"id":1,"host":"kafka02-prod01.messagehub.services.us-south.bluemix.net","port":9093},{"id":3,"host":"kafka04-prod01.messagehub.services.us-south.bluemix.net","port":9093},{"id":0,"host":"kafka01-prod01.messagehub.services.us-south.bluemix.net","port":9093}]}
Producer obtained metadata: {"orig_broker_id":0,"orig_broker_name":"sasl_ssl://kafka01-prod01.messagehub.services.us-south.bluemix.net:9093/0","topics":[{"name":"mh-nodejs-console-sample-topic","partitions":[{"id":0,"leader":0,"replicas":[0,1,4],"isrs":[null,null,null,1]}]}],"brokers":[{"id":2,"host":"kafka03-prod01.messagehub.services.us-south.bluemix.net","port":9093},{"id":4,"host":"kafka05-prod01.messagehub.services.us-south.bluemix.net","port":9093},{"id":1,"host":"kafka02-prod01.messagehub.services.us-south.bluemix.net","port":9093},{"id":3,"host":"kafka04-prod01.messagehub.services.us-south.bluemix.net","port":9093},{"id":0,"host":"kafka01-prod01.messagehub.services.us-south.bluemix.net","port":9093}]}
Message produced, offset: 1
No messages consumed
Message produced, offset: 2
Message consumed: topic=mh-nodejs-console-sample-topic, partition=0, offset=1, key=key, value=This is a test message #1
Message produced, offset: 3
Message consumed: topic=mh-nodejs-console-sample-topic, partition=0, offset=2, key=key, value=This is a test message #2
Message produced, offset: 4
Message consumed: topic=mh-nodejs-console-sample-topic, partition=0, offset=3, key=key, value=This is a test message #3
```
