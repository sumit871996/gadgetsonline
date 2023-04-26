# GadgetsOnline-DotNet
A sample online shopping app built using ASP.NET MVC 5.

1. Update connection string GadgetsOnlineEntities in Web.config.
3. Run the application using Visual Studio or dotnet CLI.




# License

The application code is released under the MIT-0 License

# Pre-Requisites 

On a Windows VM
{
1. Docker installed with switched to windows container
2. Git for Windows.
}

On a linux VM
{
1. Docker installed
2. jenkins container configured with following steps: (forward port 50000 while running container) 
}

Steps:

On windows VM:
step A: docker run -d --name MSSQLLocalDB --env sa_password=#yourpassword sumithpe/sql-server-windows:#tag
step B: Open Web.config in "./gadgetsonline\GadgetsOnline\GadgetsOnline" location.
        replace "Password=Sumit@mssql8796" with "Password=#yourpassword" from step A.

On linux VM:
configure jenkins

dashboard: security > agents > port: fixed : 50000
dashboard > node > add node > fill properties and save agent

step P: update webhook at github.

step Q: add a freestyle project:
step R: restrict where project can run: and add label from the slave node
step S: Link Git repo
step T: Git polling enable

step U: add build steps:

docker image build -t sumithpe/gadgets ./GadgetsOnline/
docker image push sumithpe/gadgets
docker container stop gadgetsonline
docker container rm gadgetsonline
docker container start MSSQLLocalDB
docker container run -d -p 8000:80 --rm --name gadgetsonline sumithpe/gadgets
