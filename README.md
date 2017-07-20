# dockerfiles

My Dockerfiles

This project contains Dockerfiles, help yourself.


## Usage

I'm using those Dockerfiles as basis for specific project Dockerfiles.
Dockerfiles should be at `.docker/` of your folder with project.

### My usual project structure is:

    .
    ├── build
    ├── docker                  # My folder with 'docker' stuff
    |   ├── tools
    |   ├── docker-compose.yml
    |   └── Dockerfile
    ├── docs
    ├── src
    ├── test
    ├── tools
    ├── package.json
    ├── LICENSE
    └── README.md

Local path which will be as home in your container can be changed in `docker-compose.yml`. Actual path is `./../` - path starts at folder `docker` where you run command `sudo docker-compose build` for building your container.

### Calling container

I'm creating aliases for running containers - for example my michalsindler/ionic:ionic3 (change 'projectname'):

`alias projectname='sudo docker run -ti --privileged -v /dev/bus/usb:/dev/bus/usb -v $PWD:/myApp:rw -p 8100:8100 -p 35729:35729 -p 5037:5037 michalsindler/projectname:ionic3 ionic`

With that alias is possible to call:
`projectname info` which calls `ionic info` in container

### Run Docker without sudo

If you want to run Docker wihtout `sudo`, you can add your user to group `docker`:
1. Check if 'docker' group exists `egrep -i "^docker" /etc/group;`
   If you see output like this:
   `docker:x:999:<yourusername>`
   That means that group exists and your user is in it
2. If group does not exists, create it `sudo groupadd docker`
3. If your user is not in 'docker' group. add it `sudo gpasswd -a $USER docker`
4. Changes will be in effect after log out & log in or `newgrp docker`

## Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## History

## Credits

Lot's of good people of internet.

## License

Live long and dock your projects.