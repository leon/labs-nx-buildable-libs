# Buildable Libs

## Setup was

create empty nx-workspace
create the two buildable libs, with these settings

```
ng generate @nrwl/workspace:library --name=domain --directory=shared --buildable --skipBabelrc --standaloneConfig --strict --testEnvironment=node --no-interactive
ng generate @nrwl/workspace:library --name=auth --directory=shared --buildable --skipBabelrc --standaloneConfig --strict --testEnvironment=node --no-interactive
```

then create a interface in domain
then a function that uses the domain

## Problem

Build the domain goes well, and I can see the correct output in dist.

```
nx build shared-domain
```

now we want to build shared auth which depends on domain

```
nx build shared-auth

// also tried, same result
nx build shared-auth --with-deps
```

**Error**

```
File '/Users/leon/Temp/labs-buildable-libs/libs/shared/domain/src/index.ts' is not under 'rootDir' 'libs/shared/auth'. 'rootDir' is expected to contain all source files.
import { User } from '@myorg/shared/domain';
```

According to the NX Cloud 2.0 video --with-deps was needed before, but not any longer.
since nx.json knows this itself by the new targetDependencies.

```
"targetDependencies": {
    "build": [
      {
        "target": "build",
        "projects": "dependencies"
      }
    ]
  },
```

nx dep-graph shows the correct relationship

Could it be that `@nrwl/workspace:tsc` doesn't know how to use the buildable libs?
