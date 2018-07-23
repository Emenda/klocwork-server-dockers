# EMENDA Dockerfile for Klocwork

This repository gives you Dockerfiles for Klocwork Server(static analysis tools for C/C++, Java, C# for quality and security) to help you in the deployment of your Klocwork environment.

## What is Klocwork?

The Klocwork analysis engine is the culmination of over 15 years of static analysis research. At the core of its technology is the ability to monitor the lifecycles of objects and infer their run time behaviour without executing the code. This allows a broad range of quality, reliability, security, and maintainability issues to be identified, with high accuracy.<br>
<img src="http://emenda.com/imgs/emenda-logo.svg" height="200" width="200" title = "Emenda" alt = "Emenda"><br>
<img src="https://image.noelshack.com/fichiers/2018/10/1/1520246980-klocwork.png" height="100" width="200" title = "Klocwork" alt = "Klocwork">



## Quick reference

### Where to get help
* [Docker forum](https://forums.docker.com/)
* [Emenda forum](http://emenda.com/)

### Supported architecture:
amd64

## How to use images?

### Prerequisites
* Have administrative rights
* Have an available internet connexion
* Download **Docker** from [official website](https://www.docker.com/community-edition#/download  "Docker official website") and install it by following the instructions
* Have a valid Klocwork installer (Contact [Emenda](http://emenda.com/))
* Have a valid Klocwork license (Contact [Emenda](http://emenda.com/))
 	
### Configure the Docker file
* Download your dockerfile for your favorite environment
* Edit the dockerfile with your favorite editor and update
	* KW database port
	* KW server port (to access server with the browser)
	* KW license port (server license port)
	* KW installer path (server install directory)
	* KW project root (path of your project root)
	* KW installer path (path of the installer archive)
	* KW license file (path of your license file)

*Example: (update bold values in Dockerfile)* 
> ARG DATABASE\_PORT=**3123**  
> ARG KW\_PORT=**8123**  
> ARG LICENSE\_PORT=**27000**  
> ARG INSTALLER\_PATH=**/opt/Klocwork**  
> ARG INSTALL\_DIRECTORY=**/opt/Klocwork/Server**  
> ARG PROJECTS\_ROOT=**/opt/Klocwork/Projects\_root\_12\_3**  
> ARG INSTALLER\_FILE=**http://emenda.com/download.?file=kw-server-installer.12.3.0.810.linux64.tar.gz**  
> ARG LICENSE\_FILE=**/license_path/LICENSE.lic**  
 

### How to run it?	


<ol> <li>Start Docker service: <code>sudo service docker start</code></li>
<li> If you use the image from DockerHub ignore this step go to step 3 directly
<ol><li> Compile the Dockerfile <code>docker build -t <b>[Name of your docker image] [path of the docker file]</b></code>
<br>
<em>Example</em>
<br><code>docker build -t <b>Ubuntu\_KW12\_3\_server\_docker</b> <b>.</b></code>
<pre><code>Sending build context to Docker daemon
Step 0 : FROM debian:unbuntu
 ---> bf84c1d84a8f
Step 1 : RUN apt-get -y update
...
Removing intermediate container 9522c6b9bf95
Successfully built aaf20fb25dac</code></pre>
</li>
<li> Run the image <code>docker run -d --name <b>[contener name]</b> -p <b>[local computer port]</b>:<b>[container port] [Name of your docker image]</b></code>
<br>
<em>Example</em>
<br><code>docker run -d --name <b>KW\_server\_12\_3</b> -p <b>8123:8123</b> <b>Ubuntu\_KW12\_3\_server\_docker</b>
<pre></code> <code>e9ca3cd8f90b8554ca99ec8ba15a039f827005bd8fecbf80d72ce7267006a6df</code></pre>
</li>
</ol>
<li> If you use directly image from the DockerHub Website (<a href="https://hub.docker.com/r/emenda/klocwork/">link</a>)</li>
<ol><li>Pull the image from Docker Hub <code>docker pull emenda klocwork </code>
</li>
<li> Run the image <code>docker run -d --name <b>[contener name]</b> -p <b>[local computer port]</b>:<b>[container port] [Name of your docker image]</b></code>
<br>
<em>Example</em>
<br><code>docker run -d --name <b>KW\_server\_12\_3</b> -p <b>8123:8123</b> <b>Ubuntu\_KW12\_3\_server\_docker</b>
<pre></code> <code>e9ca3cd8f90b8554ca99ec8ba15a039f827005bd8fecbf80d72ce7267006a6df</code></pre>
</li>
</ol>
<li> Optional
<ol> <li>Stop the docker <code>docker stop <b>[Name of your docker image]</b></code></li>

<em>Example</em>
<br><code>docker stop <b>Ubuntu\_KW12\_3\_server\_docker</b>
</code>
<li>Delete the docker <code>docker rm <b>[Name of your docker image]</b></code></li>

<em>Example</em>
<br><code>docker rm <b>Ubuntu\_KW12\_3\_server\_docker</b></code></li>
</ol>
</ol>

## Authors

* **Ludovic Ponsolle** - *Initial work* - [Emenda](http://emenda.com)

## Need helps to customize your Docker
### Don't hesitate to contact directly [Emenda](http://emenda.com/) if you need help to customize your Klocwork Docker image or to start your continuous integration process.###

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details



