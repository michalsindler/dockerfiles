# michalsindler/ionic/ionic3

Files for building docker image with working ionic v3.x.
USB passed = possible run on connected device.

Not everything is possible yet, but helpful when creating images to be able to build your app with specific versions - check out variables on top of Dockerfile.

## Installation

1. Pull this sources and go to folder with sources on your disk
2. Install Docker ([https://docs.docker.com/engine/installation/](https://docs.docker.com/engine/installation/))
3. Install Docker Compose ([https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/))
4. Build image `sudo docker-compose build`
5. Run container `sudo docker-compose up`

## Usage

Create alias "ionic" for running container:
`alias ionic='sudo docker run -ti --privileged -v /dev/bus/usb:/dev/bus/usb -v $PWD:/myApp:rw -p 8100:8100 -p 35729:35729 -p 5037:5037 michalsindler/ionic:ionic3 ionic`

Call ionic commands:
`ionic cordova build android`
`ionic cordova run android`

## Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## History

It' short. Very short. It's like ... now.

## Credits

Lot's of good people of internet.

## License

Live long and dock your projects.