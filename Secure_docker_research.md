# Secure Docker deployments

The intention is to deploy the django + postgresql application on two docker containers as securely as possible.

## Concerns

 - Users can exec into docker containers. 
 - If root priv is gained on the postgresql container (priv esc is usually very very easy once RCE is obtained), the conf file can be edited and access to the database can be gained. This way the raw csv can be easily viewed.
 
 ## Solutions

- Remove docker from the sudo group, this would disable non root users from using any docker commands.
- Add a nologin flag for any user other than administrator/maintainer inside the docker container. This would prevent any user from attaching to the docker container even if they somehow figure out how to use docker commands.
- Encrypt the data in the postgresql database to prepare for a doomsday scenario. Preferably a symmetric encryption so it doesn't take too much time to encrypt and decrypt
- Drop any requests that come from an ip that is unauthorized. The front end will have a static ip whose requests will be allowed to pass through.

## References

- https://serverfault.com/questions/724553/how-to-prevent-attach-or-exec-in-a-docker-container
- https://man7.org/linux/man-pages/man8/nologin.8.html
- https://stackoverflow.com/questions/14588212/postgresql-resetting-password-of-postgresql-on-ubuntu
- https://github.com/moby/moby/issues/8664 (has a few interesting perspectives on `docker exec`)
