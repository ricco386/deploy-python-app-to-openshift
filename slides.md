# #27 CNCF Meetup

How to deploy Python app to OpenShift

Richard Kellner

---

# About Me

* Working as hlavný projektant IS dohľadu at Národná banka Slovenska
* Python 10+ years exp. before that PHP developer in London
* RedHat Certified System Administrator + OpenShift Developer
* Chairman at SPy o.z.: [PyCon SK](https://pycon.sk) & [Učíme s hárdverom](https://www.ucimeshardverom.sk/)
* PSF Fellow
* More at [www.linkedin.com/in/richardkellner](https://www.linkedin.com/in/richardkellner)

Note: Moje vlastne nazory nijako nepreviazane na zamestnavatela a nemam ziadne zavazky voci Red Hatu

---

# What is OpenShift

OKD is a distribution of Kubernetes optimized for continuous application development and multi-tenant deployment.

OKD embeds Kubernetes and extends it with security and other integrated concepts.

--

![](https://cloud.redhat.com/hubfs/images/marketecture.png?t=1535557524001)

Note:
* Porovnanie s distribuciou Linuxu
* OpenShift vs. OKD.io
* Minishift (< 3.X ), Code Ready Containers (< 4.X)

---

# Python web apps

Let's create a sample Django app and deploy to OpenShift.

Any application that supports WSGI (ASGI), essentialy all popular framewroks...

Note:

WSGI is implementation-neutral interface between web servers and web applications or frameworks to promote common ground for portable web application development.

* Prakticka ukazka v terminaly, Spravit Django projekt
* Project vs. app
* virtual envs, compare to container

---

# How to deploy app in OpenShift

1. Build the application from source code
2. Build the application from source code and a Dockerfile
3. Build the application from a container image

--

## S2I

OpenSource at GitHub:
* [https://github.com/openshift/source-to-image](https://github.com/openshift/source-to-image)
* [https://github.com/sclorg/s2i-python-container](https://github.com/sclorg/s2i-python-container)

For a dynamic language like Python, the build-time and run-time environments are typically the same. Starting with a builder image that describes this environment - with Python, GCC, and other packages needed to set up and run your application installed. 

--

1. Start a container from the builder image with the application source injected into a known directory
2. The container process transforms that source code into the appropriate runnable setup - in this case, by installing dependencies and moving the source code into a pre-defined directory.
3. Commit the new container and set the image entrypoint to be a script (provided by the builder image) that will start webserver (runserver, gunicorn) to host the Python application.