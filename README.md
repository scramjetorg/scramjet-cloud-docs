# **Scramjet Transform Hub - Quick Start introduction**

<p align="center">
    <a href=https://github.com/scramjetorg/scramjet-cloud-docs/blob/main/LICENSE>
        <img src="https://img.shields.io/badge/license-MIT-green?color=green&style=plastic" alt="GitHub license"/></a>
    <a href=https://github.com/scramjetorg/scramjet-cloud-docs/stargazers>
        <img src="https://img.shields.io/github/stars/scramjetorg/scramjet-cloud-docs?color=pink&style=plastic" alt="GitHub stars" /></a>
    <a href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=7F7V65C43EBMW">
        <img src="https://img.shields.io/badge/Donate-PayPal-green.svg?color=yellow&style=plastic" alt="Donate" /></a>
    <a href="https://scramjet.org/">
        <img src="https://img.shields.io/badge/www-scramjet-2d71c5?style=plastic" alt="Slack"/></a>
    <a href="https://join.slack.com/t/scramjetorg/shared_invite/zt-bb16pluv-XlICrq5Khuhbq5beenP2Fg">
        <img src="https://img.shields.io/badge/slack-purple.svg?style=plastic&logo=slack&logoColor=white"/></a>
    <a href="https://www.linkedin.com/company/scramjet/">
        <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=plastic&logo=linkedin&logoColor=white" alt="Slack"/></a>
</p>
<p align="center">⭐ Star us on GitHub — it motivates us a lot! 🚀 </p>
<p align="center">
    <img src="https://assets.scramjet.org/sth-logo.svg" alt="Scramjet Transform Hub Logo">
</p> 

> :bulb: **Note**: This repository contains introductory documentation and code samples for Scramjet Transform Hub. 

