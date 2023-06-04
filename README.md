## Notes

### To watch for filesystem changes
For Node-based applications, `nodemon` is a great tool to watch for 
file changes and then restart the application. There are equivalent 
tools in most other languages and frameworks.

### Security
While using env vars to set connection settings is generally ok for 
development, it is HIGHLY DISCOURAGED when running applications in 
production. Diogo Monica, a former lead of security at Docker, 
wrote a fantastic [blog post](https://diogomonica.com/2017/03/27/why-you-shouldnt-use-env-variables-for-secret-data/) explaining why.

A more secure mechanism is to use the secret support provided by 
your container orchestration framework. In most cases, these secrets 
are mounted as files in the running container. You'll see many apps 
(including the MySQL image and the todo app) also support env vars 
with a `_FILE` suffix to point to a file containing the variable.

As an example, setting the `MYSQL_PASSWORD_FILE` var will cause the 
app to use the contents of the referenced file as the connection 
password. Docker does not do anything to support these env vars. Your 
app will need to know to look for the variable and get the file 
contents.