# DockerizeNodeJS
Step by step tutorial, How to dockerize a nodejs istance

<pre><font color="#586E75"><b>chinaski@chinaski-XPS-15-9550</b></font>:<font color="#839496"><b>~</b></font>$ cd Desktop/
<font color="#586E75"><b>chinaski@chinaski-XPS-15-9550</b></font>:<font color="#839496"><b>~/Desktop</b></font>$ mkdir DockerizeNodeJS
<font color="#586E75"><b>chinaski@chinaski-XPS-15-9550</b></font>:<font color="#839496"><b>~/Desktop</b></font>$ cd DockerizeNodeJS/
<font color="#586E75"><b>chinaski@chinaski-XPS-15-9550</b></font>:<font color="#839496"><b>~/Desktop/DockerizeNodeJS</b></font>$ sudo npm init
name: (DockerizeNodeJS) dockerizenodejs
version: (1.0.0) 
description: Step by step tutorial - How to dockerize NodeJS applications
entry point: (index.js) 
test command: 
git repository: 
keywords: docker,nodejs,dockerize
author: AndreaBorio
license: (ISC) GPL
Sorry, license should be a valid SPDX license expression (without &quot;LicenseRef&quot;), &quot;UNLICENSED&quot;, or &quot;SEE LICENSE IN &lt;filename&gt;&quot; and license is similar to the valid expression &quot;GPL-3.0&quot;.
license: (ISC) 
About to write to /home/chinaski/Desktop/DockerizeNodeJS/package.json:

{
  &quot;name&quot;: &quot;dockerizenodejs&quot;,
  &quot;version&quot;: &quot;1.0.0&quot;,
  &quot;description&quot;: &quot;Step by step tutorial - How to dockerize NodeJS applications&quot;,
  &quot;main&quot;: &quot;index.js&quot;,
  &quot;scripts&quot;: {
    &quot;test&quot;: &quot;echo \&quot;Error: no test specified\&quot; &amp;&amp; exit 1&quot;
  },
  &quot;keywords&quot;: [
    &quot;docker&quot;,
    &quot;nodejs&quot;,
    &quot;dockerize&quot;
  ],
  &quot;author&quot;: &quot;AndreaBorio&quot;,
  &quot;license&quot;: &quot;ISC&quot;
}


</pre>
<pre><font color="#586E75"><b>chinaski@chinaski-XPS-15-9550</b></font>:<font color="#839496"><b>~/Desktop/DockerizeNodeJS</b></font>$ npm install express --save
</pre>

<b> Package.json </b>
<pre>
{
  "name": "dockerizenodejs",
  "version": "1.0.0",
  "description": "Step by step tutorial - How to dockerize NodeJS applications",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "docker",
    "nodejs",
    "dockerize"
  ],
  "author": "AndreaBorio",
  "license": "ISC",
  "dependencies": {
    "express": "^4.16.3"
  }
}
</pre>
<pre><font color="#586E75"><b>chinaski@chinaski-XPS-15-9550</b></font>:<font color="#839496"><b>~/Desktop/DockerizeNodeJS</b></font>$ touch index.js
</pre>

<b> index.js </b>
<pre>
var express = require('express')
var app = express()

app.get('/', function (req, res) {
  res.send('Hey folks!')
})

app.listen(8000, function () {
  console.log('server listening on port 8000!')
})
</pre>
<b> Run your server </b>
<pre><font color="#586E75"><b>chinaski@chinaski-XPS-15-9550</b></font>:<font color="#839496"><b>~/Desktop/DockerizeNodeJS</b></font>$ node index.js
server listening on port 8000!

</pre>
<b> .Dockerfile </b>
<pre>
FROM node:7
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
CMD node index.js
EXPOSE 8000
</pre>

<b> Building image </b>
  <pre><font color="#586E75"><b>chinaski@chinaski-XPS-15-9550</b></font>:<font color="#839496"><b>~/Desktop/DockerizeNodeJS</b></font>$ sudo docker build -t dockerizenodejs .</pre>
<b> Push the image to Docker Hub </b>
<pre><font color="#586E75"><b>chinaski@chinaski-XPS-15-9550</b></font>:<font color="#839496"><b>~/Desktop/DockerizeNodeJS</b></font>$ docker push andreaborio/dockerizenodejs
The push refers to repository [docker.io/andreaborio/dockerizenodejs]
</pre>

<b> Now test image </b>
<pre><font color="#586E75"><b>chinaski@chinaski-XPS-15-9550</b></font>:<font color="#839496"><b>~/Desktop/DockerizeNodeJS</b></font>$ docker run andreaborio/dockerizenodejs
server listening on port 8000!

</pre>
It works!