* Developers looking for source code repository should visit the following link [https://github.com/scramjetorg/transform-hub](https://github.com/scramjetorg/transform-hub).
* You can also find our packages published in NPM: 
  * STH [https://www.npmjs.com/package/@scramjet/sth](https://www.npmjs.com/package/@scramjet/sth)
  * CLI [https://www.npmjs.com/package/@scramjet/cli](https://www.npmjs.com/package/@scramjet/cli)
---
## **Table of Contents**

1. [What is Scramjet Transform Hub (STH)?](#1-what-is-scramjet-transform-hub-STH-?)
2. [Solution concept diagram](#2-solution-concept-diagram)
    - [Inputs](#21-inputs)
    - [Host](#22-host)
    - [Outputs](#23-outputs)
3. [Install Scramjet Transform Hub](#3-install-scramjet-transform-hub)
    - [Prepare environment](#31-prepare-environment)
    - [Install STH](#32-install-sth)
4. [Run your first sequence](#4-run-your-first-sequence)
    - [Review the package](#41-review-the-package)
    - [Prepare and send sequence package](#42-prepare-and-send-sequence-package)
    - [Run the sequence](#43-run-the-sequence)
    - [Send data to the sequence](#44-send-data-to-the-sequence)
5. [Where to go next](#5-where-to-go-next)

---
## **1. What is Scramjet Transform Hub (STH)**

Scramjet Transform Hub allows you to deploy and run multiple data processing apps called sequences. 

> **Sequences** are specific apps, not just any apps. They specialize in efficient data processing.

STH can be treated both as data processing engine and execution platform for multiple sequences running on the same platform and performing various data processing tasks. 

We named our apps "sequences" and that term describes well its nature, as they process data through a sequence of chained functions. Therefore, usually our sequences are concise, easy to write and powerful at the same time.

Our vanilla STH engine is based on Node.js and thus allows developers to benefit from rich ecosystem, numerous packages and solutions provided by this vibrant community.

The core part of our STH engine is called the "host". 
> **Host** is responsible for maintaining and deploying sequences, keeping them running and managing its lifecycle. 

Host exposes also its own REST API to provide and receive data and manage sequences and host itself.

What we also do on the host level is that we apply a set of algorithms to optimize and speed up data processing execution in sequences. 
> We call our processing optimization algorithms **"IFCA"** meaning "Intelligent Function Composition Algorithms". 

You can interact with host using our dedicated STH CLI that will help you with sequences deployment, running it and monitoring.


## **2. Solution concept diagram**

<img src="./images/sth-diagram.png" width="85%"/>

### **2.1 Inputs**
1. STH can handle any input that can be handled by Node.js application. 
2. You, as a developer, are free to process variety of inputs in your sequence applications, such as: Text, JSON, XML, SOAP, Audio, Video and more.
3. Inputs can be either:
    * Provided to STH via its REST API; or
    * Consumed from various local or remote sources by the app; such as: Stream, STDIN, File, API, URL
    * Generated by the app itself

### **2.2 Host**
This is a solution for the central processing and management unit with the following major components:

1.  **Sequences** - these are the actual "STH" apps. It is a gzipped package (`*.tar.gz`) containing at least two files:
    * **package.json** - JSON manifest file describing the app and its configuration; such as main file to run
    * **main file** - file such as `index.js` or `index.ts` that contains a lightweight application business logic.
2. **Instance** - once a sequence is run, the host will create a separate runtime environment for it and will execute sequence code inside this runtime entity. This is an instance.
3. **API & CLI** - our Application Programming Interface and CLI connecting to it allows both for **Data operations** (sending input data and receiving output data) and **Management operations** (manage host itself and its entities: sequences or instances)

### **2.3 Outputs**
Our engine outputs can be managed in several ways: 

* **File** - you can save your output to a local or a remote file
* **STDOUT** - output can be directed to system STDOUT (STDERR is supported as well)
* **API** - output can be consumed from our  STH REST API
* **URL Request** - you can write your app in a way to request URL, webhook etc
* **Stream** - output can be streamed to a particular destination
* you can mix multiple actions together: you can both send data to remote system/URL and save it locally.

## **3. Install Scramjet Transform Hub**
### **3.1 Prepare environment**
In order to install Scramjet Transform Hub, please follow these 3 steps:
1. Get Linux machine (local UNIX/Linux OS, cloud VM etc)
2. Install Docker on this Linux machine ([official Docker instructions are here](https://docs.docker.com/get-docker/)) 
3. Install npm on this machine ([official instructions are here](https://nodejs.org/)). Currently we recommend Node.js version 16.x LTS.
### **3.2 Install STH**
Open one Linux terminal window and issue following commands:

**1. Install Scramjet Transform Hub and  STH CLI:**
```
npm i -g @scramjet/sth @scramjet/cli
```
**2. Run STH:**
```
scramjet-transform-hub
```
## **4. Run your first sequence**
### **4.1 Review the package**

> :bulb: **Note:** all commands here are executed from the root of this repository.

We have prepared for you a simple sample sequence "hello-snowman". This sequence is available in the directory `samples/hello-snowman` in this repository.
In this directory you will find two files:

* `package.json` - manifest file that describes this particular sequence
* `index.js` - file containing main application logic.

This particular application is written in plain JavaScript to simplify this example. However, you can also write your sequences in TypeScript and build them before packaging and sending sequence to STH.

In the template's [readme](templates/README.md) you will find a more specific descriptions of the particular file's content.

There is no need to change anything in our `hello-snowman` sequence for a first run. Let's move to the next step.

### **4.2 Prepare and send sequence package**

Our "sequence" apps need to be packaged before sending to Transform Hub. Package is a simple TAR archive and our STH CLI has a special command to pack an app directory into a sequence tarball.

> :bulb: **Note:** any time, you can display STH CLI help by issuing terminal command `si help` (for general help) or `si <command> help` for specific command (ie. `si sequence help`)

Please open new terminal window (and keep the first one open with STH running). Then issue following commands in the root directory of this repository:

a) pack directory `hello-snowman` into archive `hello-sequence.tar.gz`:

    si pack ./samples/hello-snowman/ -o ./samples/hello-snowman.tar.gz

There is no output shown in the terminal but you can verify with `ls` that tarball package is created inside `samples` directory.

b) send `hello-snowman.tar.gz` to the running host (default localhost API endpoint will be used by the CLI send command):

    si sequence send ./samples/hello-snowman.tar.gz

> :bulb: **Note:** if you receive reply: **Request ok: http://127.0.0.1:8000/api/v1/sequence status: 422 Unprocessable Entity**, it means that STH Docker images are not yet pulled from DockerHub. Please wait 2-3 minutes and try to issue `si sequence send` command again. We are working on fixing this issue in the next STH release.

The output will look similar to this one:

```bash
Request ok: http://127.0.0.1:8000/api/v1/sequence status: 202 Accepted
SequenceClient {
  _id: 'cf775cc1-105b-473d-b929-6885a0c2182c',
  host: HostClient {
    apiBase: 'http://127.0.0.1:8000/api/v1',
    client: ClientUtils {
      apiBase: 'http://127.0.0.1:8000/api/v1',
      log: [Object]
    }
  },
  sequenceURL: 'sequence/cf775cc1-105b-473d-b929-6885a0c2182c'
}
```
Now we have uploaded sequence to the host and host assigned to it a random ID (GUID), in my case our sequence ID is:

 `_id: 'cf775cc1-105b-473d-b929-6885a0c2182c'`
 
 Host also exposes REST API endpoint for each sequence and this is also described in this response.

### **4.3 Run the sequence**

We can now use sequence ID to run this uploaded sequence. The command is `si seq start <sequence_id>`. You can also pass arbitrary number of parameters by providing them after `<sequence_id>`, in case of our `hello-snowman` parameters are not used.
For example for the above sequence we could write:

    si sequence start cf775cc1-105b-473d-b929-6885a0c2182c


The output will look similar to this one:

```bash
Request ok: http://127.0.0.1:8000/api/v1/sequence/cf775cc1-105b-473d-b929-6885a0c2182c/start status: 200 OK
InstanceClient {
  host: HostClient {
    apiBase: 'http://127.0.0.1:8000/api/v1',
    client: ClientUtils {
      apiBase: 'http://127.0.0.1:8000/api/v1',
      log: [Object]
    }
  },
  _id: 'e70222d1-acfc-4e00-b046-4a3a9481c53b',
  instanceURL: 'instance/e70222d1-acfc-4e00-b046-4a3a9481c53b'
}
```

Sequence is an app template. Once it is up and running, it will become a new instance. Instance also receives its own ID (GUID). In this case instance ID is:

`_id: 'e70222d1-acfc-4e00-b046-4a3a9481c53b'`

Of course, sequences can be run multiple times. Each run will create a separate instance with a distinct instance ID.

### **4.4 Send data to the sequence**

We want to make your life easier and for this very example, we have prepared a special Node.js app that will generate a stream of simple messages and send them to our running instance of `hello-snowman`.

For fun, our stream generator will send simple text messages containing temperature readings from artificial weather station. Temperature value will be generated randomly in range of <-50,50> degrees Celsius.
Our `hello-snowman` app will read and interpret these messages and will inform us about state of our Snowman:

- if temperature will be 0 or below, sequence will return message: `Snowman is freezing ... :)`
- in the other case (temperature above 0 degrees), sequence will return message: `Snowman is melting! :(`

To run this app, please execute the following command from the root of our directory `node ./tools/stream-gen-tool/stream-gen.js <instance_id>`. In our case this would look like this:

    node ./tools/stream-gen-tool/stream-gen.js e70222d1-acfc-4e00-b046-4a3a9481c53b


The output will look similar to this one:

```bash
----------------------------------------
Message# 1 | Temperature measure
INPUT | 41
OUTPUT| Snowman is melting! :(
----------------------------------------
Message# 2 | Temperature measure
INPUT | -33
OUTPUT| Snowman is freezing ... :)
----------------------------------------
Message# 3 | Temperature measure
INPUT | -36
OUTPUT| Snowman is freezing ... :)
----------------------------------------
```

Our sequence generator app does two things here:

- Sends stream of messages; each one containing number with temperature value
- Reads output from Host API that is generated by our `hello-snowman` sequences

Separately, you can also open a new terminal window and see log of this particular instance with command `si instance log <instance_id>`. In our case this would be:

    si instance log e70222d1-acfc-4e00-b046-4a3a9481c53b

The sample output will be similar to this one:

```bash
...
2021-08-09T04:29:39.790Z log (object:Runner) Input message <Buffer 32 30>
2021-08-09T04:29:40.791Z log (object:Runner) Input message <Buffer 2d 34>
2021-08-09T04:29:41.792Z log (object:Runner) Input message <Buffer 33 33>
2021-08-09T04:29:42.798Z log (object:Runner) Input message <Buffer 2d 34 35>
2021-08-09T04:29:43.801Z log (object:Runner) Input message <Buffer 2d 33 36>
...
```


> Congratulations! :clap::clap::clap: You have run your first Scramjet Transform Hub sequence! 

## **5. Where to go next**
Here you can find more resources related to Scramjet Transform Hub:
- [Check out more samples](samples) :books: - we have prepared some ready-to-use apps, which you can either use as a starting point for creating your own sequences or simply run them just to see what they do, and how the STH works with them.
- [Start from our app templates](templates) :file_folder: - almost  a blank file structure (package) and usage instructions, ready to be used as a starting point for building your own sequences. This is the simplest base we can provide for you to start with.
- [Contribute to STH development](https://github.com/scramjetorg/transform-hub) :construction_worker: - please feel free to contribute to STH development by submitting pull requests or creating issues.
- [Visit our Scramjet.org page](https://scramjet.org) :globe_with_meridians: - check out our website for more information about our Scramjet team, history and products.

---

### Thank you for reading! We hope you enjoyed it, if not here is a random cheer up joke, that may make you smile :smile: !
![Jokes Card](https://readme-jokes.vercel.app/api)