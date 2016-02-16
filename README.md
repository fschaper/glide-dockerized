# Dockerized Glide

This is a docker configuration for glide - an on-demand image manipulation library written in PHP.

Its API is exposed via HTTP, similar to cloud image processing services like [Imgix](http://www.imgix.com/) and [Cloudinary](http://cloudinary.com/).

See [https://github.com/thephpleague/glide](https://github.com/thephpleague/glide) for their github site.

The Dockerfile extends upon the official php7 docker image. It adds imagemagick support, php composer and of course glide.

## Documentation

Full documentation of glide and their API can be found at [glide.thephpleague.com](http://glide.thephpleague.com).

## Installation

Build the docker image from within the git directory

```bash
$ docker build -t glide .
```

Mount the ./images directory to the container and run the glide server. If you are on OS X using the virtualbox driver, ensure that your project is located under `/Users` otherweise you will have to manually add the directory to the VirtualBox mount points for your docker machine.

```bash
$ docker run -ti -v "$(pwd)/images:/var/lib/glide/master" -p 8080:80 glide
```

You can now access the container from your host machine via `http://127.0.0.1:8080/{your_image_name?optional_parameters}`

There are two important directories.
- One is the master image directory `/var/lib/glide/master` where all your source images are hostet and 
- the cache directory `/var/lib/glide/cache` where glide will keep all the processed images.

You probably would not want the latter one to be on the containers COW filesystem.

## Todo

This docker image is no more than a simple playground. It is not ready for production use.

- [ ] get rid of the .htaccess file which slows down apache.
- [ ] implement proper error handling in the index.php file.
- [ ] make the glide manipulators customizable for the container.
- [ ] optimize the image size.

## Credits

- [Jonathan Reinink](https://github.com/reinink) for glide

## License

The MIT License

Copyright (c) 2010-2016 Google, Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
