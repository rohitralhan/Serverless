<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <!--[if IE]><meta http-equiv="X-UA-Compatible" content="IE=edge"><![endif]-->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="generator" content="Asciidoctor 1.5.4">
  <!-- <title>Quarkus Serverless Datagrid - Deploying Quarkus Serverless apps integrated with
    Datagrid</title> -->
  <link rel="stylesheet" href="https://asciidoclive.com/assets/asciidoctor.js/css/asciidoctor.css">
</head>

<body class="article toc2 toc-left">
<div id="header">
<h1>Deploying Quarkus Serverless apps with Datagrid on Red Hat OpenShift Platform</h1>
<div id="toc" class="toc2">
<div id="toctitle">Table of Contents</div>
<ul class="sectlevel1">
<li><a href="#_background">Background</a></li>
<li><a href="#_prerequisites">Prerequisites</a></li>
<li><a href="#_goals">Goals</a></li>
<li><a href="#_steps">Steps</a></li>
</ul>
</div>
</div>
<div id="content">
<div class="sect1">
<h2 id="_background">Background</h2>
<div class="sectionbody">
<div class="paragraph">
<p>Serverless, a popular word. No need for keeping resources alive where there is no need to. It&rsquo;s event-driven programming, one process per request, and you can scale immediately when you need to. From zero to enough, without you having to worry about it. When it&rsquo;s finished, it scales back to zero, just like that.&rdquo;</p>
</div>
<div class="paragraph">
<p>What do you need to achieve this? You need something which can offer low memory footprint and fast startup and shutdown times. Can you use Java, sure you can, but can it offer the real benefits required by a serverless application probably not OOTB, it is not natively optimized for running serverless: well &ldquo;When you activate a Java serverless function for the first time, you&rsquo;ll see that it takes about 300 milliseconds to start. This so-called cold-start is relatively fast, but not fast enough, in my opinion. Also, Java is more memory-intensive and when you do cloud-native development, the less memory you consume, the better.&rdquo;</p>
</div>
<div class="paragraph">
<p>To fix this, many vendors put a lot of effort in optimizing runtimes for containerized environments and cloud-native development. So did Red Hat by launching Quarkus. Quarkus is a Kubernetes-native Java framework, also known as &ldquo;supersonic subatomic Java,&rdquo; that allows developers to build Java applications that are meant to run in, and are optimized for, these type of environments.</p>
</div>
<div class="paragraph">
<p>This demo will use Quarkus for building the applications, Red Hat OpenShift for Serverless, Red Hat DataGrid for in-memory, distributed, NoSQL datastore solution. The scripts will allow you to create the Red Hat DataGrid cluster and deploy the Quarkus Serverless application on Red Hat OpenShift platform.</p>
</div>
</div>
</div>
<div class="sect1">
<h2 id="_prerequisites">Prerequisites</h2>
<div class="sectionbody">
<div class="paragraph">
<p><strong>Tools</strong></p>
</div>
<div class="paragraph">
<p>The tools you need locally:</p>
</div>
<div class="ulist">
<ul>
<li>
<p>Access to Red Hat OpenShift platform</p>
</li>
<li>
<p>JDK, OpenSSL, Keytool</p>
</li>
<li>
<p>oc - OpenShift Command Line Interface (CLI) - Available from&nbsp;OpenShift cluster (See image below)</p>
</li>
<li>
<p>kn - OpenShift Serverless Command Line Interface (CLI)- Available from&nbsp;OpenShift cluster (See image below)</p>
</li>
<li>
<p>Access to command line</p>
</li>
<li>
<p>A browser (Chrome, Firefox)</p>
</li>
</ul>
<p><strong>OpenShift command line tool download:</strong></p>
<div class="paragraph">
<p><span class="image"><img src="images/command-line-tools-download_1.png" alt="Code" /></span></p>
</div>
</div>
<div class="paragraph">
<p><strong>Skills</strong></p>
</div>
<div class="ulist">
<ul>
<li>
<p>Familiarity with Red Hat OpenShift Platform and Operators.</p>
</li>
<li>
<p>Shell Scripts (optional)</p>
</li>
</ul>
</div>
</div>
</div>
<div class="sect1">
<h2 id="_goals">Goals</h2>
<div class="sectionbody">
<div class="ulist">
<ul>
<li>
<p>Have Red Hat DataGrid Cluster deployed on Red Hat OpenShift</p>
</li>
<li>
<p>Have the Quarkus Serverless Applications deployed on Red Hat OpenShift</p>
</li>
</ul>
</div>
<div class="paragraph">
<p>Once the serverless applications are deployed you should be able to hit the URL and see the data appear on the screen in JSON format in the browser.</p>
</div>
</div>
</div>
<div class="sect1">
<h2 id="_steps">Steps</h2>
<div class="sectionbody">
<div class="ulist">
<ul>
<li>
<p>Provision a Red Hat OpenShift platform</p>
</li>
<li>
<p>Install the OpenShift Serverless Operator (using the UI or CLI)</p>
</li>
</ul>
</div>
<div class="paragraph">
<p><span class="image"><img src="images/operator.png" alt="ServerlessOperator" /></span></p>
</div>
<ul>
<li>
<p>Install the Knative Serving under Red Hat OpenShift Serverless</p>
</li>
</ul>
</div>
<div class="paragraph">
<p><span class="image"><img src="images/knativeserving.png" alt="KnativeServing" /></span></p>
</div>
<div class="ulist">
<ul>
<li>
<p>Download the scripts to a folder</p>
</li>
<li>
<p>Go to command line and login to your OpenShift installation</p>
</li>
<li>
<p>Edit the <strong>provision-serverless-dg-workshop.sh</strong> (optional)</p>
</li>
</ul>
</div>
<div class="paragraph">
<p><span class="image"><img src="images/code.png" alt="Code" /></span></p>
</div>
<div class="ulist">
<ul>
<li>
<p>Execute the <strong>provision-serverless-dg-workshop.sh</strong></p>
<div class="ulist">
<ul>
<li>
<p>This script will provision the Red Hat DataGrid Cluster and the Quarkus Serverless applications</p>
</li>
<li>
<p>The namespace names are controlled by the following variables in the <strong>provision-serverless-dg-workshop.sh</strong>:</p>
<div class="literalblock">
<div class="content">
<pre>SERVERLESS_PROJECT_NAME="serverless-apps-1" +
SERVERLESS_PROJECT_DISPLAY_NAME="ServerlessApps"</pre>
</div>
</div>
<div class="literalblock">
<div class="content">
<pre>DATAGRID_PROJECT_NAME="datagrid-ws-1" +
DATAGRID_PROJECT_DISPLAY_NAME="DataGridCluster"</pre>
</div>
</div>
</li>
</ul>
</div>
</li>
<li>
<p>Once the provisioning is complete select <strong>Developer</strong> in the dropdown and select <strong>Topology</strong></p>
</li>
</ul>
</div>
<div class="paragraph">
<p><span class="image"><img src="images/topology.png" alt="Topology" /></span></p>
</div>
<div class="ulist">
<ul>
<li>
<p>Click on the quarkus-serverless-server application and the browser should open and should show an error on the screen (RESTEASY003210: Could not find resource for full path:...) this is expected. Copy the URL and using a <strong>rest client application</strong> execute a post wiht the below URL <strong>http:// &lt;&lt; replace with copied URL of quarkus-serverless-server app&gt;&gt;/employees/</strong> and use the below body in JSON format:</p>
<div class="ulist">
<ul>
<li>
<p>[ { "empId": "1A", "empName": "John Doe", "empProject": "Quarkus" }, { "empId": "2A", "empName": "Jane Doe", "empProject": "Quarkus" }, { "empId": "3A", "empName": "Jo Doe", "empProject": "Quarkus" } ]</p>
</li>
</ul>
<strong>OR</strong>
<ul>
<li>
<p><strong>curl</strong> -H "Content-Type: application/json" -X POST -d '[ { "empId": "1A", "empName": "John Doe", "empProject": "Quarkus" }, { "empId": "2A", "empName": "Jane Doe", "empProject": "Quarkus" }, { "empId": "3A", "empName": "Jo Doe", "empProject": "Quarkus" } ]' &lt;&gt;/employees</p>
</li>
</ul>
</div>
</li>
<li>
<p>Now click on the Open Url icon at the top of the quarkus-serverless-client application.</p>
</li>
<li>
<p>Once you click the browser will open and you should see the list of employees</p>
</li>
</ul>
</div>
</div>
</div>
</body>

</html>
