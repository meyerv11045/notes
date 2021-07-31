# Docker Tags

- Enable you to ensure that anyone who pulls down your images knows exactly what they are getting
- Not the same as file tags
- Used for clarification-- tells you exactly what image you are pulling from the repository

## Adding Tags to Images

`docker tag IMAGE ID image/TAG` 

- IMAGE ID is the 12 character identification string for the image (listed from the `docker images` command) 
- TAG is our newly created versioning tag (e.g. `dev:v1.6.14.2020`)
- To create a new Ubuntu image:
  - `docker tag 7b9b13f7b9c0 ubuntu/dev:v1.6.14.2020`





https://www.techrepublic.com/article/how-to-use-docker-tags-to-add-version-control-to-images/