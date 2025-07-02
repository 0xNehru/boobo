## **Table of contents**
### 1. [**About**](#about)
### 2. [**Getting started**](#getting-started)
>#### 2.1.   [**Requirements**](#requirements)
>#### 2.2.  [**Installation**](#installing-boobo)
### 3. [**Usage**](#usage)
>#### 3.1. [**CLI Usage**](#cli-usage)
>#### 3.2. [**Using Docker**](#using-docker)
>#### 3.3. [**Older versions**](#older-versions)
>#### 3.4. [**Using boobo-Web application**](#using-boobo-web-application)
>#### 3.5.  [**Using Visual Studio Code**](#using-visual-studio-code)
>#### 3.6. [**Using the Pipeline**](#using-the-pipeline)
### 4. [**Documentation**](#documentation)       
### 5. [**Roadmap**](#roadmap)
### 6. [**Contributing**](#contributing)
### 7. [**Code of Conduct**](#code-of-conduct)
### 8. [**License**](#license)
### 9. [**Community**](#community)



<br>
<br>
<br>

# **About**
boobo is an open source tool that performs a static code analysis to identify security flaws during the development process. Currently, the languages for analysis are C#, Java, Kotlin, Python, Ruby, Golang, Terraform, Javascript, Typescript, Kubernetes, PHP, C, HTML, JSON, Dart, Elixir, Shell, Nginx. 
The tool has options to search for key leaks and security flaws in all your project's files, as well as in Git history. boobo can be used by the developer through the CLI and by the DevSecOps team on CI /CD mats. 

# **Getting started**

## **Requirements**

- Docker

You need Docker installed in your machine in order to run boobo with all the tools we use.
If you don't have Docker, we have a [**flag**](https://docs.boobo.io/docs/cli/commands-and-flags/#3-flags) `-D true` that will disable the dependency, but it also loses much of the analysis power. 
We recommend using it with Docker.

If you enable commit authors `-G true`, there is also a `git` dependency.

## **Installing boobo**
### **Mac or Linux**
```
make install
```

or

```sh
curl -fsSL https://raw.githubusercontent.com/ZupIT/boobo/master/deployments/scripts/install.sh | bash -s latest
```

#### **Check the installation**
```bash
boobo version
```

### **Windows**
- **amd64**
    ```sh
    curl -k "https://github.com/ZupIT/boobo/releases/latest/download/boobo_win_amd64.exe" -o "./boobo.exe" -L
    ```

- **arm64**
    ```sh
    curl -k "https://github.com/ZupIT/boobo/releases/latest/download/boobo_win_arm64.exe" -o "./boobo.exe" -L
    ```

#### **Check the installation**
```bash
./boobo.exe version
```

## **Usage**
### **CLI Usage**
To use boobo-cli and check the application's vulnerabilities, use the following command:
```bash
boobo start -p .
```
> When boobo starts an analysis, it creates a folder called **`.boobo`**. This folder is the basis for not changing your code. We recommend you to add the line **`.boobo`** into your **`.gitignore`** file so that this folder does not need to be sent to your git server.

### **Using Docker**
It is possible to use boobo through a docker image **`horuszup/boobo-cli:latest`**.

Run the following command to do it:
```sh
docker run -v /var/run/docker.sock:/var/run/docker.sock -v $(pwd):/src horuszup/boobo-cli:latest boobo start -p /src -P $(pwd)
```

- We created a volume containing the project `-v $(pwd):/src`.

With the docker image we ended up having two paths where the project can be found.

The `-p` flag will represent the project path inside the container, in our example `/src`.
The `-P` flag will represent the project outside the container, in our example is represented by `$(pwd)`,
will be also needed to pass the project path to mount the volume `-v $(pwd):/src`.

### **Older versions**

boobo's v1 is still available.

