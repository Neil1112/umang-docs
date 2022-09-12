# Semantic Versioning

Semantic Versioning is a widely-adopted version scheme that uses a three-part version number (MAJOR.MINOR.PATCH), an optional pre-release tag, and an optional build meta tag.

The presence of a pre-release tag indicates substanial risk (can contain bugs), and so does the version with a MAJOR as 0. For example - `0.x.y`.


## Semantic Versioning Specification (SemVer)

The following points makes the complete spcification of Semantic Versioning.

1. Software using Semantic Versioning MUST declare a public API. This API could be declared in the code itself or exist strictly in documentation. However it is done, it SHOULD be precise and comprehensive.

1. A normal version number MUST take the form X.Y.Z where X, Y, and Z are non-negative integers, and MUST NOT contain leading zeroes. X is the major version, Y is the minor version, and Z is the patch version. Each element MUST increase numerically. For instance: 1.9.0 -> 1.10.0 -> 1.11.0.

1. Once a versioned package has been released, the contents of that version MUST NOT be modified. Any modifications MUST be released as a new version.

1. Major version zero (0.y.z) is for initial development. Anything MAY change at any time. The public API SHOULD NOT be considered stable.

1. Version 1.0.0 defines the public API. The way in which the version number is incremented after this release is dependent on this public API and how it changes.

1. Patch version Z (x.y.Z | x > 0) MUST be incremented if only backwards compatible bug fixes are introduced. A bug fix is defined as an internal change that fixes incorrect behavior.

1. Minor version Y (x.Y.z | x > 0) MUST be incremented if new, backwards compatible functionality is introduced to the public API. It MUST be incremented if any public API functionality is marked as deprecated. It MAY be incremented if substantial new functionality or improvements are introduced within the private code. It MAY include patch level changes. Patch version MUST be reset to 0 when minor version is incremented.

1. Major version X (X.y.z | X > 0) MUST be incremented if any backwards incompatible changes are introduced to the public API. It MAY also include minor and patch level changes. Patch and minor versions MUST be reset to 0 when major version is incremented.

1. A pre-release version MAY be denoted by appending a hyphen and a series of dot separated identifiers immediately following the patch version. Identifiers MUST comprise only ASCII alphanumerics and hyphens [0-9A-Za-z-]. Identifiers MUST NOT be empty. Numeric identifiers MUST NOT include leading zeroes. Pre-release versions have a lower precedence than the associated normal version. A pre-release version indicates that the version is unstable and might not satisfy the intended compatibility requirements as denoted by its associated normal version. Examples: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 1.0.0-x.7.z.92, 1.0.0-x-y-z.–.

1. Build metadata MAY be denoted by appending a plus sign and a series of dot separated identifiers immediately following the patch or pre-release version. Identifiers MUST comprise only ASCII alphanumerics and hyphens [0-9A-Za-z-]. Identifiers MUST NOT be empty. Build metadata MUST be ignored when determining version precedence. Thus two versions that differ only in the build metadata, have the same precedence. Examples: 1.0.0-alpha+001, 1.0.0+20130313144700, 1.0.0-beta+exp.sha.5114f85, 1.0.0+21AF26D3—-117B344092BD.

1. Precedence refers to how versions are compared to each other when ordered.

    1. Precedence MUST be calculated by separating the version into major, minor, patch and pre-release identifiers in that order (Build metadata does not figure into precedence).

    1. Precedence is determined by the first difference when comparing each of these identifiers from left to right as follows: Major, minor, and patch versions are always compared numerically.

    Example: 1.0.0 < 2.0.0 < 2.1.0 < 2.1.1.

    1. When major, minor, and patch are equal, a pre-release version has lower precedence than a normal version:

    Example: 1.0.0-alpha < 1.0.0.

    1. Precedence for two pre-release versions with the same major, minor, and patch version MUST be determined by comparing each dot separated identifier from left to right until a difference is found as follows:

        1. Identifiers consisting of only digits are compared numerically.

        1. Identifiers with letters or hyphens are compared lexically in ASCII sort order.

        1. Numeric identifiers always have lower precedence than non-numeric identifiers.

        1. A larger set of pre-release fields has a higher precedence than a smaller set, if all of the preceding identifiers are equal.
    
    Example: 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.


## Designating development stages

Software in the experimental stage (alpha or beta) often uses a zero in the first ("MAJOR") position of the sequence to designate its status. However, this scheme is only useful for the early stages, not for upcoming releases with established software where the version number has already progressed past 0. 

That is, while the software is in early developments and requires frequent updates, it's MAJOR is 0 which indicates under initial development. Once the softwares passes MAJOR 0, unstable versions are indicated with a pre-release tag, while the version without pre-release tag indicates a stable version.

The following table shows the comparison of different development stages:

| Stage | Semver | Notes |
| -------------- | ------------- | -------------- |
| Intial Development | 0.5.2 | initial version indicated by a leading zero |
| Alpha | 1.2.0-a.1 | alpha version indicated by `a.1`. It is written by a hyphen, which indicates pre-release tag |
| Beta | 1.2.0-b.2 | beta version indicated by `b.2`. It is written by a hyphen, which indicates pre-release tag |
| Release Candidate | 1.2.0-rc.3 | release candidate version indicated by `rc.3`. It is written by a hyphen, which indicates pre-release tag |
| Release | 1.2.0 | no pre-release tag indicates a production version |
| Post-release fixes | 1.2.5 | the incremented patch indicates post-release fixes |

Thus a typical development progresses as:

```
Initial development stage ("MAJOR" as zero):
0.0.0 -> 0.0.1 -> 0.1.0 -> ..... -> 0.5.5

Alpha stage:
1.0.0-a.1 -> 1.0.0-a.2 .....

Beta stage:
1.0.0-b.1 -> 1.0.0-b.2 .....

Release candidate:
1.0.0-rc.1 -> 1.0.0-rc.2 .....

Release:
1.0.0

Post-release fixes:
1.0.1 -> 1.0.2 -> 1.0.3 .....
```

## Summary

### Given a version number MAJOR.MINOR.PATCH, increment the:

1. MAJOR version when you make incompatible API changes
1. MINOR version when you add functionality in a backwards compatible manner
1. PATCH version when you make backwards compatible bug fixes

Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

> Example - software that relies on version **2.1.5** is compatible with version **2.2.3**, but not nessarily with the version **3.2.4**


### The development stages progresses as:

`initial development` -> `alpha` -> `beta` -> `release candidate` -> `release` -> `post-release-fixes`

## References

1. [Wikipedia](https://en.wikipedia.org/wiki/Software_versioning)
1. [Semantic Versioning guide](https://semver.org)