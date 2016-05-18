# GitBook

This Dockerfile implementation of the gitbook-cli toolchain is intended for 
standalone hosting of a written GitBook, or for those using their
own editor to create content. 

See the [GitBook Project Documentation](https://help.gitbook.com/) for more 
information on GitBook (including designing GitBooks using their fantastic editor), 
or the [GitBookIO gitbook-cli GitHub page](https://github.com/gitbookio/gitbook-cli) 
for more information about the gitbook-cli toolchain.

See [tobegit3hub's Dockerfile](https://github.com/tobegit3hub/gitbook-server) 
for the basis of my Dockerfile.  My main goal was to slim the image down
while maintaining the functionality - for instance, using Alpine instead of Ubuntu, 
and using a more up-to-date instance of GitBook.  Since installing Calibre would
require glibc packages, it was left out of this version.  Stay tuned for a Calibre
version, still in the works.


## Creating a new book

```
docker run --rm -v /home/yourname/yourbook:/gitbook drockney/gitbook:latest gitbook init /gitbook
```

This will initialize a README.md and SUMMARY.md in whatever directory you've specified.

## Generating PDF output

Not currently possible due to lack of Calibre libraries.

## Starting GitBook with a locally-hosted book

```
docker run -d -p 4000:4000 -v /home/yourname/yourbook:/gitbook drockney/gitbook:latest
```

Any contents found in the "/home/yourname/yourbook" location will automatically 
be updated - GitBook is watching for changes in that directory and will
reload the contents whenever necessary.


## Versioning
Why the strange versioning?  Check out 
[RisingStack Engineering's article](https://blog.risingstack.com/minimal-docker-containers-for-node-js/) 
about how they version their Node.js Docker images.  I liked their reasoning so 
I also adopted it here.

When you see 3.3-2.6.7-1.0.0, it means it's an Alpine Linux 3.3 image, 
implementing version 2.6.7 of GitBook, and the first (1.0.0) release that I felt
was ready to be seen by the public.