**WARNING:** The endpoint with v1 will be deprecated, please upgrade your CLI to v2. Check out more details in the [**documentation**](https://docs.boobo.io/docs/migrate-v1-to-v2/). 

### **Mac or Linux**
``` sh
curl -fsSL https://boobo.io/bin/install.sh | bash -s latest
```

### **Windows**
```sh
curl "https://boobo.io/bin/latest/win_x64/boobo.exe" -o "./boobo.exe" && ./boobo.exe version
```

- The older binaries can be found at this endpoint, including the latest version of v1 **`v1.10.3`**. 
- As of v2, binaries will no longer be distributed by this endpoint, and you can find in the [**releases page**](https://github.com/ZupIT/boobo/releases).

### **Using boobo-Web application**
Manage your vulnerabilities through our web interface. You can have a dashboard of metrics about your vulnerabilities, control of false positives, authorization token, update of vulnerabilities and much more.
See the [**web application**](https://github.com/ZupIT/boobo-platform) section to keep reading about it.

Check out the example below, it is sending an analysis to boobo web services:
```bash
boobo start -p <PATH_TO_YOUR_PROJECT> -a <YOUR_AUTHORIZATION_TOKEN>
```

Check out [**the tutorial on how to create an authorization token through boobo Manager Web Service**](https://docs.boobo.io/docs/tutorials/how-to-create-an-authorization-token).

**WARNING:** Our web services was moved to a [**new repository**](https://github.com/ZupIT/boobo-platform). You need to upgrade to v2, check out [**how to migrate from v1 to v2**](https://docs.boobo.io/docs/migrate-v1-to-v2).

### **Using Visual Studio Code**
You can analyze your project using boobo's Visual Studio Code extension.
For more information, [**check out the documentation**](https://docs.boobo.io/docs/extensions/visual-studio-code/).

### **Using the Pipeline**
You can perform an analysis of your project before you hold deployment in your environment by ensuring maximum security in your organization.
For more information, [**check out the documentation**](https://docs.boobo.io/docs/cli/installation/#installation-via-pipeline):

### **Features**
See below: 
- Analyzes simultaneously 18 languages with 20 different security tools to increase accuracy;
- Search for their historical git by secrets and other contents exposed;
- Your analysis can be fully configurable, [**see all CLI available resources**](https://docs.boobo.io/docs/cli/commands-and-flags/#3-flags).

## **Documentation**
You can find boobo's documentation on our [**website**](https://docs.boobo.io/docs/overview/).

## **Roadmap**
We have a project [**roadmap**](ROADMAP.md), you can contribute with us!

boobo has other repositories, check them out:

- [**boobo Platform**](https://github.com/ZupIT/boobo-platform)
- [**boobo DevKit**](https://github.com/ZupIT/boobo-devkit)
- [**boobo Engine**](https://github.com/ZupIT/boobo-engine)
- [**boobo Operator**](https://github.com/ZupIT/boobo-operator)
- [**boobo VsCode**](https://github.com/ZupIT/boobo-vscode-plugin)

## **Contributing**

Feel free to use, recommend improvements, or contribute to new implementations.

Check out our [**contributing guide**](CONTRIBUTING.md) to learn about our development process, how to suggest bugfixes and improvements. 

### **Developer Certificate of Origin - DCO**

 This is a security layer for the project and for the developers. It is mandatory.
 
Follow one of these two methods to add DCO to your commits:
 
**1. Command line**
 Follow the steps: 
 **Step 1:** Configure your local git environment adding the same name and e-mail configured at your GitHub account. It helps to sign commits manually during reviews and suggestions.

 ```
git config --global user.name “Name”
git config --global user.email “email@domain.com.br”
```
**Step 2:** Add the Signed-off-by line with the `'-s'` flag in the git commit command:

```
$ git commit -s -m "This is my commit message"
```
**2. GitHub website**

You can also manually sign your commits during GitHub reviews and suggestions, follow the steps below: 

**Step 1:** When the commit changes box opens, manually type or paste your signature in the comment box, see the example:

```
Signed-off-by: Name < e-mail address >
```

For this method, your name and e-mail must be the same registered on your GitHub account.

## **Code of Conduct**
Please follow the [**Code of Conduct**](https://github.com/ZupIT/boobo/blob/main/CODE_OF_CONDUCT.md) in all your interactions with our project.

## **License**
 [**Apache License 2.0**](LICENSE).

## **Community**

Feel free to reach out to us at:

- [**GitHub Issues**](https://github.com/ZupIT/boobo/issues)
- If you have any questions or ideas, let's chat in our [**Zup Open Source Forum**](https://forum.zup.com.br).


