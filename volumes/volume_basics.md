# Volumes

## VOLUME command in Dockerfile
A VOLUME command in a dockerfile makes that folder a Volume. This means that the files written to that folder will be written to the host filesystem (in the docker folders). This also means that the folder will be empty on startup.

Another complication is that you can’t commit data in that folder (since the data is in fact on the host filesystem and not the containers).

## docker run -v <folder>
This is exactly the same as above but at run time instead of build time.

## docker run -v <host-folder>:<folder>
This is where you mount a folder from the host into the container. All writes will occur on both sides (since there is in fact only one side). 
Be aware of the permission dilemma, if you use root in the container then all writes will be done by root! And the other way is if you have files owned by root in the folder and the container is using a non-root user, then it doesn’t have permission to write to that file.

