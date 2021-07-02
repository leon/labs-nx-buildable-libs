# Buildable Libs

Two `@nrwl/workspace:library` where one depends on the other.

Build the domain

```
nx build shared-domain
```

now we want to build shared auth which depends on domain

```
nx build shared-auth
```
