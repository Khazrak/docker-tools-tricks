# Post-Start Scripting
A good scenario for this is a database container in dev. So you want your MySQL up and running fast. But what about the data? Maybe you want automatic testing with clean data for every test. How do you get the data in the datacontainer?

With Docker 1.8 we now have a copy-command that can both copy to and from a running container. So we could start the container, copy a script or a dump into the container and then do a exec command to run the script. That's 3 extra steps that developers want to automate. The Postgres Image has a nice solution for this, they have a folder where scripts will be run on startup. The MySQL Image doesn’t have that.

So how do we improve the MySQL Image? We extend it. But now comes the tricky part. This is important to know if you’re going to make custom docker Images. The last process in the foreground is the process that the container will listen to. So if your database uses a startscript (like MySQL) and you use a custom script after this, the container will listen to the script. So when the script is done, the container stops (trouble!).

Once I did a ugly hack script so the custom script was run first, slept and then started the database so technically the database was the last process so the container listens to it. 

This was not a good solution but it was a solution.

So the other day i stumbled on a Linux command not used for scripting but could work well in containers. The command *fg*. The fg command puts a command that is run in background (usually by running it with one & character). This means that you could start the database, run the script and then use the fg command to listen to the database.

Now people will say that you shouldn’t use job handling in non-interactive mode since you can control processes by PID. But we don’t want to *wait* and  *kill*. We want to “listen”.

You need to use “set -m” in the script to active job handling.

This solution can be used for more than databases, every where you need to do a little “magic” when you start your container this works fine.
