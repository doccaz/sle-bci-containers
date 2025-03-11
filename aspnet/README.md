# What is this?

This is a very simple "Hello world" ASP.NET application, modified to use SUSE's SLE-BCI (Base Container Images). 

If you're unfamiliar with SLE-BCI, it's a collection of SUSE-maintained hardened base container images that can be used by anyone, for free. Subscription options are available for L3 support.

Besides de the basic SLE Micro-based image which can confortably replace something like Alpine Linux, there are images with all sorts of different frameworks available, like .NET, Java, NodeJS, Go, etc.

More details here: https://registry.suse.com


Also, check out: https://registry.suse.com/repositories/bci-dotnet-aspnet9


# How to build this


Run this command inside the directory containing "Dockerfile":

```
# podman build -t myimagetag/aspnet-sample-bci .
```

Wait for the build. Done!


# How to run this

Since this is just a hello world (not a server application), you just need this:

```
# podman run -it --rm myimagetag/aspnet-sample-bci
```

And that's it.



Original sources come from: https://github.com/dotnet/dotnet-docker/tree/main/samples



