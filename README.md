# CMC
## CRS4 Microservice Core - Global project
This repository groups all the projects that compose the CMC framework.
The purpose of this global project is to provide a single entry point to the CMC framework, 
along with a concise documentation (this README) to guide the user through the main concepts behind CMC
and the minimal steps to deploy a fully working environment.

###What does CMC do?
CMC is a general-purpose framework for building services 
that live and communicate in the context of a modular and highly scalable architecture.
It provides cross-cutting functionalities that helps not to reinvent the wheel.
They can be grouped as <b>core</b> functionalities, taking care of authentication, user management and 
third-party integration, and <b>helper</b> functionalities, currently a messaging service and a file management one.

### The CMC modules
CMC is built around a Microservice architecture. This means that each high level functionality is delivered
through a software piece called Microservice. A microservice is self-contained, runs on its own server, 
is independent from the other microservices but can call them if needed.<br>
From the code point of view, all services have its own repository as a submodule of <code>cmc</code> repo, 
so to clone the whole framework just type:

<code> git clone git@github.com:smartenv-crs4/cmc.git </code> <br>
<code> cd cmc </code> <br>
<code> git submodule update --init --remote </code> <br><br>

All done! Now you should have a <code>cmc</code> folder containing a directory for each module.

### Module configuration and run
Now let's see how to properly configure each module in order to have the whole framework up and running.

0. In each module directory, rename the <code>/config/default.json.rename</code> file to <code>/config/default.json</code>
0. In this file, set the properties which are mandatory to correctly run that service.
As a rule of thumb, properties which have a placeholder must be set, while others have a default value which should
work in the majority of environments. <br>
0. <code>cmc-auth</code> must be the first to be set, with the URL of the database (<code>dbHost</code>) and the service itself (<code>authHost</code>).
Note that for each service two profiles can be configured, <b>development</b> and <b>production</b>
<u>In the documentation of each service is explained how to run the service itself, also setting a profile different from the default (production)</u>
0. Start <u>only</u> <code>cmc-auth</code> according to that documentation
0. Point the browser to <code>http://your_base_url:3000/configure</code>,
sign in with the default <code>admin@admin.com/admin</code> email/password, and you will be presented with the following screen:<br>
![alt text](https://drive.google.com/open?id=14cyOz0SBNm6DpuHI1J0ZI3HIShg-CUW4 "Auth MS configuration panel")
0. The "+" button adds a new microservice to the platform. <u>Make sure to do this operation before starting the new service</u>.
Here you must set an arbitrary service name, the URL where the service will be available (directly or through a load balancer/API gateway), and the color and icon of the UI frame
0. Once added, click on the "Get Token" link inside the frame to get the token the authorisation service has just generated.
This token must be set in the <code>auth_token</code> property of <code>default.json</code> before running it
0. Run the new service
0. Repeat steps 5, 6, 7 for each service you want to add to the system.