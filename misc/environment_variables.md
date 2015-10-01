# Environment Variables know-how
You can set Environment variables in the Dockerfile or the docker run command. The run command overrides the Dockerfiles value if the same variable is used (good for setting default values which you override).

**Problem:**  
But a big headache is the fact that a process at runtime (after run command) can’t change an environment variable globally. It can change it for that specific process (say a script).

