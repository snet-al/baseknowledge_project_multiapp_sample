# project_multiapp_sample
This is an example of a project with multi applications

## The definition of a project
To create the best architecture for big projects first of all we have to create some definitions of what are we creating.
The main concept we want to coin is the concept of a project.
Based on my experience the best way to think of a project is as the full software solution created for a given problem.
In the term of project i include all the source code, development processes, deployment etc.
The main elements of a project is code management, and in this domain are a lot of a solutions how the source code is managed,
but the best practise that is emerging is the management of code throught git, and git repositories. Also with the emerging of 
microservices, the source code of a project can be distributed in multiple repositories each of them considered a microservice.
The job of the project repo is to integrate all this repo in one, ready to be deployed.
The first script i propose for the project is `init`.
What `init` does is cloning all the repositories of the project in the actual folders for each app.

## The definition of an app (application)
The application is the smallest unit of software that can be deployed as a autonomous unit, 
independent(at least at some levels) of the other code, 
can be coded in different technologies, 
tested independently, and more importantly included very well in another project.
Examples of app in a projects are backend of a site created in php, some services created in python, and frontend
created with vuejs and all of them created separately.

Another difference between the concept of project and app is that for the project we now can talk about 
infrastructure architecture, and for the app we specify the software achitecture.


### init.sh
Lets go and see how we will integrate the source code of our project.
In init.sh file we will specify all the repositories for each app we need, and specify where to clone it, for example:

```code
git clone http://app_user.git app_user
git clone http://app_backend_laravel.git app_backend
git clone http://app_vuejs-site.git app_site
...
```
With these lines we manage where we have the code and how we want to integrate it in out project.
And every app now can be developer in a separate IDE.

### buid.sh
The next task of a project is to specify the integration between apps. This is the proces of building the environment
for the apps to be able to run as a full system.
We tend to make the apps as independently as possible but if are necessary some configuration and envirement files are
created, or updated by this script.
For example each app has its own `.env` file but some url must be unique, so the duty of `build.sh` is to update these files.
If these is not possible must be at least printed some instructions for developer to manually change them.

### deploy.sh
This is the script that start the services. This script should have at least two options `dev` and `live`.
It is very specific to the project the strategy of deployment so we are not defining it here.

