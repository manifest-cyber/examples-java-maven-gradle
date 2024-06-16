# Untitled

# SBOM Generation for Java

## Overview

SBOM generation has become essential for detecting vulnerabilities, ensuring compliance, and addressing license issues. Although it may seem straightforward, the quality of results varies based on ecosystems, generators, formats, and specific project files.

By utilizing this repository, a fork from [arun-gupta/docker-java-sample](https://github.com/arun-gupta/docker-java-sample), which is an open-source Java library with Maven support, we aim to demonstrate different outputs and guide you through the SBOM generation process and its expected results. This will assist you in reproducing the process in your own projects with Manifest.

<aside>
⚠️ This repository assumes the use of Maven. Native codebases with JAR or other archived based project should function the same. However, different output and supported features are expected.

</aside>

## Prerequisites

- Install Manifest CLI by following the [installation guide](https://github.com/manifest-cyber/cli).
- **java sdk,** **maven** and **gradle** are installed and configured
- (optional) Node, NPM installed (**cdxgen** only)

## Generate

In this example, we would compare the results of **syft**, **trivy,** and **cdxgen** to **spdx-sbom-generator.**

### Installing Generators

The **manifest-cli** cannot function without the proper installation of the underlying generators. Fortunately, you can install them using the following command.

```bash
manifest-cli install -g cdxgen
manifest-cli install -g syft
manifest-cli install -g trivy
manifest-cli install -g spdx-sbom-generator
```

### Project files

Java projects have different configurations, some use `pom.xml` , some `build.gradle` or `settings.gradle` , others includes Scala, Kotlin. In addition, `gradle.lock` exists which might come handy in various situations.

### Generation with Manifest

The example project uses a mix of those, lets attempt to generate an SBOM and compare the results.

**Syft**

```tsx
manifest-cli sbom --name=publiccms --version=0.0.0-dev --generator=syft -f test-syft.json .

```

The output should look like this:

```tsx
{
  "$schema": "http://cyclonedx.org/schema/bom-1.5.schema.json",
  "bomFormat": "CycloneDX",
  "specVersion": "1.5",
  "version": 1,
  "metadata": {
    "tools": {
      "components": [
        {
          "type": "application",
          "author": "anchore",
          "name": "syft",
          "version": "1.3.0"
        }
      ]
    },
    "component": {
      "bom-ref": "publiccms@0.0.0-dev",
      "type": "application",
      "name": "publiccms",
      "version": "0.0.0-dev"
    }
  },
  "components": [
    {
      "bom-ref": ".@:af63bd4c8601b7f1",
      "type": "file",
      "name": ".",
      "components": [
        {
          "bom-ref": ".@:pkg:maven/gradle-wrapper/gradle-wrapper@3.1?package-id=047e2669c985652a",
          "type": "library",
          "name": "gradle-wrapper",
          "version": "3.1",
          "cpe": "cpe:2.3:a:gradle-wrapper:gradle-wrapper:3.1:*:*:*:*:*:*:*",
          "purl": "pkg:maven/gradle-wrapper/gradle-wrapper@3.1",
          "externalReferences": [
            {
              "url": "",
              "hashes": [
                {
                  "alg": "SHA-1",
                  "content": "02b860aedb748a825e668867c665ab3dedc16e22"
                }
              ],
              "type": "build-meta"
            }
          ],
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "java-archive-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "java"
            },
            {
              "name": "syft:package:type",
              "value": "java-archive"
            },
            {
              "name": "syft:package:metadataType",
              "value": "java-archive"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:gradle-wrapper:gradle_wrapper:3.1:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:gradle_wrapper:gradle-wrapper:3.1:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:gradle_wrapper:gradle_wrapper:3.1:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:gradle:gradle-wrapper:3.1:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:gradle:gradle_wrapper:3.1:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:location:0:path",
              "value": "/gradle/wrapper/gradle-wrapper.jar"
            },
            {
              "name": "syft:metadata:virtualPath",
              "value": "/gradle/wrapper/gradle-wrapper.jar"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/redis.clients/jedis@4.3.1?package-id=f92d8d41649e4a09",
          "type": "library",
          "group": "redis.clients",
          "name": "jedis",
          "version": "4.3.1",
          "licenses": [
            {
              "license": {
                "id": "MIT"
              }
            }
          ],
          "cpe": "cpe:2.3:a:jedis:jedis:4.3.1:*:*:*:*:*:*:*",
          "purl": "pkg:maven/redis.clients/jedis@4.3.1",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "java-pom-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "java"
            },
            {
              "name": "syft:package:type",
              "value": "java-archive"
            },
            {
              "name": "syft:package:metadataType",
              "value": "java-archive"
            },
            {
              "name": "syft:location:0:path",
              "value": "/pom.xml"
            },
            {
              "name": "syft:metadata:-:artifactID",
              "value": "jedis"
            },
            {
              "name": "syft:metadata:-:groupID",
              "value": "redis.clients"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/junit/junit@3.8.1?package-id=04300aded26a03a4",
          "type": "library",
          "group": "junit",
          "name": "junit",
          "version": "3.8.1",
          "licenses": [
            {
              "license": {
                "name": "Common Public License Version 1.0"
              }
            }
          ],
          "cpe": "cpe:2.3:a:junit:junit:3.8.1:*:*:*:*:*:*:*",
          "purl": "pkg:maven/junit/junit@3.8.1",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "java-pom-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "java"
            },
            {
              "name": "syft:package:type",
              "value": "java-archive"
            },
            {
              "name": "syft:package:metadataType",
              "value": "java-archive"
            },
            {
              "name": "syft:location:0:path",
              "value": "/pom.xml"
            },
            {
              "name": "syft:metadata:-:artifactID",
              "value": "junit"
            },
            {
              "name": "syft:metadata:-:groupID",
              "value": "junit"
            }
          ]
        }
      ]
    }
  ],
  "dependencies": [
    {
      "ref": "publiccms@0.0.0-dev",
      "dependsOn": [
        ".@:af63bd4c8601b7f1"
      ]
    }
  ]
}

```

At a quick glance, it seems like **syft** is missing the dependencies tree, if we look closely, it also missing transitive dependencies, as `jedis` is dependent on a few packages like `org.slf4j` , its worth mentioning that in Maven, there are different scopes for dependencies (very much like `devDependencies` in Node). It is debatable if the final SBOM should include all transitive dependencies, even if they do not get published after build.

It’s worth mentioning that since **syft** implements the `jar` cataloger, the SBOM contains the information for gradle wrapper.

**syft** also supports `gradle.lock` , lets generate one for the project first:

Edit `build.gradle` and add:

```groovy
dependencyLocking {
    lockAllConfigurations()
}
```

Run:

```groovy
./gradlew dependencies --write-locks
```

if all goes well, a new `gradle.lock` file should be generated.

Lets try and running generation again, lets ignore `.grade` folder:

```tsx
manifest-cli sbom --name=publiccms --version=0.0.0-dev --generator=syft -vvv -f test-syft.json .  --exclude="**/.gradle/**"
```

the output should be:

```tsx
{
  "$schema": "http://cyclonedx.org/schema/bom-1.5.schema.json",
  "bomFormat": "CycloneDX",
  "specVersion": "1.5",
  "version": 1,
  "metadata": {
    "tools": {
      "components": [
        {
          "type": "application",
          "author": "anchore",
          "name": "syft",
          "version": "1.3.0"
        }
      ]
    },
    "component": {
      "bom-ref": "publiccms@0.0.0-dev",
      "type": "application",
      "name": "publiccms",
      "version": "0.0.0-dev"
    }
  },
  "components": [
    {
      "bom-ref": ".@:af63bd4c8601b7f1",
      "type": "file",
      "name": ".",
      "components": [
        {
          "bom-ref": ".@:pkg:maven/org.apache.commons/commons-pool2@2.11.1?package-id=f96eeca5786f3519",
          "type": "library",
          "name": "commons-pool2",
          "version": "2.11.1",
          "cpe": "cpe:2.3:a:apache:commons-pool2:2.11.1:*:*:*:*:*:*:*",
          "purl": "pkg:maven/org.apache.commons/commons-pool2@2.11.1",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "java-gradle-lockfile-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "java"
            },
            {
              "name": "syft:package:type",
              "value": "java-archive"
            },
            {
              "name": "syft:package:metadataType",
              "value": "java-archive"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:apache:commons_pool2:2.11.1:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:apache:commons:2.11.1:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:location:0:path",
              "value": "/gradle.lockfile"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/gradle-wrapper/gradle-wrapper?package-id=42b168761d5dd985",
          "type": "library",
          "name": "gradle-wrapper",
          "licenses": [
            {
              "license": {
                "id": "Apache-2.0"
              }
            }
          ],
          "cpe": "cpe:2.3:a:gradle-wrapper:gradle-wrapper:*:*:*:*:*:*:*:*",
          "purl": "pkg:maven/gradle-wrapper/gradle-wrapper",
          "externalReferences": [
            {
              "url": "",
              "hashes": [
                {
                  "alg": "SHA-1",
                  "content": "1a5591754096883e87f8d5fdbf57ec2a6a99e724"
                }
              ],
              "type": "build-meta"
            }
          ],
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "java-archive-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "java"
            },
            {
              "name": "syft:package:type",
              "value": "java-archive"
            },
            {
              "name": "syft:package:metadataType",
              "value": "java-archive"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:gradle-wrapper:gradle_wrapper:*:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:gradle_wrapper:gradle-wrapper:*:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:gradle_wrapper:gradle_wrapper:*:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:gradle:gradle-wrapper:*:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:gradle:gradle_wrapper:*:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:location:0:path",
              "value": "/gradle/wrapper/gradle-wrapper.jar"
            },
            {
              "name": "syft:metadata:virtualPath",
              "value": "/gradle/wrapper/gradle-wrapper.jar"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/com.google.code.gson/gson@2.8.9?package-id=4882a3d5ef4699e0",
          "type": "library",
          "name": "gson",
          "version": "2.8.9",
          "cpe": "cpe:2.3:a:google:code:2.8.9:*:*:*:*:*:*:*",
          "purl": "pkg:maven/com.google.code.gson/gson@2.8.9",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "java-gradle-lockfile-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "java"
            },
            {
              "name": "syft:package:type",
              "value": "java-archive"
            },
            {
              "name": "syft:package:metadataType",
              "value": "java-archive"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:google:gson:2.8.9:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:code:code:2.8.9:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:code:gson:2.8.9:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:gson:code:2.8.9:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:gson:gson:2.8.9:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:location:0:path",
              "value": "/gradle.lockfile"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/org.hamcrest/hamcrest-core@1.3?package-id=27c49cf4a81058bc",
          "type": "library",
          "name": "hamcrest-core",
          "version": "1.3",
          "cpe": "cpe:2.3:a:hamcrest-core:hamcrest-core:1.3:*:*:*:*:*:*:*",
          "purl": "pkg:maven/org.hamcrest/hamcrest-core@1.3",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "java-gradle-lockfile-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "java"
            },
            {
              "name": "syft:package:type",
              "value": "java-archive"
            },
            {
              "name": "syft:package:metadataType",
              "value": "java-archive"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:hamcrest-core:hamcrest_core:1.3:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:hamcrest_core:hamcrest-core:1.3:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:hamcrest_core:hamcrest_core:1.3:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:hamcrest:hamcrest-core:1.3:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:hamcrest:hamcrest_core:1.3:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:location:0:path",
              "value": "/gradle.lockfile"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/redis.clients/jedis@4.3.1?package-id=62a9d97d14a5665d",
          "type": "library",
          "name": "jedis",
          "version": "4.3.1",
          "cpe": "cpe:2.3:a:jedis:jedis:4.3.1:*:*:*:*:*:*:*",
          "purl": "pkg:maven/redis.clients/jedis@4.3.1",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "java-gradle-lockfile-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "java"
            },
            {
              "name": "syft:package:type",
              "value": "java-archive"
            },
            {
              "name": "syft:package:metadataType",
              "value": "java-archive"
            },
            {
              "name": "syft:location:0:path",
              "value": "/gradle.lockfile"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/redis.clients/jedis@4.3.1?package-id=f92d8d41649e4a09",
          "type": "library",
          "group": "redis.clients",
          "name": "jedis",
          "version": "4.3.1",
          "licenses": [
            {
              "license": {
                "id": "MIT"
              }
            }
          ],
          "cpe": "cpe:2.3:a:jedis:jedis:4.3.1:*:*:*:*:*:*:*",
          "purl": "pkg:maven/redis.clients/jedis@4.3.1",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "java-pom-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "java"
            },
            {
              "name": "syft:package:type",
              "value": "java-archive"
            },
            {
              "name": "syft:package:metadataType",
              "value": "java-archive"
            },
            {
              "name": "syft:location:0:path",
              "value": "/pom.xml"
            },
            {
              "name": "syft:metadata:-:artifactID",
              "value": "jedis"
            },
            {
              "name": "syft:metadata:-:groupID",
              "value": "redis.clients"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/org.json/json@20220320?package-id=aaa19ccfc4bb9347",
          "type": "library",
          "name": "json",
          "version": "20220320",
          "cpe": "cpe:2.3:a:json:json:20220320:*:*:*:*:*:*:*",
          "purl": "pkg:maven/org.json/json@20220320",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "java-gradle-lockfile-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "java"
            },
            {
              "name": "syft:package:type",
              "value": "java-archive"
            },
            {
              "name": "syft:package:metadataType",
              "value": "java-archive"
            },
            {
              "name": "syft:location:0:path",
              "value": "/gradle.lockfile"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/junit/junit@4.12?package-id=88eb9ea33801578f",
          "type": "library",
          "name": "junit",
          "version": "4.12",
          "cpe": "cpe:2.3:a:junit:junit:4.12:*:*:*:*:*:*:*",
          "purl": "pkg:maven/junit/junit@4.12",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "java-gradle-lockfile-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "java"
            },
            {
              "name": "syft:package:type",
              "value": "java-archive"
            },
            {
              "name": "syft:package:metadataType",
              "value": "java-archive"
            },
            {
              "name": "syft:location:0:path",
              "value": "/gradle.lockfile"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/junit/junit@4.12?package-id=60c2dfa2407bdbdb",
          "type": "library",
          "group": "junit",
          "name": "junit",
          "version": "4.12",
          "licenses": [
            {
              "license": {
                "name": "Eclipse Public License 1.0"
              }
            }
          ],
          "cpe": "cpe:2.3:a:junit:junit:4.12:*:*:*:*:*:*:*",
          "purl": "pkg:maven/junit/junit@4.12",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "java-pom-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "java"
            },
            {
              "name": "syft:package:type",
              "value": "java-archive"
            },
            {
              "name": "syft:package:metadataType",
              "value": "java-archive"
            },
            {
              "name": "syft:location:0:path",
              "value": "/pom.xml"
            },
            {
              "name": "syft:metadata:-:artifactID",
              "value": "junit"
            },
            {
              "name": "syft:metadata:-:groupID",
              "value": "junit"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/org.slf4j/slf4j-api@1.7.36?package-id=6a54a62f3f576558",
          "type": "library",
          "name": "slf4j-api",
          "version": "1.7.36",
          "cpe": "cpe:2.3:a:slf4j-api:slf4j-api:1.7.36:*:*:*:*:*:*:*",
          "purl": "pkg:maven/org.slf4j/slf4j-api@1.7.36",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "java-gradle-lockfile-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "java"
            },
            {
              "name": "syft:package:type",
              "value": "java-archive"
            },
            {
              "name": "syft:package:metadataType",
              "value": "java-archive"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:slf4j-api:slf4j_api:1.7.36:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:slf4j_api:slf4j-api:1.7.36:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:slf4j_api:slf4j_api:1.7.36:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:slf4j:slf4j-api:1.7.36:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:slf4j:slf4j_api:1.7.36:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:location:0:path",
              "value": "/gradle.lockfile"
            }
          ]
        }
      ]
    }
  ],
  "dependencies": [
    {
      "ref": "publiccms@0.0.0-dev",
      "dependsOn": [
        ".@:af63bd4c8601b7f1"
      ]
    }
  ]
}

```

That’s more like it! The gradle cataloger is able to pick up much more. You might notice that **syft** runs multiple catalogers, so it will pick up duplicates. The main caveat for `gradle.lock` cataloger is that licenses data is absent.

Its also important to understand that transitive dependencies included in the `gradle.lock` file, are only runtime/compile time and not test. you will have to specify them explicitly in `build.gradle` if you wish.

Notable remarks, **syft** generates CPEs which are valuable for vulnerabilities and license issues detections.

**Cdxgen**

```tsx
manifest-cli sbom --name=publiccms --version=0.0.0-dev --generator=cdxgen -vvv -f test-cdx.json .
```

Just like syft, **cdxgen** supports `pom.xml` alongside `build.gradle` and others, however, it doesn’t mention anything about lockfiles.

```tsx
{
  "$schema": "http://cyclonedx.org/schema/bom-1.5.schema.json",
  "bomFormat": "CycloneDX",
  "specVersion": "1.5",
  "version": 1,
  "metadata": {
    "tools": {
      "components": [
        {
          "bom-ref": "pkg:npm/@cyclonedx/cdxgen@10.6.1",
          "type": "application",
          "author": "OWASP Foundation",
          "publisher": "OWASP Foundation",
          "group": "@cyclonedx",
          "name": "cdxgen",
          "version": "10.6.1",
          "purl": "pkg:npm/%40cyclonedx/cdxgen@10.6.1"
        }
      ]
    },
    "component": {
      "bom-ref": "publiccms@0.0.0-dev",
      "type": "application",
      "name": "publiccms",
      "version": "0.0.0-dev"
    }
  },
  "components": [
    {
      "bom-ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/org.examples.java/helloworld@1.0-SNAPSHOT?type=jar",
      "type": "library",
      "group": "org.examples.java",
      "name": "helloworld",
      "version": "1.0-SNAPSHOT",
      "licenses": [],
      "purl": "pkg:maven/org.examples.java/helloworld@1.0-SNAPSHOT?type=jar",
      "externalReferences": [
        {
          "url": "http://maven.apache.org",
          "type": "website"
        }
      ],
      "components": [
        {
          "bom-ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/junit/junit@4.12?type=jar",
          "type": "framework",
          "publisher": "JUnit",
          "group": "junit",
          "name": "junit",
          "version": "4.12",
          "description": "JUnit is a unit testing framework for Java, created by Erich Gamma and Kent Beck.",
          "scope": "required",
          "hashes": [
            {
              "alg": "MD5",
              "content": "5b38c40c97fbd0adee29f91e60405584"
            },
            {
              "alg": "SHA-1",
              "content": "2973d150c0dc1fefe998f834810d68f278ea58ec"
            },
            {
              "alg": "SHA-256",
              "content": "59721f0805e223d84b90677887d9ff567dc534d7c502ca903c0c2b17f05c116a"
            },
            {
              "alg": "SHA-512",
              "content": "5974670c3d178a12da5929ba5dd9b4f5ff461bdc1b92618c2c36d53e88650df7adbf3c1684017bb082b477cb8f40f15dcf7526f06f06183f93118ba9ebeaccce"
            },
            {
              "alg": "SHA-384",
              "content": "e2f0c2db405e282d0f84a1766b9e8d9736d4377e292a5ef8457aec10384f9077005865167025b2779634d75bcb4d62cd"
            },
            {
              "alg": "SHA3-384",
              "content": "a24a1d6d5ffe2f9fc3a90a442c3d1d5a12ae7bda3c68996c3b50f00186a2f961808c5ef504a771e9d6ab95ee38a383f0"
            },
            {
              "alg": "SHA3-256",
              "content": "02b1f076652120813646a0cb34350f0c73a3299b221567e089f6aaadf8ab444a"
            },
            {
              "alg": "SHA3-512",
              "content": "9e8f7057647c11564178e4569cf4f5682d3688b49d81acc60fd301f61053932ee9ac109c19cb639f7710d23afc76cb106ebde0f8143e2fe5fa08605201720a8b"
            }
          ],
          "licenses": [
            {
              "license": {
                "id": "EPL-1.0",
                "url": "http://www.eclipse.org/legal/epl-v10.html"
              }
            }
          ],
          "purl": "pkg:maven/junit/junit@4.12?type=jar",
          "externalReferences": [
            {
              "url": "http://junit.org",
              "type": "website"
            },
            {
              "url": "https://junit.ci.cloudbees.com/",
              "type": "build-system"
            },
            {
              "url": "https://github.com/junit-team/junit/wiki/Download-and-Install",
              "type": "distribution"
            },
            {
              "url": "https://oss.sonatype.org/service/local/staging/deploy/maven2/",
              "type": "distribution-intake"
            },
            {
              "url": "https://github.com/junit-team/junit/issues",
              "type": "issue-tracker"
            },
            {
              "url": "https://groups.yahoo.com/neo/groups/junit/info",
              "type": "mailing-list"
            },
            {
              "url": "http://github.com/junit-team/junit/tree/master",
              "type": "vcs"
            }
          ],
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/java/docker-java-sample/pom.xml"
            },
            {
              "name": "Namespaces",
              "value": "org.junit.ClassRule\norg.junit.Assert\norg.junit.After\norg.junit.rules.Stopwatch$Clock\norg.junit.rules.DisableOnDebug\norg.junit.rules.ExternalResource\norg.junit.rules.TestWatcher$1\norg.junit.rules.TemporaryFolder\norg.junit.rules.Timeout$Builder\norg.junit.rules.RunRules\norg.junit.rules.TestWatchman$1\norg.junit.rules.Verifier$1\norg.junit.rules.ExpectedException\norg.junit.rules.ExpectedException$ExpectedExceptionStatement\norg.junit.rules.RuleChain\norg.junit.rules.ErrorCollector$1\norg.junit.rules.TestRule\norg.junit.rules.Verifier\norg.junit.rules.Stopwatch\norg.junit.rules.Stopwatch$1\norg.junit.rules.Timeout\norg.junit.rules.ExpectedExceptionMatcherBuilder\norg.junit.rules.MethodRule\norg.junit.rules.Timeout$1\norg.junit.rules.ExternalResource$1\norg.junit.rules.TestWatchman\norg.junit.rules.ErrorCollector\norg.junit.rules.TestWatcher\norg.junit.rules.Stopwatch$InternalWatcher\norg.junit.rules.TestName\norg.junit.AssumptionViolatedException\norg.junit.ComparisonFailure$ComparisonCompactor$DiffExtractor\norg.junit.Assume\norg.junit.runners.AllTests\norg.junit.runners.Suite$SuiteClasses\norg.junit.runners.JUnit4\norg.junit.runners.ParentRunner$1\norg.junit.runners.BlockJUnit4ClassRunner\norg.junit.runners.Parameterized$Parameters\norg.junit.runners.MethodSorters\norg.junit.runners.ParentRunner$2\norg.junit.runners.ParentRunner$3\norg.junit.runners.Parameterized$UseParametersRunnerFactory\norg.junit.runners.ParentRunner$4\norg.junit.runners.ParentRunner\norg.junit.runners.BlockJUnit4ClassRunner$1\norg.junit.runners.Parameterized$Parameter\norg.junit.runners.parameterized.ParametersRunnerFactory\norg.junit.runners.parameterized.TestWithParameters\norg.junit.runners.parameterized.BlockJUnit4ClassRunnerWithParameters\norg.junit.runners.parameterized.BlockJUnit4ClassRunnerWithParametersFactory\norg.junit.runners.Suite\norg.junit.runners.model.MultipleFailureException\norg.junit.runners.model.RunnerScheduler\norg.junit.runners.model.NoGenericTypeParametersValidator\norg.junit.runners.model.TestClass$1\norg.junit.runners.model.RunnerBuilder\norg.junit.runners.model.Annotatable\norg.junit.runners.model.FrameworkField\norg.junit.runners.model.Statement\norg.junit.runners.model.TestTimedOutException\norg.junit.runners.model.FrameworkMember\norg.junit.runners.model.TestClass\norg.junit.runners.model.TestClass$FieldComparator\norg.junit.runners.model.FrameworkMethod\norg.junit.runners.model.TestClass$MethodComparator\norg.junit.runners.model.InitializationError\norg.junit.runners.model.FrameworkMethod$1\norg.junit.runners.Parameterized\norg.junit.ComparisonFailure\norg.junit.matchers.JUnitMatchers\norg.junit.Test$None\norg.junit.runner.FilterFactory\norg.junit.runner.Result\norg.junit.runner.JUnitCommandLineParseResult$CommandLineParserError\norg.junit.runner.Result$Listener\norg.junit.runner.JUnitCommandLineParseResult\norg.junit.runner.Describable\norg.junit.runner.FilterFactories\norg.junit.runner.Result$SerializedForm\norg.junit.runner.Runner\norg.junit.runner.RunWith\norg.junit.runner.manipulation.NoTestsRemainException\norg.junit.runner.manipulation.Sortable\norg.junit.runner.manipulation.Filter\norg.junit.runner.manipulation.Filter$2\norg.junit.runner.manipulation.Filter$3\norg.junit.runner.manipulation.Sorter\norg.junit.runner.manipulation.Sorter$1\norg.junit.runner.manipulation.Filterable\norg.junit.runner.manipulation.Filter$1\norg.junit.runner.JUnitCore\norg.junit.runner.FilterFactory$FilterNotCreatedException\norg.junit.runner.Result$1\norg.junit.runner.Request\norg.junit.runner.FilterFactoryParams\norg.junit.runner.Computer$1\norg.junit.runner.Request$1\norg.junit.runner.notification.Failure\norg.junit.runner.notification.RunNotifier\norg.junit.runner.notification.RunNotifier$1\norg.junit.runner.notification.RunNotifier$2\norg.junit.runner.notification.RunNotifier$3\norg.junit.runner.notification.RunListener$ThreadSafe\norg.junit.runner.notification.RunNotifier$4\norg.junit.runner.notification.SynchronizedRunListener\norg.junit.runner.notification.RunNotifier$SafeNotifier\norg.junit.runner.notification.RunNotifier$5\norg.junit.runner.notification.StoppedByUserException\norg.junit.runner.notification.RunNotifier$6\norg.junit.runner.notification.RunNotifier$7\norg.junit.runner.notification.RunListener\norg.junit.runner.Description\norg.junit.runner.Computer\norg.junit.validator.AnnotationsValidator$FieldValidator\norg.junit.validator.TestClassValidator\norg.junit.validator.ValidateWith\norg.junit.validator.AnnotationsValidator$AnnotatableValidator\norg.junit.validator.AnnotationsValidator$MethodValidator\norg.junit.validator.AnnotationsValidator$ClassValidator\norg.junit.validator.AnnotationValidatorFactory\norg.junit.validator.AnnotationValidator\norg.junit.validator.AnnotationsValidator$1\norg.junit.validator.AnnotationsValidator\norg.junit.validator.PublicClassValidator\norg.junit.ComparisonFailure$1\norg.junit.Ignore\norg.junit.BeforeClass\norg.junit.Before\norg.junit.Test\norg.junit.AfterClass\norg.junit.FixMethodOrder\norg.junit.ComparisonFailure$ComparisonCompactor\norg.junit.internal.ExactComparisonCriteria\norg.junit.internal.matchers.ThrowableMessageMatcher\norg.junit.internal.matchers.TypeSafeMatcher\norg.junit.internal.matchers.StaracePrintingMatcher\norg.junit.internal.matchers.ThrowableCauseMatcher\norg.junit.internal.ArrayComparisonFailure\norg.junit.internal.InexactComparisonCriteria\norg.junit.internal.TextListener\norg.junit.internal.MethodSorter\norg.junit.internal.JUnitSystem\norg.junit.internal.runners.JUnit38ClassRunner$OldTestClassAdaptingListener\norg.junit.internal.runners.JUnit4ClassRunner$1\norg.junit.internal.runners.MethodRoadie$2\norg.junit.internal.runners.TestMethod\norg.junit.internal.runners.rules.RuleMemberValidator\norg.junit.internal.runners.rules.RuleMemberValidator$MethodMustBeARule\norg.junit.internal.runners.rules.RuleMemberValidator$MemberMustBePublic\norg.junit.internal.runners.rules.ValidationError\norg.junit.internal.runners.rules.RuleMemberValidator$MemberMustBeStatic\norg.junit.internal.runners.rules.RuleMemberValidator$Builder\norg.junit.internal.runners.rules.RuleMemberValidator$MemberMustBeNonStaticOrAlsoClassRule\norg.junit.internal.runners.rules.RuleMemberValidator$FieldMustBeARule\norg.junit.internal.runners.rules.RuleMemberValidator$MethodMustBeATestRule\norg.junit.internal.runners.rules.RuleMemberValidator$RuleValidator\norg.junit.internal.runners.rules.RuleMemberValidator$1\norg.junit.internal.runners.rules.RuleMemberValidator$DeclaringClassMustBePublic\norg.junit.internal.runners.rules.RuleMemberValidator$FieldMustBeATestRule\norg.junit.internal.runners.MethodRoadie$1\norg.junit.internal.runners.TestClass\norg.junit.internal.runners.ErrorReportingRunner\norg.junit.internal.runners.JUnit4ClassRunner\norg.junit.internal.runners.FailedBefore\norg.junit.internal.runners.statements.FailOnTimeout$1\norg.junit.internal.runners.statements.Fail\norg.junit.internal.runners.statements.FailOnTimeout\norg.junit.internal.runners.statements.RunAfters\norg.junit.internal.runners.statements.RunBefores\norg.junit.internal.runners.statements.ExpectException\norg.junit.internal.runners.statements.InvokeMethod\norg.junit.internal.runners.statements.FailOnTimeout$Builder\norg.junit.internal.runners.statements.FailOnTimeout$CallableStatement\norg.junit.internal.runners.JUnit4ClassRunner$2\norg.junit.internal.runners.MethodValidator\norg.junit.internal.runners.JUnit38ClassRunner\norg.junit.internal.runners.SuiteMethod\norg.junit.internal.runners.MethodRoadie\norg.junit.internal.runners.InitializationError\norg.junit.internal.runners.ClassRoadie\norg.junit.internal.runners.JUnit38ClassRunner$1\norg.junit.internal.runners.MethodRoadie$1$1\norg.junit.internal.runners.model.ReflectiveCallable\norg.junit.internal.runners.model.EachTestNotifier\norg.junit.internal.runners.model.MultipleFailureException\norg.junit.internal.requests.FilterRequest\norg.junit.internal.requests.ClassRequest\norg.junit.internal.requests.SortingRequest\norg.junit.internal.AssumptionViolatedException\norg.junit.internal.RealSystem\norg.junit.internal.MethodSorter$2\norg.junit.internal.ComparisonCriteria\norg.junit.internal.Throwables\norg.junit.internal.MethodSorter$1\norg.junit.internal.Classes\norg.junit.internal.builders.IgnoredClassRunner\norg.junit.internal.builders.JUnit4Builder\norg.junit.internal.builders.AnnotatedBuilder\norg.junit.internal.builders.IgnoredBuilder\norg.junit.internal.builders.JUnit3Builder\norg.junit.internal.builders.AllDefaultPossibilitiesBuilder\norg.junit.internal.builders.NullBuilder\norg.junit.internal.builders.SuiteMethodBuilder\norg.junit.experimental.results.ResultMatchers$1\norg.junit.experimental.results.ResultMatchers$2\norg.junit.experimental.results.FailureList\norg.junit.experimental.results.ResultMatchers$3\norg.junit.experimental.results.ResultMatchers\norg.junit.experimental.results.PrintableResult\norg.junit.experimental.ParallelComputer$1\norg.junit.experimental.max.MaxHistory$RememberingListener\norg.junit.experimental.max.MaxCore\norg.junit.experimental.max.MaxHistory$1\norg.junit.experimental.max.MaxHistory$TestComparator\norg.junit.experimental.max.MaxCore$1\norg.junit.experimental.max.MaxCore$1$1\norg.junit.experimental.max.CouldNotReadCoreException\norg.junit.experimental.max.MaxHistory\norg.junit.experimental.ParallelComputer\norg.junit.experimental.theories.ParameterSignature\norg.junit.experimental.theories.Theories$TheoryAnchor$2\norg.junit.experimental.theories.Theories$TheoryAnchor\norg.junit.experimental.theories.Theory\norg.junit.experimental.theories.PotentialAssignment$1\norg.junit.experimental.theories.Theories$TheoryAnchor$1$1\norg.junit.experimental.theories.FromDataPoints\norg.junit.experimental.theories.DataPoints\norg.junit.experimental.theories.suppliers.TestedOnSupplier\norg.junit.experimental.theories.suppliers.TestedOn\norg.junit.experimental.theories.Theories$TheoryAnchor$1\norg.junit.experimental.theories.PotentialAssignment\norg.junit.experimental.theories.ParametersSuppliedBy\norg.junit.experimental.theories.Theories\norg.junit.experimental.theories.DataPoint\norg.junit.experimental.theories.internal.AllMembersSupplier$MethodParameterValue\norg.junit.experimental.theories.internal.AllMembersSupplier\norg.junit.experimental.theories.internal.EnumSupplier\norg.junit.experimental.theories.internal.Assignments\norg.junit.experimental.theories.internal.SpecificDataPointsSupplier\norg.junit.experimental.theories.internal.BooleanSupplier\norg.junit.experimental.theories.internal.AllMembersSupplier$1\norg.junit.experimental.theories.internal.ParameterizedAssertionError\norg.junit.experimental.theories.PotentialAssignment$CouldNotGenerateValueException\norg.junit.experimental.theories.ParameterSupplier\norg.junit.experimental.categories.ExcludeCategories$ExcludesAny\norg.junit.experimental.categories.IncludeCategories\norg.junit.experimental.categories.ExcludeCategories\norg.junit.experimental.categories.Categories$CategoryFilter\norg.junit.experimental.categories.Categories$ExcludeCategory\norg.junit.experimental.categories.CategoryValidator\norg.junit.experimental.categories.IncludeCategories$IncludesAny\norg.junit.experimental.categories.Category\norg.junit.experimental.categories.CategoryFilterFactory\norg.junit.experimental.categories.Categories\norg.junit.experimental.categories.Categories$IncludeCategory\norg.junit.experimental.runners.Enclosed\norg.junit.Rule\njunit.framework.TestCase\njunit.framework.TestResult\njunit.framework.TestFailure\njunit.framework.JUnit4TestAdapter\njunit.framework.TestResult$1\njunit.framework.TestSuite$1\njunit.framework.AssertionFailedError\njunit.framework.TestSuite\njunit.framework.ComparisonCompactor\njunit.framework.JUnit4TestAdapterCache\njunit.framework.Assert\njunit.framework.ComparisonFailure\njunit.framework.JUnit4TestCaseFacade\njunit.framework.TestListener\njunit.framework.Protectable\njunit.framework.JUnit4TestAdapterCache$1\njunit.framework.Test\njunit.runner.Version\njunit.runner.TestRunListener\njunit.runner.BaseTestRunner\njunit.extensions.TestDecorator\njunit.extensions.ActiveTestSuite$1\njunit.extensions.TestSetup\njunit.extensions.ActiveTestSuite\njunit.extensions.TestSetup$1\njunit.extensions.RepeatedTest\njunit.textui.TestRunner\njunit.textui.ResultPrinter"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 0.8,
              "methods": [
                {
                  "technique": "binary-analysis",
                  "confidence": 0.8,
                  "value": "/var/folders/ld/bx6fm65j2qdgtyp4xkvbkh9c0000gp/T/mvn-deps-3mgsEe/junit/junit/4.12/junit-4.12.jar"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/org.hamcrest/hamcrest-core@1.3?type=jar",
          "type": "framework",
          "group": "org.hamcrest",
          "name": "hamcrest-core",
          "version": "1.3",
          "description": "This is the core API of hamcrest matcher framework to be used by third-party framework providers. This includes the a foundation set of matcher implementations for common operations.",
          "scope": "required",
          "hashes": [
            {
              "alg": "MD5",
              "content": "6393363b47ddcbba82321110c3e07519"
            },
            {
              "alg": "SHA-1",
              "content": "42a25dc3219429f0e5d060061f71acb49bf010a0"
            },
            {
              "alg": "SHA-256",
              "content": "66fdef91e9739348df7a096aa384a5685f4e875584cce89386a7a47251c4d8e9"
            },
            {
              "alg": "SHA-512",
              "content": "e237ae735aac4fa5a7253ec693191f42ef7ddce384c11d29fbf605981c0be077d086757409acad53cb5b9e53d86a07cc428d459ff0f5b00d32a8cbbca390be49"
            },
            {
              "alg": "SHA-384",
              "content": "4b5297d2a12cc32b824153afc83f1ba9f1869ca288330f0a2f759659d09e4c420eb6ba4a1efbfa0657b625edd41293d5"
            },
            {
              "alg": "SHA3-384",
              "content": "b14d34985c0a78cf0ba19b5a18bffd403e08adcb2afde228ddef6e16121c7046dbebf58c04d3419311c4496c48aa93be"
            },
            {
              "alg": "SHA3-256",
              "content": "f679af77deedf69b3c3066f7916583848c6fd32a950f9c0b0e2ef1da121717ba"
            },
            {
              "alg": "SHA3-512",
              "content": "bca821931e438a1977b7b4356b5f8cebf485634f82159d505c48267c34e6a0f4fde9c2917331365f66dc0e52e2ca3a2db5256863584110c27ecebefc28741f63"
            }
          ],
          "licenses": [
            {
              "license": {
                "id": "BSD-3-Clause"
              }
            }
          ],
          "purl": "pkg:maven/org.hamcrest/hamcrest-core@1.3?type=jar",
          "externalReferences": [
            {
              "url": "https://github.com/hamcrest/JavaHamcrest/hamcrest-core",
              "type": "website"
            },
            {
              "url": "https://github.com/hamcrest/JavaHamcrest/hamcrest-core",
              "type": "vcs"
            }
          ],
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/java/docker-java-sample/pom.xml"
            },
            {
              "name": "Namespaces",
              "value": "org.hamcrest.BaseDescription\norg.hamcrest.BaseMatcher\norg.hamcrest.Condition$1\norg.hamcrest.Condition$Matched\norg.hamcrest.Condition$NotMatched\norg.hamcrest.Condition$Step\norg.hamcrest.Condition\norg.hamcrest.CoreMatchers\norg.hamcrest.CustomMatcher\norg.hamcrest.CustomTypeSafeMatcher\norg.hamcrest.Description$NullDescription\norg.hamcrest.Description\norg.hamcrest.DiagnosingMatcher\norg.hamcrest.Factory\norg.hamcrest.FeatureMatcher\norg.hamcrest.Matcher\norg.hamcrest.MatcherAssert\norg.hamcrest.SelfDescribing\norg.hamcrest.StringDescription\norg.hamcrest.TypeSafeDiagnosingMatcher\norg.hamcrest.TypeSafeMatcher\norg.hamcrest.core.AllOf\norg.hamcrest.core.AnyOf\norg.hamcrest.core.CombinableMatcher$CombinableBothMatcher\norg.hamcrest.core.CombinableMatcher$CombinableEitherMatcher\norg.hamcrest.core.CombinableMatcher\norg.hamcrest.core.DescribedAs\norg.hamcrest.core.Every\norg.hamcrest.core.Is\norg.hamcrest.core.IsAnything\norg.hamcrest.core.IsCollectionContaining\norg.hamcrest.core.IsEqual\norg.hamcrest.core.IsInstanceOf\norg.hamcrest.core.IsNot\norg.hamcrest.core.IsNull\norg.hamcrest.core.IsSame\norg.hamcrest.core.ShortcutCombination\norg.hamcrest.core.StringContains\norg.hamcrest.core.StringEndsWith\norg.hamcrest.core.StringStartsWith\norg.hamcrest.core.SubstringMatcher\norg.hamcrest.internal.ArrayIterator\norg.hamcrest.internal.ReflectiveTypeFinder\norg.hamcrest.internal.SelfDescribingValue\norg.hamcrest.internal.SelfDescribingValueIterator"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 0.8,
              "methods": [
                {
                  "technique": "binary-analysis",
                  "confidence": 0.8,
                  "value": "/var/folders/ld/bx6fm65j2qdgtyp4xkvbkh9c0000gp/T/mvn-deps-3mgsEe/org/hamcrest/hamcrest-core/1.3/hamcrest-core-1.3.jar"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/redis.clients/jedis@4.3.1?type=jar",
          "type": "library",
          "group": "redis.clients",
          "name": "jedis",
          "version": "4.3.1",
          "description": "Jedis is a blazingly small and sane Redis java client.",
          "scope": "required",
          "hashes": [
            {
              "alg": "MD5",
              "content": "eaca03c5afc8b8513ce2f2e8d68be4b0"
            },
            {
              "alg": "SHA-1",
              "content": "c780769bddbb1dbba2441c89af68e9fa126a32cb"
            },
            {
              "alg": "SHA-256",
              "content": "597894244e42e1b3171470e9294781824dbf617949e77aa0230eaa3ec4772db4"
            },
            {
              "alg": "SHA-512",
              "content": "b8f809669881cd69fee7a6994983e85853859343020bdaac2424051b93d4b48baf3b3c1d80af248184cb76bd3332916448b608910beaacc8401e307701a95d50"
            },
            {
              "alg": "SHA-384",
              "content": "b7b4d67b3b26bb932b42ac118d15bc9e210bb00dc8e067afc60651d0189b8f2bb4c529a226ace0a5b51551b12b902f0c"
            },
            {
              "alg": "SHA3-384",
              "content": "092e89f46b9657a6d2e65550c46649d2cd0f9e4be48dea61e1ca94d2d068d65ce2afdf3eb3d32e693ad0b93247d7ea7c"
            },
            {
              "alg": "SHA3-256",
              "content": "995459fa1458c1b9e5aed13c12096cee7a9b71a97ef7c39fb74ff019408f830b"
            },
            {
              "alg": "SHA3-512",
              "content": "c98637b0406817bce109b87c4951df264b45169056620fad006b14777db4f81fd780d9092dbb027c9c65e4aec237cd72e45e4949e1cb2754f0f493f1f7c7cf77"
            }
          ],
          "licenses": [
            {
              "license": {
                "id": "MIT",
                "url": "https://opensource.org/licenses/MIT"
              }
            }
          ],
          "purl": "pkg:maven/redis.clients/jedis@4.3.1?type=jar",
          "externalReferences": [
            {
              "url": "https://github.com/redis/jedis",
              "type": "website"
            },
            {
              "url": "https://oss.sonatype.org/service/local/staging/deploy/maven2/",
              "type": "distribution-intake"
            },
            {
              "url": "http://github.com/redis/jedis/issues",
              "type": "issue-tracker"
            },
            {
              "url": "http://groups.google.com/group/jedis_redis",
              "type": "mailing-list"
            },
            {
              "url": "scm:git:git@github.com:redis/jedis.git",
              "type": "vcs"
            }
          ],
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/java/docker-java-sample/pom.xml"
            },
            {
              "name": "Namespaces",
              "value": "redis.clients.jedis.BuilderFactory$7\nredis.clients.jedis.BuilderFactory$81\nredis.clients.jedis.ConnectionFactory\nredis.clients.jedis.params.LPosParams\nredis.clients.jedis.params.LolwutParams\nredis.clients.jedis.params.ZParams\nredis.clients.jedis.params.ZParams$Aggregate\nredis.clients.jedis.params.StrAlgoLCSParams\nredis.clients.jedis.params.ZIncrByParams\nredis.clients.jedis.params.Params\nredis.clients.jedis.params.XAddParams\nredis.clients.jedis.params.XPendingParams\nredis.clients.jedis.params.CommandListFilterByParams\nredis.clients.jedis.params.ZRangeParams\nredis.clients.jedis.params.ClientKillParams\nredis.clients.jedis.params.LCSParams\nredis.clients.jedis.util.JedisByteHashMap$ByteArrayWrapper\nredis.clients.jedis.util.RedisInputStream\nredis.clients.jedis.util.RedisOutputStream\nredis.clients.jedis.util.SafeEncoder\nredis.clients.jedis.util.Pool\nredis.clients.jedis.util.JedisClusterHashTag\nredis.clients.jedis.Protocol$ClusterKeyword\nredis.clients.jedis.BuilderFactory$29\nredis.clients.jedis.JedisPooled\nredis.clients.jedis.BuilderFactory$68\nredis.clients.jedis.BuilderFactory$27\nredis.clients.jedis.BuilderFactory$64\nredis.clients.jedis.CommandObjects\nredis.clients.jedis.commands.ListPipelineCommands\nredis.clients.jedis.commands.GeoCommands\nredis.clients.jedis.commands.SetBinaryCommands\nredis.clients.jedis.commands.ClientCommands\nredis.clients.jedis.commands.ScriptingControlCommands\nredis.clients.jedis.commands.FunctionBinaryCommands\nredis.clients.jedis.commands.FunctionCommands\nredis.clients.jedis.commands.StreamPipelineCommands\nredis.clients.jedis.commands.ScriptingKeyCommands\nredis.clients.jedis.search.IndexDefinition$Type\nredis.clients.jedis.search.Schema$FieldType\nredis.clients.jedis.search.RediSearchPipelineCommands\nredis.clients.jedis.search.RediSearchUtil\nredis.clients.jedis.search.querybuilder.Values$2\nredis.clients.jedis.search.querybuilder.Values$ScalableValue\nredis.clients.jedis.search.querybuilder.Node\nredis.clients.jedis.search.querybuilder.LongRangeValue\nredis.clients.jedis.search.querybuilder.Node$Parenthesize\nredis.clients.jedis.search.querybuilder.ValueNode\nredis.clients.jedis.search.querybuilder.Values\nredis.clients.jedis.search.querybuilder.GeoValue\nredis.clients.jedis.search.querybuilder.OptionalNode\nredis.clients.jedis.search.querybuilder.RangeValue\nredis.clients.jedis.search.Query$NumericFilter\nredis.clients.jedis.search.FieldName\nredis.clients.jedis.search.aggr.Reducers$3\nredis.clients.jedis.search.aggr.Reducers$1\nredis.clients.jedis.search.aggr.Reducers$2\nredis.clients.jedis.search.aggr.AggregationResult\nredis.clients.jedis.search.aggr.SortedField\nredis.clients.jedis.search.aggr.Reducers$4\nredis.clients.jedis.search.aggr.Reducer\nredis.clients.jedis.search.aggr.Reducers\nredis.clients.jedis.search.aggr.Limit\nredis.clients.jedis.search.Query\nredis.clients.jedis.search.LazyRawable\nredis.clients.jedis.search.Query$GeoFilter\nredis.clients.jedis.search.IndexDefinition\nredis.clients.jedis.search.schemafields.VectorField$1\nredis.clients.jedis.search.schemafields.TextField\nredis.clients.jedis.search.schemafields.GeoField\nredis.clients.jedis.search.schemafields.SchemaField\nredis.clients.jedis.UnifiedJedis\nredis.clients.jedis.JedisSocketFactory\nredis.clients.jedis.BuilderFactory$38\nredis.clients.jedis.BuilderFactory$66\nredis.clients.jedis.HostAndPortMapper\nredis.clients.jedis.bloom.RedisBloomProtocol$CuckooFilterCommand\nredis.clients.jedis.bloom.BFReserveParams\nredis.clients.jedis.bloom.RedisBloomProtocol$BloomFilterCommand\nredis.clients.jedis.bloom.commands.TDigestSketchCommands\nredis.clients.jedis.bloom.commands.CuckooFilterPipelineCommands\nredis.clients.jedis.bloom.commands.TopKFilterCommands\nredis.clients.jedis.bloom.commands.RedisBloomCommands\nredis.clients.jedis.bloom.commands.TDigestSketchPipelineCommands\nredis.clients.jedis.bloom.commands.CuckooFilterCommands\nredis.clients.jedis.bloom.commands.BloomFilterCommands\nredis.clients.jedis.bloom.commands.CountMinSketchPipelineCommands\nredis.clients.jedis.bloom.commands.RedisBloomPipelineCommands\nredis.clients.jedis.bloom.commands.BloomFilterPipelineCommands\nredis.clients.jedis.bloom.commands.CountMinSketchCommands\nredis.clients.jedis.bloom.commands.TopKFilterPipelineCommands\nredis.clients.jedis.bloom.RedisBloomProtocol$TopKCommand\nredis.clients.jedis.bloom.RedisBloomProtocol\nredis.clients.jedis.bloom.RedisBloomProtocol$CountMinSketchCommand\nredis.clients.jedis.bloom.CFReserveParams\nredis.clients.jedis.bloom.TDigestMergeParams\nredis.clients.jedis.Protocol$SentinelKeyword\nredis.clients.jedis.Builder\nredis.clients.jedis.TransactionBase\nredis.clients.jedis.BuilderFactory$72\nredis.clients.jedis.BuilderFactory$15\nredis.clients.jedis.BuilderFactory$21\nredis.clients.jedis.BuilderFactory$74\nredis.clients.jedis.json.Path\nredis.clients.jedis.json.JsonSetParams\nredis.clients.jedis.json.JsonProtocol$JsonCommand\nredis.clients.jedis.json.RedisJsonPipelineCommands\nredis.clients.jedis.json.JsonProtocol\nredis.clients.jedis.json.Path2\nredis.clients.jedis.json.RedisJsonCommands\nredis.clients.jedis.BuilderFactory$46\nredis.clients.jedis.BuilderFactory$69\nredis.clients.jedis.BuilderFactory$11\nredis.clients.jedis.ShardedCommandObjects\nredis.clients.jedis.ClusterCommandArguments\nredis.clients.jedis.BuilderFactory$6\nredis.clients.jedis.BuilderFactory$2\nredis.clients.jedis.BuilderFactory$24\nredis.clients.jedis.DefaultJedisClientConfig$Builder\nredis.clients.jedis.BuilderFactory$32\nredis.clients.jedis.BuilderFactory$SetFromList\nredis.clients.jedis.JedisSentinelPool\nredis.clients.jedis.HostAndPort\nredis.clients.jedis.BuilderFactory$1\nredis.clients.jedis.DefaultJedisSocketFactory\nredis.clients.jedis.executors.CommandExecutor\nredis.clients.jedis.executors.SimpleCommandExecutor\nredis.clients.jedis.executors.ClusterCommandExecutor\nredis.clients.jedis.executors.RetryableCommandExecutor\nredis.clients.jedis.BuilderFactory$31\nredis.clients.jedis.BuilderFactory$41\nredis.clients.jedis.ClusterPipeline\nredis.clients.jedis.ConnectionPool\nredis.clients.jedis.BuilderFactory$43\nredis.clients.jedis.DefaultJedisClientConfig\nredis.clients.jedis.BuilderFactory$30\nredis.clients.jedis.ClusterCommandObjects\nredis.clients.jedis.BuilderFactory$62\nredis.clients.jedis.JedisSentinelPool$MasterListener$1\nredis.clients.jedis.JedisCluster\nredis.clients.jedis.GeoCoordinate\nredis.clients.jedis.BuilderFactory$17\nredis.clients.jedis.StreamEntryID$4\nredis.clients.jedis.BuilderFactory$3\nredis.clients.jedis.BuilderFactory$34\nredis.clients.jedis.BuilderFactory$75\nredis.clients.jedis.BuilderFactory$12\nredis.clients.jedis.BuilderFactory$33\nredis.clients.jedis.JedisClusterInfoCache\nredis.clients.jedis.JedisMonitor\nredis.clients.jedis.BuilderFactory$23\nredis.clients.jedis.BuilderFactory$13\nredis.clients.jedis.exceptions.JedisClusterOperationException\nredis.clients.jedis.exceptions.JedisAccessControlException\nredis.clients.jedis.exceptions.JedisBusyException\nredis.clients.jedis.exceptions.JedisDataException\nredis.clients.jedis.exceptions.JedisNoScriptException\nredis.clients.jedis.exceptions.JedisClusterException\nredis.clients.jedis.exceptions.JedisRedirectionException\nredis.clients.jedis.exceptions.JedisMovedDataException\nredis.clients.jedis.exceptions.AbortedTransactionException\nredis.clients.jedis.exceptions.JedisConnectionException\nredis.clients.jedis.exceptions.InvalidURIException\nredis.clients.jedis.exceptions.JedisAskDataException\nredis.clients.jedis.exceptions.JedisException\nredis.clients.jedis.CommandObjects$GsonObjectBuilder\nredis.clients.jedis.BuilderFactory$16\nredis.clients.jedis.ConnectionPoolConfig\nredis.clients.jedis.StreamEntryID$1\nredis.clients.jedis.BuilderFactory$77\nredis.clients.jedis.BuilderFactory$44\nredis.clients.jedis.BuilderFactory$57\nredis.clients.jedis.BuilderFactory$47\nredis.clients.jedis.Protocol$Keyword\nredis.clients.jedis.args.RawableFactory$Raw\nredis.clients.jedis.args.SortingOrder\nredis.clients.jedis.args.ListPosition\nredis.clients.jedis.args.BitOP\nredis.clients.jedis.args.SaveMode\nredis.clients.jedis.args.ListDirection\nredis.clients.jedis.args.RawableFactory$RawString\nredis.clients.jedis.BuilderFactory$35\nredis.clients.jedis.ShardedPipeline\nredis.clients.jedis.BuilderFactory$26\nredis.clients.jedis.JedisPool\nredis.clients.jedis.BuilderFactory$63\nredis.clients.jedis.BuilderFactory$56\nredis.clients.jedis.BuilderFactory\nredis.clients.jedis.JedisPoolConfig\nredis.clients.jedis.BuilderFactory$73\nredis.clients.jedis.Protocol$ResponseKeyword\nredis.clients.jedis.BuilderFactory$65\nredis.clients.jedis.BuilderFactory$79\nredis.clients.jedis.Jedis\nredis.clients.jedis.graph.GraphProtocol\nredis.clients.jedis.graph.RedisGraphCommands\nredis.clients.jedis.graph.ResultSet\nredis.clients.jedis.graph.RedisGraphQueryUtil\nredis.clients.jedis.graph.GraphProtocol$GraphKeyword\nredis.clients.jedis.graph.GraphCommandObjects$GraphCacheImpl\nredis.clients.jedis.graph.GraphCommandObjects$GraphCacheList\nredis.clients.jedis.graph.Statistics\nredis.clients.jedis.graph.GraphQueryParams\nredis.clients.jedis.graph.ResultSetBuilder$HeaderImpl\nredis.clients.jedis.graph.GraphProtocol$GraphCommand\nredis.clients.jedis.graph.ResultSetBuilder$1\nredis.clients.jedis.graph.ResultSet$ColumnType\nredis.clients.jedis.graph.ResultSetBuilder$StatisticsImpl\nredis.clients.jedis.graph.RedisGraphPipelineCommands\nredis.clients.jedis.graph.GraphCache\nredis.clients.jedis.graph.Record\nredis.clients.jedis.graph.Header\nredis.clients.jedis.graph.entities.Path\nredis.clients.jedis.graph.entities.Node\nredis.clients.jedis.graph.entities.Point\nredis.clients.jedis.graph.entities.GraphEntity\nredis.clients.jedis.graph.entities.Property\nredis.clients.jedis.graph.entities.Edge\nredis.clients.jedis.graph.ResultSetBuilder$ResultSetImpl\nredis.clients.jedis.graph.ResultSetBuilder$RecordImpl\nredis.clients.jedis.graph.ResultSetBuilder\nredis.clients.jedis.StreamEntryID\nredis.clients.jedis.params.XAutoClaimParams\nredis.clients.jedis.params.XTrimParams\nredis.clients.jedis.params.MigrateParams\nredis.clients.jedis.params.ScanParams\nredis.clients.jedis.params.FailoverParams\nredis.clients.jedis.params.GeoRadiusParam\nredis.clients.jedis.params.SortingParams\nredis.clients.jedis.params.GeoAddParams\nredis.clients.jedis.params.ClientKillParams$SkipMe\nredis.clients.jedis.params.ZAddParams\nredis.clients.jedis.params.XReadGroupParams\nredis.clients.jedis.params.RestoreParams\nredis.clients.jedis.params.XClaimParams\nredis.clients.jedis.params.SetParams\nredis.clients.jedis.params.XReadParams\nredis.clients.jedis.params.GetExParams\nredis.clients.jedis.params.GeoSearchParam\nredis.clients.jedis.params.BitPosParams\nredis.clients.jedis.params.ShutdownParams\nredis.clients.jedis.params.IParams\nredis.clients.jedis.params.GeoRadiusStoreParam\nredis.clients.jedis.BuilderFactory$54\nredis.clients.jedis.BuilderFactory$60\nredis.clients.jedis.BuilderFactory$48\nredis.clients.jedis.BuilderFactory$61\nredis.clients.jedis.timeseries.TSCreateParams\nredis.clients.jedis.timeseries.AggregationType\nredis.clients.jedis.timeseries.TSKeyValue\nredis.clients.jedis.timeseries.TimeSeriesProtocol\nredis.clients.jedis.timeseries.TSElement\nredis.clients.jedis.timeseries.TSKeyedElements\nredis.clients.jedis.timeseries.TimeSeriesProtocol$TimeSeriesCommand\nredis.clients.jedis.timeseries.RedisTimeSeriesCommands\nredis.clients.jedis.timeseries.DuplicatePolicy\nredis.clients.jedis.timeseries.TSMRangeParams\nredis.clients.jedis.timeseries.TSGetParams\nredis.clients.jedis.timeseries.TSRangeParams\nredis.clients.jedis.timeseries.RedisTimeSeriesPipelineCommands\nredis.clients.jedis.timeseries.TSInfo$1\nredis.clients.jedis.timeseries.TSAlterParams\nredis.clients.jedis.timeseries.TSInfo\nredis.clients.jedis.timeseries.TSInfo$Rule\nredis.clients.jedis.timeseries.TSMGetParams\nredis.clients.jedis.timeseries.TimeSeriesProtocol$TimeSeriesKeyword\nredis.clients.jedis.util.MurmurHash\nredis.clients.jedis.util.ByteArrayComparator\nredis.clients.jedis.util.Hashing\nredis.clients.jedis.util.KeyValue\nredis.clients.jedis.util.IOUtils\nredis.clients.jedis.util.JedisClusterCRC16\nredis.clients.jedis.util.JedisByteHashMap\nredis.clients.jedis.util.Hashing$1\nredis.clients.jedis.util.DoublePrecision\nredis.clients.jedis.util.JedisURIHelper\nredis.clients.jedis.util.JedisByteHashMap$JedisByteEntry\nredis.clients.jedis.BuilderFactory$18\nredis.clients.jedis.BuilderFactory$37\nredis.clients.jedis.commands.ScriptingKeyPipelineCommands\nredis.clients.jedis.commands.SortedSetBinaryCommands\nredis.clients.jedis.commands.ControlBinaryCommands\nredis.clients.jedis.commands.DatabaseCommands\nredis.clients.jedis.commands.StringBinaryCommands\nredis.clients.jedis.commands.SetCommands\nredis.clients.jedis.commands.SlowlogCommands\nredis.clients.jedis.commands.StreamCommands\nredis.clients.jedis.commands.PipelineBinaryCommands\nredis.clients.jedis.commands.StringCommands\nredis.clients.jedis.commands.ListCommands\nredis.clients.jedis.commands.SampleBinaryKeyedPipelineCommands\nredis.clients.jedis.commands.ListPipelineBinaryCommands\nredis.clients.jedis.commands.HyperLogLogPipelineCommands\nredis.clients.jedis.commands.SortedSetPipelineCommands\nredis.clients.jedis.commands.GeoBinaryCommands\nredis.clients.jedis.commands.ProtocolCommand\nredis.clients.jedis.commands.FunctionPipelineCommands\nredis.clients.jedis.commands.KeyPipelineCommands\nredis.clients.jedis.commands.KeyCommands\nredis.clients.jedis.commands.GeoPipelineBinaryCommands\nredis.clients.jedis.commands.RedisModuleCommands\nredis.clients.jedis.commands.HashPipelineCommands\nredis.clients.jedis.commands.FunctionPipelineBinaryCommands\nredis.clients.jedis.commands.SampleBinaryKeyedCommands\nredis.clients.jedis.commands.ClusterCommands\nredis.clients.jedis.commands.JedisBinaryCommands\nredis.clients.jedis.commands.SetPipelineBinaryCommands\nredis.clients.jedis.commands.StringPipelineBinaryCommands\nredis.clients.jedis.commands.ServerCommands\nredis.clients.jedis.commands.SampleKeyedCommands\nredis.clients.jedis.commands.StreamPipelineBinaryCommands\nredis.clients.jedis.commands.HyperLogLogBinaryCommands\nredis.clients.jedis.commands.ControlCommands\nredis.clients.jedis.commands.StreamBinaryCommands\nredis.clients.jedis.commands.GenericControlCommands\nredis.clients.jedis.commands.SentinelCommands\nredis.clients.jedis.commands.HyperLogLogCommands\nredis.clients.jedis.commands.PipelineCommands\nredis.clients.jedis.commands.AccessControlLogCommands\nredis.clients.jedis.commands.SampleKeyedPipelineCommands\nredis.clients.jedis.commands.ScriptingKeyBinaryCommands\nredis.clients.jedis.commands.JedisCommands\nredis.clients.jedis.commands.ModuleCommands\nredis.clients.jedis.commands.DatabasePipelineCommands\nredis.clients.jedis.commands.HashCommands\nredis.clients.jedis.commands.HashBinaryCommands\nredis.clients.jedis.commands.ConfigCommands\nredis.clients.jedis.commands.ScriptingKeyPipelineBinaryCommands\nredis.clients.jedis.commands.ListBinaryCommands\nredis.clients.jedis.commands.HashPipelineBinaryCommands\nredis.clients.jedis.commands.GeoPipelineCommands\nredis.clients.jedis.commands.SortedSetCommands\nredis.clients.jedis.commands.SortedSetPipelineBinaryCommands\nredis.clients.jedis.commands.StringPipelineCommands\nredis.clients.jedis.commands.CommandCommands\nredis.clients.jedis.commands.AccessControlLogBinaryCommands\nredis.clients.jedis.commands.HyperLogLogPipelineBinaryCommands\nredis.clients.jedis.commands.KeyBinaryCommands\nredis.clients.jedis.commands.RedisModulePipelineCommands\nredis.clients.jedis.commands.KeyPipelineBinaryCommands\nredis.clients.jedis.commands.ClientBinaryCommands\nredis.clients.jedis.commands.SetPipelineCommands\nredis.clients.jedis.search.FTSearchParams$SummarizeParams\nredis.clients.jedis.search.IndexOptions\nredis.clients.jedis.search.Schema$TagField\nredis.clients.jedis.search.FTSearchParams$HighlightParams\nredis.clients.jedis.search.FTSearchParams\nredis.clients.jedis.search.RediSearchCommands\nredis.clients.jedis.search.SearchResult$SearchResultBuilder\nredis.clients.jedis.search.Schema\nredis.clients.jedis.search.FTCreateParams\nredis.clients.jedis.search.Schema$Field\nredis.clients.jedis.search.SearchProtocol\nredis.clients.jedis.search.FTSearchParams$GeoFilter\nredis.clients.jedis.search.SearchResult\nredis.clients.jedis.search.Query$Paging\nredis.clients.jedis.search.SearchProtocol$SearchKeyword\nredis.clients.jedis.search.querybuilder.DisjunctUnionNode\nredis.clients.jedis.search.querybuilder.IntersectNode\nredis.clients.jedis.search.querybuilder.DoubleRangeValue\nredis.clients.jedis.search.querybuilder.Values$1\nredis.clients.jedis.search.querybuilder.QueryBuilders\nredis.clients.jedis.search.querybuilder.DisjunctNode\nredis.clients.jedis.search.querybuilder.Value\nredis.clients.jedis.search.querybuilder.UnionNode\nredis.clients.jedis.search.querybuilder.QueryNode\nredis.clients.jedis.search.Query$HighlightTags\nredis.clients.jedis.search.Document\nredis.clients.jedis.search.SearchProtocol$SearchCommand\nredis.clients.jedis.search.aggr.Reducers$5\nredis.clients.jedis.search.aggr.AggregationBuilder\nredis.clients.jedis.search.aggr.Row\nredis.clients.jedis.search.aggr.Group\nredis.clients.jedis.search.aggr.SortedField$SortOrder\nredis.clients.jedis.search.Schema$TextField\nredis.clients.jedis.search.FTSearchParams$NumericFilter\nredis.clients.jedis.search.SearchResult$1\nredis.clients.jedis.search.Query$Filter\nredis.clients.jedis.search.Schema$VectorField$VectorAlgo\nredis.clients.jedis.search.IndexDataType\nredis.clients.jedis.search.Schema$VectorField\nredis.clients.jedis.search.schemafields.VectorField$VectorAlgorithm\nredis.clients.jedis.search.schemafields.NumericField\nredis.clients.jedis.search.schemafields.TagField\nredis.clients.jedis.search.schemafields.VectorField$Builder\nredis.clients.jedis.search.schemafields.VectorField\nredis.clients.jedis.BuilderFactory$58\nredis.clients.jedis.BuilderFactory$10\nredis.clients.jedis.BuilderFactory$40\nredis.clients.jedis.Connection\nredis.clients.jedis.bloom.RedisBloomProtocol$TDigestCommand\nredis.clients.jedis.bloom.BFInsertParams\nredis.clients.jedis.bloom.CFInsertParams\nredis.clients.jedis.bloom.RedisBloomProtocol$RedisBloomKeyword\nredis.clients.jedis.providers.ShardedConnectionProvider\nredis.clients.jedis.providers.PooledConnectionProvider\nredis.clients.jedis.providers.ClusterConnectionProvider\nredis.clients.jedis.providers.ManagedConnectionProvider\nredis.clients.jedis.providers.ConnectionProvider\nredis.clients.jedis.BuilderFactory$20\nredis.clients.jedis.resps.GeoRadiusResponse\nredis.clients.jedis.resps.LibraryInfo\nredis.clients.jedis.resps.StreamInfo\nredis.clients.jedis.resps.LCSMatchResult\nredis.clients.jedis.resps.FunctionStats\nredis.clients.jedis.resps.KeyedListElement\nredis.clients.jedis.resps.StreamConsumersInfo\nredis.clients.jedis.resps.AccessControlLogEntry\nredis.clients.jedis.resps.StreamGroupInfo\nredis.clients.jedis.resps.LCSMatchResult$MatchedPosition\nredis.clients.jedis.resps.CommandInfo$1\nredis.clients.jedis.resps.ScanResult\nredis.clients.jedis.resps.LCSMatchResult$Position\nredis.clients.jedis.resps.CommandDocument\nredis.clients.jedis.resps.StreamEntry\nredis.clients.jedis.resps.StreamGroupFullInfo\nredis.clients.jedis.resps.KeyedZSetElement\nredis.clients.jedis.resps.StreamConsumerFullInfo\nredis.clients.jedis.resps.StreamFullInfo\nredis.clients.jedis.resps.StreamPendingEntry\nredis.clients.jedis.resps.FunctionStats$1\nredis.clients.jedis.resps.StreamPendingSummary\nredis.clients.jedis.resps.CommandDocument$1\nredis.clients.jedis.resps.CommandInfo\nredis.clients.jedis.resps.LibraryInfo$1\nredis.clients.jedis.resps.Slowlog\nredis.clients.jedis.resps.AccessControlUser\nredis.clients.jedis.resps.Tuple\nredis.clients.jedis.BuilderFactory$76\nredis.clients.jedis.BuilderFactory$25\nredis.clients.jedis.Module\nredis.clients.jedis.Queable\nredis.clients.jedis.BuilderFactory$67\nredis.clients.jedis.JedisSharding\nredis.clients.jedis.BuilderFactory$45\nredis.clients.jedis.BuilderFactory$59\nredis.clients.jedis.BuilderFactory$78\nredis.clients.jedis.Response\nredis.clients.jedis.BuilderFactory$82\nredis.clients.jedis.BuilderFactory$22\nredis.clients.jedis.BuilderFactory$4\nredis.clients.jedis.BuilderFactory$42\nredis.clients.jedis.BuilderFactory$36\nredis.clients.jedis.StreamEntryID$3\nredis.clients.jedis.Protocol\nredis.clients.jedis.BuilderFactory$28\nredis.clients.jedis.Transaction\nredis.clients.jedis.BuilderFactory$49\nredis.clients.jedis.JedisSentinelPool$MasterListener\nredis.clients.jedis.StreamEntryID$5\nredis.clients.jedis.JedisPubSub\nredis.clients.jedis.CommandObject\nredis.clients.jedis.BuilderFactory$80\nredis.clients.jedis.BuilderFactory$5\nredis.clients.jedis.BuilderFactory$50\nredis.clients.jedis.DefaultJedisClientConfig$1\nredis.clients.jedis.BuilderFactory$71\nredis.clients.jedis.StreamEntryID$2\nredis.clients.jedis.JedisClientConfig\nredis.clients.jedis.BuilderFactory$53\nredis.clients.jedis.CommandArguments\nredis.clients.jedis.BuilderFactory$52\nredis.clients.jedis.BuilderFactory$70\nredis.clients.jedis.JedisFactory\nredis.clients.jedis.ShardedCommandArguments\nredis.clients.jedis.Protocol$Command\nredis.clients.jedis.Pipeline\nredis.clients.jedis.executors.DefaultCommandExecutor\nredis.clients.jedis.BuilderFactory$9\nredis.clients.jedis.BuilderFactory$55\nredis.clients.jedis.ReliableTransaction\nredis.clients.jedis.args.RawableFactory\nredis.clients.jedis.args.FunctionRestorePolicy\nredis.clients.jedis.args.ClientPauseMode\nredis.clients.jedis.args.ClusterFailoverOption\nredis.clients.jedis.args.ExpiryOption\nredis.clients.jedis.args.Rawable\nredis.clients.jedis.args.BitCountOption\nredis.clients.jedis.args.UnblockType\nredis.clients.jedis.args.ClusterResetType\nredis.clients.jedis.args.SortedSetOption\nredis.clients.jedis.args.GeoUnit\nredis.clients.jedis.args.FlushMode\nredis.clients.jedis.args.ClientType\nredis.clients.jedis.BinaryJedisPubSub\nredis.clients.jedis.BuilderFactory$19\nredis.clients.jedis.BuilderFactory$14\nredis.clients.jedis.BuilderFactory$51\nredis.clients.jedis.BuilderFactory$8\nredis.clients.jedis.CommandObjects$GsonObjectListBuilder\nredis.clients.jedis.MultiNodePipelineBase\nredis.clients.jedis.BuilderFactory$39\nredis.clients.jedis.graph.ResultSetBuilder$ScalarType\nredis.clients.jedis.graph.GraphCommandObjects"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 0.8,
              "methods": [
                {
                  "technique": "binary-analysis",
                  "confidence": 0.8,
                  "value": "/var/folders/ld/bx6fm65j2qdgtyp4xkvbkh9c0000gp/T/mvn-deps-3mgsEe/redis/clients/jedis/4.3.1/jedis-4.3.1.jar"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/org.slf4j/slf4j-api@1.7.36?type=jar",
          "type": "framework",
          "publisher": "QOS.ch",
          "group": "org.slf4j",
          "name": "slf4j-api",
          "version": "1.7.36",
          "description": "The slf4j API",
          "scope": "required",
          "hashes": [
            {
              "alg": "MD5",
              "content": "872da51f5de7f3923da4de871d57fd85"
            },
            {
              "alg": "SHA-1",
              "content": "6c62681a2f655b49963a5983b8b0950a6120ae14"
            },
            {
              "alg": "SHA-256",
              "content": "d3ef575e3e4979678dc01bf1dcce51021493b4d11fb7f1be8ad982877c16a1c0"
            },
            {
              "alg": "SHA-512",
              "content": "f9b033fc019a44f98b16048da7e2b59edd4a6a527ba60e358f65ab88e0afae03a9340f1b3e8a543d49fa542290f499c5594259affa1ff3e6e7bf3b428d4c610b"
            },
            {
              "alg": "SHA-384",
              "content": "2b14ad035877087157e379d3277dcdcd79e58d6bdb147c47d29e377d75ce53ad42cafbf22f5fb7827c7e946ff4876b9a"
            },
            {
              "alg": "SHA3-384",
              "content": "3bc3110dafb8d5be16a39f3b2671a466463cd99eb39610c0e4719a7bf2d928f2ea213c734887c6926a07c4cca7769e4b"
            },
            {
              "alg": "SHA3-256",
              "content": "ba2608179fcf46e2291a90b9cbb4aa30d718e481f59c350cc21c73b88d826881"
            },
            {
              "alg": "SHA3-512",
              "content": "14c4edcd19702ef607d78826839d8a6d3a39157df54b89a801d3d3cbbe1307131a77671b041c761122730fb1387888c5ec2e46bdd80e1cb07f8f144676441824"
            }
          ],
          "licenses": [
            {
              "license": {
                "id": "MIT",
                "url": "https://opensource.org/licenses/MIT"
              }
            }
          ],
          "purl": "pkg:maven/org.slf4j/slf4j-api@1.7.36?type=jar",
          "externalReferences": [
            {
              "url": "http://www.slf4j.org",
              "type": "website"
            },
            {
              "url": "https://oss.sonatype.org/service/local/staging/deploy/maven2/",
              "type": "distribution-intake"
            },
            {
              "url": "https://github.com/qos-ch/slf4j/slf4j-api",
              "type": "vcs"
            }
          ],
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/java/docker-java-sample/pom.xml"
            },
            {
              "name": "Namespaces",
              "value": "org.slf4j.ILoggerFactory\norg.slf4j.IMarkerFactory\norg.slf4j.Logger\norg.slf4j.LoggerFactory\norg.slf4j.MDC$1\norg.slf4j.MDC$MDCCloseable\norg.slf4j.MDC\norg.slf4j.Marker\norg.slf4j.MarkerFactory\norg.slf4j.event.EventConstants\norg.slf4j.event.EventRecodingLogger\norg.slf4j.event.Level\norg.slf4j.event.LoggingEvent\norg.slf4j.event.SubstituteLoggingEvent\norg.slf4j.helpers.BasicMDCAdapter$1\norg.slf4j.helpers.BasicMDCAdapter\norg.slf4j.helpers.BasicMarker\norg.slf4j.helpers.BasicMarkerFactory\norg.slf4j.helpers.FormattingTuple\norg.slf4j.helpers.MarkerIgnoringBase\norg.slf4j.helpers.MessageFormatter\norg.slf4j.helpers.NOPLogger\norg.slf4j.helpers.NOPLoggerFactory\norg.slf4j.helpers.NOPMDCAdapter\norg.slf4j.helpers.NamedLoggerBase\norg.slf4j.helpers.SubstituteLogger\norg.slf4j.helpers.SubstituteLoggerFactory\norg.slf4j.helpers.Util$1\norg.slf4j.helpers.Util$ClassContextSecurityManager\norg.slf4j.helpers.Util\norg.slf4j.spi.LocationAwareLogger\norg.slf4j.spi.LoggerFactoryBinder\norg.slf4j.spi.MDCAdapter\norg.slf4j.spi.MarkerFactoryBinder"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 0.8,
              "methods": [
                {
                  "technique": "binary-analysis",
                  "confidence": 0.8,
                  "value": "/var/folders/ld/bx6fm65j2qdgtyp4xkvbkh9c0000gp/T/mvn-deps-3mgsEe/org/slf4j/slf4j-api/1.7.36/slf4j-api-1.7.36.jar"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/org.apache.commons/commons-pool2@2.11.1?type=jar",
          "type": "framework",
          "publisher": "The Apache Software Foundation",
          "group": "org.apache.commons",
          "name": "commons-pool2",
          "version": "2.11.1",
          "description": "The Apache Commons Object Pooling Library.",
          "scope": "required",
          "hashes": [
            {
              "alg": "MD5",
              "content": "2210a041929e7c94485d5402458340b9"
            },
            {
              "alg": "SHA-1",
              "content": "8970fd110c965f285ed4c6e40be7630c62db6f68"
            },
            {
              "alg": "SHA-256",
              "content": "ea0505ee7515e58b1ac0e686e4d1a5d9f7d808e251a61bc371aa0595b9963f83"
            },
            {
              "alg": "SHA-512",
              "content": "7177d8a9e45ae47881ec323150dc7bd3372ce32eff9866029b47a77cb734535d5e987f22e6cb7009104832c3772079fb6322b2919650765b76a4b4aa8eae648e"
            },
            {
              "alg": "SHA-384",
              "content": "c77e99c898da417d33b035745e6f827d47f3c9a5f159764d1e31f0f0ee0b0b3569929495013db6c4d84922c78a3325cf"
            },
            {
              "alg": "SHA3-384",
              "content": "ba6e6d5a0e8d9e4778e619d8303ebba6c56bcd70169372e420067f3961cf98bd2631f177ac084d5dc1ad0790767816fe"
            },
            {
              "alg": "SHA3-256",
              "content": "985483edbf54bb59552633f3584ca0e484e2a0c471fafd7b2643809da874aea1"
            },
            {
              "alg": "SHA3-512",
              "content": "2757b5a8bd74bae36ad48a6102405457774d0aed03afdbe46cc804ed02f58dd484d637a0341195bb12bbcd8f3083ee3a644105734c0128fccfbe045cdf6b4491"
            }
          ],
          "licenses": [
            {
              "license": {
                "id": "Apache-2.0"
              }
            }
          ],
          "purl": "pkg:maven/org.apache.commons/commons-pool2@2.11.1?type=jar",
          "externalReferences": [
            {
              "url": "https://commons.apache.org/proper/commons-pool/",
              "type": "website"
            },
            {
              "url": "https://builds.apache.org/",
              "type": "build-system"
            },
            {
              "url": "https://repository.apache.org/service/local/staging/deploy/maven2",
              "type": "distribution-intake"
            },
            {
              "url": "https://issues.apache.org/jira/browse/POOL",
              "type": "issue-tracker"
            },
            {
              "url": "https://mail-archives.apache.org/mod_mbox/commons-user/",
              "type": "mailing-list"
            },
            {
              "url": "https://gitbox.apache.org/repos/asf?p=commons-pool.git",
              "type": "vcs"
            }
          ],
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/java/docker-java-sample/pom.xml"
            },
            {
              "name": "Namespaces",
              "value": "org.apache.commons.pool2.BaseKeyedPooledObjectFactory\norg.apache.commons.pool2.BaseObject\norg.apache.commons.pool2.BaseObjectPool\norg.apache.commons.pool2.BasePooledObjectFactory\norg.apache.commons.pool2.DestroyMode\norg.apache.commons.pool2.KeyedObjectPool\norg.apache.commons.pool2.KeyedPooledObjectFactory\norg.apache.commons.pool2.ObjectPool\norg.apache.commons.pool2.PoolUtils$ErodingFactor\norg.apache.commons.pool2.PoolUtils$ErodingKeyedObjectPool\norg.apache.commons.pool2.PoolUtils$ErodingObjectPool\norg.apache.commons.pool2.PoolUtils$ErodingPerKeyKeyedObjectPool\norg.apache.commons.pool2.PoolUtils$KeyedObjectPoolMinIdleTimerTask\norg.apache.commons.pool2.PoolUtils$ObjectPoolMinIdleTimerTask\norg.apache.commons.pool2.PoolUtils$SynchronizedKeyedObjectPool\norg.apache.commons.pool2.PoolUtils$SynchronizedKeyedPooledObjectFactory\norg.apache.commons.pool2.PoolUtils$SynchronizedObjectPool\norg.apache.commons.pool2.PoolUtils$SynchronizedPooledObjectFactory\norg.apache.commons.pool2.PoolUtils$TimerHolder\norg.apache.commons.pool2.PoolUtils\norg.apache.commons.pool2.PooledObject\norg.apache.commons.pool2.PooledObjectFactory\norg.apache.commons.pool2.PooledObjectState\norg.apache.commons.pool2.SwallowedExceptionListener\norg.apache.commons.pool2.TrackedUse\norg.apache.commons.pool2.UsageTracking\norg.apache.commons.pool2.impl.AbandonedConfig\norg.apache.commons.pool2.impl.BaseGenericObjectPool$EvictionIterator\norg.apache.commons.pool2.impl.BaseGenericObjectPool$Evictor\norg.apache.commons.pool2.impl.BaseGenericObjectPool$IdentityWrapper\norg.apache.commons.pool2.impl.BaseGenericObjectPool$StatsStore\norg.apache.commons.pool2.impl.BaseGenericObjectPool\norg.apache.commons.pool2.impl.BaseObjectPoolConfig\norg.apache.commons.pool2.impl.CallStack\norg.apache.commons.pool2.impl.CallStackUtils\norg.apache.commons.pool2.impl.DefaultEvictionPolicy\norg.apache.commons.pool2.impl.DefaultPooledObject\norg.apache.commons.pool2.impl.DefaultPooledObjectInfo\norg.apache.commons.pool2.impl.DefaultPooledObjectInfoMBean\norg.apache.commons.pool2.impl.EvictionConfig\norg.apache.commons.pool2.impl.EvictionPolicy\norg.apache.commons.pool2.impl.EvictionTimer$1\norg.apache.commons.pool2.impl.EvictionTimer$EvictorThreadFactory\norg.apache.commons.pool2.impl.EvictionTimer$Reaper\norg.apache.commons.pool2.impl.EvictionTimer$WeakRunner\norg.apache.commons.pool2.impl.EvictionTimer\norg.apache.commons.pool2.impl.GenericKeyedObjectPool$ObjectDeque\norg.apache.commons.pool2.impl.GenericKeyedObjectPool\norg.apache.commons.pool2.impl.GenericKeyedObjectPoolConfig\norg.apache.commons.pool2.impl.GenericKeyedObjectPoolMXBean\norg.apache.commons.pool2.impl.GenericObjectPool\norg.apache.commons.pool2.impl.GenericObjectPoolConfig\norg.apache.commons.pool2.impl.GenericObjectPoolMXBean\norg.apache.commons.pool2.impl.InterruptibleReentrantLock\norg.apache.commons.pool2.impl.LinkedBlockingDeque$1\norg.apache.commons.pool2.impl.LinkedBlockingDeque$AbstractItr\norg.apache.commons.pool2.impl.LinkedBlockingDeque$DescendingItr\norg.apache.commons.pool2.impl.LinkedBlockingDeque$Itr\norg.apache.commons.pool2.impl.LinkedBlockingDeque$Node\norg.apache.commons.pool2.impl.LinkedBlockingDeque\norg.apache.commons.pool2.impl.NoOpCallStack\norg.apache.commons.pool2.impl.PoolImplUtils$1\norg.apache.commons.pool2.impl.PoolImplUtils\norg.apache.commons.pool2.impl.PooledSoftReference\norg.apache.commons.pool2.impl.SecurityManagerCallStack$1\norg.apache.commons.pool2.impl.SecurityManagerCallStack$PrivateSecurityManager\norg.apache.commons.pool2.impl.SecurityManagerCallStack$Snapshot\norg.apache.commons.pool2.impl.SecurityManagerCallStack\norg.apache.commons.pool2.impl.SoftReferenceObjectPool\norg.apache.commons.pool2.impl.ThrowableCallStack$1\norg.apache.commons.pool2.impl.ThrowableCallStack$Snapshot\norg.apache.commons.pool2.impl.ThrowableCallStack\norg.apache.commons.pool2.proxy.BaseProxyHandler\norg.apache.commons.pool2.proxy.CglibProxyHandler\norg.apache.commons.pool2.proxy.CglibProxySource\norg.apache.commons.pool2.proxy.JdkProxyHandler\norg.apache.commons.pool2.proxy.JdkProxySource\norg.apache.commons.pool2.proxy.ProxiedKeyedObjectPool\norg.apache.commons.pool2.proxy.ProxiedObjectPool\norg.apache.commons.pool2.proxy.ProxySource"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 0.8,
              "methods": [
                {
                  "technique": "binary-analysis",
                  "confidence": 0.8,
                  "value": "/var/folders/ld/bx6fm65j2qdgtyp4xkvbkh9c0000gp/T/mvn-deps-3mgsEe/org/apache/commons/commons-pool2/2.11.1/commons-pool2-2.11.1.jar"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/com.google.code.gson/gson@2.8.9?type=jar",
          "type": "library",
          "group": "com.google.code.gson",
          "name": "gson",
          "version": "2.8.9",
          "description": "Gson JSON library",
          "scope": "required",
          "hashes": [
            {
              "alg": "MD5",
              "content": "e67627f67e03301092dc7de0a2d7cef8"
            },
            {
              "alg": "SHA-1",
              "content": "8a432c1d6825781e21a02db2e2c33c5fde2833b9"
            },
            {
              "alg": "SHA-256",
              "content": "d3999291855de495c94c743761b8ab5176cfeabe281a5ab0d8e8d45326fd703e"
            },
            {
              "alg": "SHA-512",
              "content": "46501e4dd34c9a6f33ff63aeeec45b049579365c5273490e5dfd5ea4effaeced907d0fc728204c619aa136e867ad826204582ff9ba3080d06693c1c675c8473f"
            },
            {
              "alg": "SHA-384",
              "content": "2f2897912784595e52d3f8e57741aed7dd866f16a69562d57e0604d85e2fef08b2a32e58afd00d264f66cc6ec775dc79"
            },
            {
              "alg": "SHA3-384",
              "content": "3ce084f79191afdbdb0a9aa83073b128f620cf585b65c2e81ba98080fd91e9f327db3f0952903094b7dd387bc802b5ba"
            },
            {
              "alg": "SHA3-256",
              "content": "e82ae9fa3a783ee683880d219ab529bb3d0b45ea721d002ee948fad99a67b4f0"
            },
            {
              "alg": "SHA3-512",
              "content": "25cfe43039c6d41344434f89e9a8ad6f93a341512baf93e894a14a9dfd3af1cb0f0afaed4ade6db3c719f910fd9dfbeb7bec8bcfd7f49ac572ab217bce9e595e"
            }
          ],
          "licenses": [
            {
              "license": {
                "id": "Apache-2.0",
                "url": "https://www.apache.org/licenses/LICENSE-2.0"
              }
            }
          ],
          "purl": "pkg:maven/com.google.code.gson/gson@2.8.9?type=jar",
          "externalReferences": [
            {
              "url": "https://github.com/google/gson/gson",
              "type": "website"
            },
            {
              "url": "https://oss.sonatype.org/service/local/staging/deploy/maven2/",
              "type": "distribution-intake"
            },
            {
              "url": "https://github.com/google/gson/issues",
              "type": "issue-tracker"
            },
            {
              "url": "https://github.com/google/gson/gson/",
              "type": "vcs"
            }
          ],
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/java/docker-java-sample/pom.xml"
            },
            {
              "name": "Namespaces",
              "value": "com.google.gson.FieldNamingPolicy$5\ncom.google.gson.Gson$5\ncom.google.gson.JsonDeserializer\ncom.google.gson.JsonStreamParser\ncom.google.gson.Gson$FutureTypeAdapter\ncom.google.gson.Gson\ncom.google.gson.FieldNamingStrategy\ncom.google.gson.Gson$3\ncom.google.gson.JsonSerializer\ncom.google.gson.FieldNamingPolicy$3\ncom.google.gson.JsonNull\ncom.google.gson.InstanceCreator\ncom.google.gson.JsonSerializationContext\ncom.google.gson.FieldNamingPolicy$1\ncom.google.gson.JsonElement\ncom.google.gson.Gson$1\ncom.google.gson.FieldNamingPolicy$6\ncom.google.gson.TypeAdapter$1\ncom.google.gson.Gson$4\ncom.google.gson.stream.JsonReader$1\ncom.google.gson.stream.JsonReader\ncom.google.gson.stream.JsonToken\ncom.google.gson.stream.MalformedJsonException\ncom.google.gson.stream.JsonWriter\ncom.google.gson.stream.JsonScope\ncom.google.gson.FieldNamingPolicy$4\ncom.google.gson.JsonIOException\ncom.google.gson.reflect.TypeToken\ncom.google.gson.TypeAdapter\ncom.google.gson.JsonPrimitive\ncom.google.gson.internal.ConstructorConstructor$1\ncom.google.gson.internal.ConstructorConstructor$3\ncom.google.gson.internal.Streams$AppendableWriter$CurrentWrite\ncom.google.gson.internal.ConstructorConstructor$7\ncom.google.gson.internal.Excluder$1\ncom.google.gson.internal.ConstructorConstructor$5\ncom.google.gson.internal.$Gson$Types\ncom.google.gson.internal.ConstructorConstructor\ncom.google.gson.internal.ConstructorConstructor$2\ncom.google.gson.internal.LinkedTreeMap$KeySet\ncom.google.gson.internal.LinkedHashTreeMap$EntrySet$1\ncom.google.gson.internal.GsonBuildConfig\ncom.google.gson.internal.LinkedHashTreeMap$AvlIterator\ncom.google.gson.internal.LinkedTreeMap$1\ncom.google.gson.internal.LazilyParsedNumber\ncom.google.gson.internal.LinkedHashTreeMap\ncom.google.gson.internal.JsonReaderInternalAccess\ncom.google.gson.internal.reflect.PreJava9ReflectionAccessor\ncom.google.gson.internal.reflect.UnsafeReflectionAccessor\ncom.google.gson.internal.reflect.ReflectionAccessor\ncom.google.gson.internal.LinkedTreeMap$EntrySet\ncom.google.gson.internal.ConstructorConstructor$4\ncom.google.gson.internal.ObjectConstructor\ncom.google.gson.internal.LinkedTreeMap$LinkedTreeMapIterator\ncom.google.gson.internal.PreJava9DateFormatProvider\ncom.google.gson.internal.$Gson$Preconditions\ncom.google.gson.internal.LinkedHashTreeMap$KeySet\ncom.google.gson.internal.ConstructorConstructor$6\ncom.google.gson.internal.LinkedHashTreeMap$EntrySet\ncom.google.gson.internal.Streams\ncom.google.gson.internal.ConstructorConstructor$12\ncom.google.gson.internal.UnsafeAllocator\ncom.google.gson.internal.ConstructorConstructor$10\ncom.google.gson.internal.UnsafeAllocator$4\ncom.google.gson.internal.$Gson$Types$ParameterizedTypeImpl\ncom.google.gson.internal.ConstructorConstructor$8\ncom.google.gson.internal.LinkedHashTreeMap$Node\ncom.google.gson.internal.ConstructorConstructor$14\ncom.google.gson.internal.LinkedTreeMap\ncom.google.gson.internal.UnsafeAllocator$2\ncom.google.gson.internal.Primitives\ncom.google.gson.internal.LinkedTreeMap$KeySet$1\ncom.google.gson.internal.ConstructorConstructor$11\ncom.google.gson.internal.$Gson$Types$GenericArrayTypeImpl\ncom.google.gson.internal.LinkedHashTreeMap$1\ncom.google.gson.internal.ConstructorConstructor$9\ncom.google.gson.internal.LinkedHashTreeMap$AvlBuilder\ncom.google.gson.internal.$Gson$Types$WildcardTypeImpl\ncom.google.gson.internal.LinkedHashTreeMap$KeySet$1\ncom.google.gson.internal.ConstructorConstructor$13\ncom.google.gson.internal.LinkedHashTreeMap$LinkedTreeMapIterator\ncom.google.gson.internal.bind.DefaultDateTypeAdapter$1\ncom.google.gson.internal.bind.TreeTypeAdapter\ncom.google.gson.internal.bind.TypeAdapters$8\ncom.google.gson.internal.bind.ObjectTypeAdapter\ncom.google.gson.internal.bind.JsonAdapterAnnotationTypeAdapterFactory\ncom.google.gson.internal.bind.TypeAdapters$13\ncom.google.gson.internal.bind.TypeAdapters$11\ncom.google.gson.internal.bind.ObjectTypeAdapter$1\ncom.google.gson.internal.bind.ReflectiveTypeAdapterFactory$1\ncom.google.gson.internal.bind.JsonTreeReader\ncom.google.gson.internal.bind.TypeAdapters$31\ncom.google.gson.internal.bind.TypeAdapterRuntimeTypeWrapper\ncom.google.gson.internal.bind.NumberTypeAdapter$1\ncom.google.gson.internal.bind.DateTypeAdapter\ncom.google.gson.internal.bind.TypeAdapters$28\ncom.google.gson.internal.bind.TypeAdapters$15\ncom.google.gson.internal.bind.TypeAdapters$17\ncom.google.gson.internal.bind.NumberTypeAdapter\ncom.google.gson.internal.bind.util.ISO8601Utils\ncom.google.gson.internal.bind.TypeAdapters$EnumTypeAdapter\ncom.google.gson.internal.bind.ReflectiveTypeAdapterFactory$Adapter\ncom.google.gson.internal.bind.TypeAdapters$33\ncom.google.gson.internal.bind.TypeAdapters$10\ncom.google.gson.internal.bind.TreeTypeAdapter$GsonContextImpl\ncom.google.gson.internal.bind.TypeAdapters$34\ncom.google.gson.internal.bind.JsonTreeReader$1\ncom.google.gson.internal.bind.TypeAdapters$9\ncom.google.gson.internal.bind.TreeTypeAdapter$SingleTypeFactory\ncom.google.gson.internal.bind.ReflectiveTypeAdapterFactory$BoundField\ncom.google.gson.internal.bind.ObjectTypeAdapter$2\ncom.google.gson.internal.bind.TypeAdapters$12\ncom.google.gson.internal.bind.TypeAdapters$16\ncom.google.gson.internal.bind.DateTypeAdapter$1\ncom.google.gson.internal.bind.TypeAdapters$32\ncom.google.gson.internal.bind.NumberTypeAdapter$2\ncom.google.gson.internal.bind.TreeTypeAdapter$1\ncom.google.gson.internal.bind.TypeAdapters$30\ncom.google.gson.internal.bind.TypeAdapters$14\ncom.google.gson.internal.bind.TypeAdapters$29\ncom.google.gson.internal.bind.TypeAdapters$25\ncom.google.gson.internal.bind.ReflectiveTypeAdapterFactory\ncom.google.gson.internal.bind.TypeAdapters$18\ncom.google.gson.internal.bind.TypeAdapters$3\ncom.google.gson.internal.bind.TypeAdapters$1\ncom.google.gson.internal.bind.MapTypeAdapterFactory$Adapter\ncom.google.gson.internal.bind.DefaultDateTypeAdapter$DateType$1\ncom.google.gson.internal.bind.TypeAdapters$27\ncom.google.gson.internal.bind.TypeAdapters$33$1\ncom.google.gson.internal.bind.TypeAdapters$23\ncom.google.gson.internal.bind.TypeAdapters$5\ncom.google.gson.internal.bind.DefaultDateTypeAdapter\ncom.google.gson.internal.bind.ArrayTypeAdapter$1\ncom.google.gson.internal.bind.TypeAdapters$7\ncom.google.gson.internal.bind.CollectionTypeAdapterFactory\ncom.google.gson.internal.bind.TypeAdapters$21\ncom.google.gson.internal.bind.MapTypeAdapterFactory\ncom.google.gson.internal.bind.TypeAdapters$EnumTypeAdapter$1\ncom.google.gson.internal.bind.TypeAdapters\ncom.google.gson.internal.bind.TypeAdapters$26\ncom.google.gson.internal.bind.JsonTreeWriter\ncom.google.gson.internal.bind.TypeAdapters$19\ncom.google.gson.internal.bind.CollectionTypeAdapterFactory$Adapter\ncom.google.gson.internal.bind.TypeAdapters$24\ncom.google.gson.internal.bind.JsonTreeWriter$1\ncom.google.gson.internal.bind.TypeAdapters$2\ncom.google.gson.internal.bind.DefaultDateTypeAdapter$DateType\ncom.google.gson.internal.bind.TypeAdapters$6\ncom.google.gson.internal.bind.TypeAdapters$20\ncom.google.gson.internal.bind.TypeAdapters$22\ncom.google.gson.internal.bind.TypeAdapters$4\ncom.google.gson.internal.bind.ArrayTypeAdapter\ncom.google.gson.internal.UnsafeAllocator$3\ncom.google.gson.internal.LinkedTreeMap$EntrySet$1\ncom.google.gson.internal.Excluder\ncom.google.gson.internal.Streams$AppendableWriter\ncom.google.gson.internal.UnsafeAllocator$1\ncom.google.gson.internal.JavaVersion\ncom.google.gson.internal.LinkedTreeMap$Node\ncom.google.gson.internal.sql.SqlTypesSupport$1\ncom.google.gson.internal.sql.SqlTimestampTypeAdapter$1\ncom.google.gson.internal.sql.SqlTimestampTypeAdapter\ncom.google.gson.internal.sql.SqlDateTypeAdapter$1\ncom.google.gson.internal.sql.SqlTypesSupport$2\ncom.google.gson.internal.sql.SqlTimeTypeAdapter$1\ncom.google.gson.internal.sql.SqlTypesSupport\ncom.google.gson.internal.sql.SqlDateTypeAdapter\ncom.google.gson.internal.sql.SqlTimeTypeAdapter\ncom.google.gson.FieldNamingPolicy$2\ncom.google.gson.Gson$2\ncom.google.gson.ToNumberPolicy\ncom.google.gson.annotations.SerializedName\ncom.google.gson.annotations.Expose\ncom.google.gson.annotations.JsonAdapter\ncom.google.gson.annotations.Until\ncom.google.gson.annotations.Since\ncom.google.gson.TypeAdapterFactory\ncom.google.gson.ToNumberPolicy$4\ncom.google.gson.LongSerializationPolicy\ncom.google.gson.FieldNamingPolicy\ncom.google.gson.LongSerializationPolicy$1\ncom.google.gson.ToNumberPolicy$2\ncom.google.gson.JsonSyntaxException\ncom.google.gson.JsonArray\ncom.google.gson.ToNumberStrategy\ncom.google.gson.JsonParseException\ncom.google.gson.ToNumberPolicy$3\ncom.google.gson.LongSerializationPolicy$2\ncom.google.gson.JsonParser\ncom.google.gson.GsonBuilder\ncom.google.gson.FieldAttributes\ncom.google.gson.JsonDeserializationContext\ncom.google.gson.JsonObject\ncom.google.gson.ToNumberPolicy$1\ncom.google.gson.ExclusionStrategy"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 0.8,
              "methods": [
                {
                  "technique": "binary-analysis",
                  "confidence": 0.8,
                  "value": "/var/folders/ld/bx6fm65j2qdgtyp4xkvbkh9c0000gp/T/mvn-deps-3mgsEe/com/google/code/gson/gson/2.8.9/gson-2.8.9.jar"
                }
              ]
            }
          }
        }
      ]
    }
  ],
  "dependencies": [
    {
      "ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/org.examples.java/helloworld@1.0-SNAPSHOT?type=jar",
      "dependsOn": [
        "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/junit/junit@4.12?type=jar",
        "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/redis.clients/jedis@4.3.1?type=jar"
      ]
    },
    {
      "ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/junit/junit@4.12?type=jar",
      "dependsOn": [
        "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/org.hamcrest/hamcrest-core@1.3?type=jar"
      ]
    },
    {
      "ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/org.hamcrest/hamcrest-core@1.3?type=jar",
      "dependsOn": []
    },
    {
      "ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/redis.clients/jedis@4.3.1?type=jar",
      "dependsOn": [
        "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/com.google.code.gson/gson@2.8.9?type=jar",
        "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/org.apache.commons/commons-pool2@2.11.1?type=jar",
        "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/org.slf4j/slf4j-api@1.7.36?type=jar"
      ]
    },
    {
      "ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/org.slf4j/slf4j-api@1.7.36?type=jar",
      "dependsOn": []
    },
    {
      "ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/org.apache.commons/commons-pool2@2.11.1?type=jar",
      "dependsOn": []
    },
    {
      "ref": "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/com.google.code.gson/gson@2.8.9?type=jar",
      "dependsOn": []
    },
    {
      "ref": "publiccms@0.0.0-dev",
      "dependsOn": [
        "org.examples.java.helloworld@1.0-SNAPSHOT:pkg:maven/org.examples.java/helloworld@1.0-SNAPSHOT?type=jar"
      ]
    }
  ]
}

```

We obtained decent results without any manual work. Notably, unlike **syft**, the results include the component metadata, version, and name for the project, parsed from the jar file that **cdxgen** builds behind the scenes. It also successfully picks up all dependencies, including transitive ones.

Moreover, the dependency graph is accurate and the SBOM includes additional components information such as evidence and licenses.

**Trivy**

```tsx
manifest-cli sbom --name=publiccms --version=0.0.0-dev --generator=trivy -vvv -f test-trivy.json .
```

Just like other generators, **Trivy** multiple catalogers are [supported](https://aquasecurity.github.io/trivy/v0.52/docs/coverage/language/java/). Its worth mentioning that online access is required for some of the features, but mostly for JARs and other archives and `pom.xml` parsing of transitive dependencies.

```tsx
{
  "$schema": "http://cyclonedx.org/schema/bom-1.5.schema.json",
  "bomFormat": "CycloneDX",
  "specVersion": "1.5",
  "version": 1,
  "metadata": {
    "component": {
      "bom-ref": "publiccms@0.0.0-dev",
      "type": "application",
      "name": "publiccms",
      "version": "0.0.0-dev"
    }
  },
  "components": [
    {
      "bom-ref": ".@:f381188a-adbc-43d8-9c5b-bb6d5a91005f",
      "type": "application",
      "name": ".",
      "properties": [
        {
          "name": "aquasecurity:trivy:SchemaVersion",
          "value": "2"
        }
      ],
      "components": [
        {
          "bom-ref": ".@:42303f4a-0397-47d9-b71d-5d0f8166cfc2",
          "type": "application",
          "name": "pom.xml",
          "properties": [
            {
              "name": "aquasecurity:trivy:Class",
              "value": "lang-pkgs"
            },
            {
              "name": "aquasecurity:trivy:Type",
              "value": "pom"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/com.google.code.gson/gson@2.8.9",
          "type": "library",
          "name": "com.google.code.gson:gson",
          "version": "2.8.9",
          "licenses": [
            {
              "license": {
                "name": "Apache-2.0"
              }
            }
          ],
          "purl": "pkg:maven/com.google.code.gson/gson@2.8.9",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "com.google.code.gson:gson:2.8.9"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "pom"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/org.apache.commons/commons-pool2@2.11.1",
          "type": "library",
          "name": "org.apache.commons:commons-pool2",
          "version": "2.11.1",
          "licenses": [
            {
              "license": {
                "name": "Apache License, Version 2.0"
              }
            }
          ],
          "purl": "pkg:maven/org.apache.commons/commons-pool2@2.11.1",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "org.apache.commons:commons-pool2:2.11.1"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "pom"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/org.examples.java/helloworld@1.0-SNAPSHOT",
          "type": "library",
          "name": "org.examples.java:helloworld",
          "version": "1.0-SNAPSHOT",
          "purl": "pkg:maven/org.examples.java/helloworld@1.0-SNAPSHOT",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "org.examples.java:helloworld:1.0-SNAPSHOT"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "pom"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/org.slf4j/slf4j-api@1.7.36",
          "type": "library",
          "name": "org.slf4j:slf4j-api",
          "version": "1.7.36",
          "licenses": [
            {
              "license": {
                "name": "MIT License"
              }
            }
          ],
          "purl": "pkg:maven/org.slf4j/slf4j-api@1.7.36",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "org.slf4j:slf4j-api:1.7.36"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "pom"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/redis.clients/jedis@4.3.1",
          "type": "library",
          "name": "redis.clients:jedis",
          "version": "4.3.1",
          "licenses": [
            {
              "license": {
                "name": "MIT"
              }
            }
          ],
          "purl": "pkg:maven/redis.clients/jedis@4.3.1",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "redis.clients:jedis:4.3.1"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "pom"
            }
          ]
        }
      ]
    }
  ],
  "dependencies": [
    {
      "ref": ".@:42303f4a-0397-47d9-b71d-5d0f8166cfc2",
      "dependsOn": [
        ".@:pkg:maven/org.examples.java/helloworld@1.0-SNAPSHOT",
        ".@:pkg:maven/redis.clients/jedis@4.3.1"
      ]
    },
    {
      "ref": ".@:f381188a-adbc-43d8-9c5b-bb6d5a91005f",
      "dependsOn": [
        ".@:42303f4a-0397-47d9-b71d-5d0f8166cfc2"
      ]
    },
    {
      "ref": ".@:pkg:maven/com.google.code.gson/gson@2.8.9",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:maven/org.apache.commons/commons-pool2@2.11.1",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:maven/org.examples.java/helloworld@1.0-SNAPSHOT",
      "dependsOn": [
        ".@:pkg:maven/redis.clients/jedis@4.3.1"
      ]
    },
    {
      "ref": ".@:pkg:maven/org.slf4j/slf4j-api@1.7.36",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:maven/redis.clients/jedis@4.3.1",
      "dependsOn": [
        ".@:pkg:maven/com.google.code.gson/gson@2.8.9",
        ".@:pkg:maven/org.apache.commons/commons-pool2@2.11.1",
        ".@:pkg:maven/org.slf4j/slf4j-api@1.7.36"
      ]
    },
    {
      "ref": "publiccms@0.0.0-dev",
      "dependsOn": [
        ".@:f381188a-adbc-43d8-9c5b-bb6d5a91005f"
      ]
    }
  ]
}

```

As promised, accurate dependency tree, license data and all direct and indirect components found.

Lets compare it with offline-only results a `gradle.lock` could help us achieve:

```tsx
./gradlew dependencies --write-locks
```

Run generation:

```tsx
manifest-cli sbom --name=publiccms --version=0.0.0-dev --generator=trivy -vvv -f test-trivy.json .
```

Would output:

```tsx
{
  "$schema": "http://cyclonedx.org/schema/bom-1.5.schema.json",
  "bomFormat": "CycloneDX",
  "specVersion": "1.5",
  "version": 1,
  "metadata": {
    "component": {
      "bom-ref": "publiccms@0.0.0-dev",
      "type": "application",
      "name": "publiccms",
      "version": "0.0.0-dev"
    }
  },
  "components": [
    {
      "bom-ref": ".@:1e25fdf1-338b-4217-89a1-dfc2a7fa4f50",
      "type": "application",
      "name": ".",
      "properties": [
        {
          "name": "aquasecurity:trivy:SchemaVersion",
          "value": "2"
        }
      ],
      "components": [
        {
          "bom-ref": ".@:577cf3b3-6e60-4281-8d8c-b06c5d96ea00",
          "type": "application",
          "name": "pom.xml",
          "properties": [
            {
              "name": "aquasecurity:trivy:Class",
              "value": "lang-pkgs"
            },
            {
              "name": "aquasecurity:trivy:Type",
              "value": "pom"
            }
          ]
        },
        {
          "bom-ref": ".@:76182f14-1072-4b4c-a57c-f46ea3e8b250",
          "type": "application",
          "name": "gradle.lockfile",
          "properties": [
            {
              "name": "aquasecurity:trivy:Class",
              "value": "lang-pkgs"
            },
            {
              "name": "aquasecurity:trivy:Type",
              "value": "gradle"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/com.google.code.gson/gson@2.8.9",
          "type": "library",
          "name": "com.google.code.gson:gson",
          "version": "2.8.9",
          "purl": "pkg:maven/com.google.code.gson/gson@2.8.9",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "gradle"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/junit/junit@4.12",
          "type": "library",
          "name": "junit:junit",
          "version": "4.12",
          "purl": "pkg:maven/junit/junit@4.12",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "gradle"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/org.apache.commons/commons-pool2@2.11.1",
          "type": "library",
          "name": "org.apache.commons:commons-pool2",
          "version": "2.11.1",
          "purl": "pkg:maven/org.apache.commons/commons-pool2@2.11.1",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "gradle"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/org.examples.java/helloworld@1.0-SNAPSHOT",
          "type": "library",
          "name": "org.examples.java:helloworld",
          "version": "1.0-SNAPSHOT",
          "purl": "pkg:maven/org.examples.java/helloworld@1.0-SNAPSHOT",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "org.examples.java:helloworld:1.0-SNAPSHOT"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "pom"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/org.hamcrest/hamcrest-core@1.3",
          "type": "library",
          "name": "org.hamcrest:hamcrest-core",
          "version": "1.3",
          "purl": "pkg:maven/org.hamcrest/hamcrest-core@1.3",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "gradle"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/org.json/json@20220320",
          "type": "library",
          "name": "org.json:json",
          "version": "20220320",
          "purl": "pkg:maven/org.json/json@20220320",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "gradle"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/org.slf4j/slf4j-api@1.7.36",
          "type": "library",
          "name": "org.slf4j:slf4j-api",
          "version": "1.7.36",
          "purl": "pkg:maven/org.slf4j/slf4j-api@1.7.36",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "gradle"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:maven/redis.clients/jedis@4.3.1",
          "type": "library",
          "name": "redis.clients:jedis",
          "version": "4.3.1",
          "purl": "pkg:maven/redis.clients/jedis@4.3.1",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "gradle"
            }
          ]
        }
      ]
    }
  ],
  "dependencies": [
    {
      "ref": ".@:1e25fdf1-338b-4217-89a1-dfc2a7fa4f50",
      "dependsOn": [
        ".@:577cf3b3-6e60-4281-8d8c-b06c5d96ea00",
        ".@:76182f14-1072-4b4c-a57c-f46ea3e8b250"
      ]
    },
    {
      "ref": ".@:577cf3b3-6e60-4281-8d8c-b06c5d96ea00",
      "dependsOn": [
        ".@:pkg:maven/org.examples.java/helloworld@1.0-SNAPSHOT",
        ".@:pkg:maven/redis.clients/jedis@4.3.1"
      ]
    },
    {
      "ref": ".@:76182f14-1072-4b4c-a57c-f46ea3e8b250",
      "dependsOn": [
        ".@:pkg:maven/com.google.code.gson/gson@2.8.9",
        ".@:pkg:maven/junit/junit@4.12",
        ".@:pkg:maven/org.apache.commons/commons-pool2@2.11.1",
        ".@:pkg:maven/org.hamcrest/hamcrest-core@1.3",
        ".@:pkg:maven/org.json/json@20220320",
        ".@:pkg:maven/org.slf4j/slf4j-api@1.7.36",
        ".@:pkg:maven/redis.clients/jedis@4.3.1"
      ]
    },
    {
      "ref": ".@:pkg:maven/com.google.code.gson/gson@2.8.9",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:maven/junit/junit@4.12",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:maven/org.apache.commons/commons-pool2@2.11.1",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:maven/org.examples.java/helloworld@1.0-SNAPSHOT",
      "dependsOn": [
        ".@:pkg:maven/redis.clients/jedis@4.3.1"
      ]
    },
    {
      "ref": ".@:pkg:maven/org.hamcrest/hamcrest-core@1.3",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:maven/org.json/json@20220320",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:maven/org.slf4j/slf4j-api@1.7.36",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:maven/redis.clients/jedis@4.3.1",
      "dependsOn": []
    },
    {
      "ref": "publiccms@0.0.0-dev",
      "dependsOn": [
        ".@:1e25fdf1-338b-4217-89a1-dfc2a7fa4f50"
      ]
    }
  ]
}

```

Unfortunately, although it found all used dependencies, it was unable to properly build an accurate dependency tree and did not include license data.

**Trivy** supports JAR and other archive-based files. Read more about it [here](https://aquasecurity.github.io/trivy/v0.52/docs/coverage/language/java/) if this is the path you need to take.

**spdx-sbom-generator**

A less known generator, which is capable of generating SPDX 2.3 SBOMs is also supported by the Manifest CLI.

Run:

```tsx
manifest-cli sbom --name=publiccms --version=0.0.0-dev --generator=spdx-sbom-generator -o=spdx-json -vvv -f test-ssg.json .
```

It’s worth mentioning the this generator is not as popular as others and not very well maintained, we had to dig through sources to find that it supports `build.gradle` , `settings.gradle` or `pom.xml`

```tsx
{
    "spdxVersion": "SPDX-2.3",
    "dataLicense": "CC0-1.0",
    "SPDXID": "SPDXRef-DOCUMENT",
    "name": "publiccms",
    "documentNamespace": "https://spdx.org/spdxdocs/publiccms-{6093f553a50e74739a1963027d89656483393c80 []}",
    "creationInfo": {
        "creators": [
            "Tool: github.com/spdx/tools-golang/builder",
            "Tool: manifest-cli/0.14.8"
        ],
        "created": "2024-06-16T11:36:39Z"
    },
    "packages": [
        {
            "name": "publiccms",
            "SPDXID": "SPDXRef-Package-publiccms",
            "versionInfo": "0.0.0-dev",
            "downloadLocation": "NOASSERTION",
            "filesAnalyzed": true,
            "packageVerificationCode": {
                "packageVerificationCodeValue": "6093f553a50e74739a1963027d89656483393c80"
            },
            "licenseConcluded": "NOASSERTION",
            "licenseDeclared": "NOASSERTION",
            "copyrightText": "NOASSERTION"
        },
        {
            "name": "helloworld",
            "SPDXID": "SPDXRef-Package-helloworld",
            "versionInfo": "1.0-SNAPSHOT",
            "supplier": "Organization: helloworld",
            "downloadLocation": "http://maven.apache.org",
            "filesAnalyzed": false,
            "packageVerificationCode": {
                "packageVerificationCodeValue": ""
            },
            "checksums": [
                {
                    "algorithm": "SHA1",
                    "checksumValue": "6adfb183a4a2c94a2f92dab5ade762a47889a5a1"
                }
            ],
            "homepage": "http://maven.apache.org",
            "licenseConcluded": "NOASSERTION",
            "licenseDeclared": "NOASSERTION",
            "licenseComments": "NOASSERTION",
            "copyrightText": "NOASSERTION",
            "comment": "NOASSERTION"
        },
        {
            "name": "junit",
            "SPDXID": "SPDXRef-Package-junit-4.12",
            "versionInfo": "4.12",
            "supplier": "Organization: junit",
            "downloadLocation": "https://mvnrepository.com/artifact/junit/junit/4.12",
            "filesAnalyzed": false,
            "packageVerificationCode": {
                "packageVerificationCodeValue": ""
            },
            "checksums": [
                {
                    "algorithm": "SHA1",
                    "checksumValue": "fdda4a4a842bd2bb90c6bd3c8076c777264fc204"
                }
            ],
            "homepage": "NOASSERTION",
            "licenseConcluded": "NOASSERTION",
            "licenseDeclared": "NOASSERTION",
            "licenseComments": "NOASSERTION",
            "copyrightText": "NOASSERTION",
            "comment": "NOASSERTION"
        },
        {
            "name": "jedis",
            "SPDXID": "SPDXRef-Package-jedis-4.3.1",
            "versionInfo": "4.3.1",
            "supplier": "Organization: jedis",
            "downloadLocation": "https://mvnrepository.com/artifact/redis.clients/jedis/4.3.1",
            "filesAnalyzed": false,
            "packageVerificationCode": {
                "packageVerificationCodeValue": ""
            },
            "checksums": [
                {
                    "algorithm": "SHA1",
                    "checksumValue": "8b93ae7eb0b0d737e5c24a7d206f4e88f4382015"
                }
            ],
            "homepage": "NOASSERTION",
            "licenseConcluded": "NOASSERTION",
            "licenseDeclared": "NOASSERTION",
            "licenseComments": "NOASSERTION",
            "copyrightText": "NOASSERTION",
            "comment": "NOASSERTION"
        },
        {
            "name": "gson",
            "SPDXID": "SPDXRef-Package-gson-2.8.9",
            "versionInfo": "2.8.9",
            "supplier": "Organization: gson",
            "downloadLocation": "https://mvnrepository.com/artifact/com.google.code.gson/gson/2.8.9",
            "filesAnalyzed": false,
            "packageVerificationCode": {
                "packageVerificationCodeValue": ""
            },
            "checksums": [
                {
                    "algorithm": "SHA1",
                    "checksumValue": "b432828b0db9b6566355a3319da3ff27399a9363"
                }
            ],
            "homepage": "NOASSERTION",
            "licenseConcluded": "NOASSERTION",
            "licenseDeclared": "NOASSERTION",
            "licenseComments": "NOASSERTION",
            "copyrightText": "NOASSERTION",
            "comment": "NOASSERTION"
        },
        {
            "name": "commons-pool2",
            "SPDXID": "SPDXRef-Package-commons-pool2-2.11.1",
            "versionInfo": "2.11.1",
            "supplier": "Organization: commons-pool2",
            "downloadLocation": "https://mvnrepository.com/artifact/org.apache.commons/commons-pool2/2.11.1",
            "filesAnalyzed": false,
            "packageVerificationCode": {
                "packageVerificationCodeValue": ""
            },
            "checksums": [
                {
                    "algorithm": "SHA1",
                    "checksumValue": "16b9e84cb6de025a592684a5ac6cf15e8d2f429f"
                }
            ],
            "homepage": "NOASSERTION",
            "licenseConcluded": "NOASSERTION",
            "licenseDeclared": "NOASSERTION",
            "licenseComments": "NOASSERTION",
            "copyrightText": "NOASSERTION",
            "comment": "NOASSERTION"
        },
        {
            "name": "hamcrest-core",
            "SPDXID": "SPDXRef-Package-hamcrest-core-1.3",
            "versionInfo": "1.3",
            "supplier": "Organization: hamcrest-core",
            "downloadLocation": "https://mvnrepository.com/artifact/org.hamcrest/hamcrest-core/1.3",
            "filesAnalyzed": false,
            "packageVerificationCode": {
                "packageVerificationCodeValue": ""
            },
            "checksums": [
                {
                    "algorithm": "SHA1",
                    "checksumValue": "740952b7992158338becf5fef9e2246da2d7927c"
                }
            ],
            "homepage": "NOASSERTION",
            "licenseConcluded": "NOASSERTION",
            "licenseDeclared": "NOASSERTION",
            "licenseComments": "NOASSERTION",
            "copyrightText": "NOASSERTION",
            "comment": "NOASSERTION"
        },
        {
            "name": "slf4j-api",
            "SPDXID": "SPDXRef-Package-slf4j-api-1.7.36",
            "versionInfo": "1.7.36",
            "supplier": "Organization: slf4j-api",
            "downloadLocation": "https://mvnrepository.com/artifact/org.slf4j/slf4j-api/1.7.36",
            "filesAnalyzed": false,
            "packageVerificationCode": {
                "packageVerificationCodeValue": ""
            },
            "checksums": [
                {
                    "algorithm": "SHA1",
                    "checksumValue": "1f5d1163f93cc80861f59ac7e0ca1136f79765e8"
                }
            ],
            "homepage": "NOASSERTION",
            "licenseConcluded": "NOASSERTION",
            "licenseDeclared": "NOASSERTION",
            "licenseComments": "NOASSERTION",
            "copyrightText": "NOASSERTION",
            "comment": "NOASSERTION"
        }
    ],
    "relationships": [
        {
            "spdxElementId": "SPDXRef-DOCUMENT",
            "relatedSpdxElement": "SPDXRef-Package-publiccms",
            "relationshipType": "DESCRIBES"
        },
        {
            "spdxElementId": "SPDXRef-Package-publiccms",
            "relatedSpdxElement": "SPDXRef-Package-helloworld",
            "relationshipType": "DEPENDS_ON"
        },
        {
            "spdxElementId": "SPDXRef-Package-helloworld",
            "relatedSpdxElement": "SPDXRef-Package-junit-4.12",
            "relationshipType": "DEPENDS_ON"
        },
        {
            "spdxElementId": "SPDXRef-Package-helloworld",
            "relatedSpdxElement": "SPDXRef-Package-jedis-4.3.1",
            "relationshipType": "DEPENDS_ON"
        },
        {
            "spdxElementId": "SPDXRef-Package-helloworld",
            "relatedSpdxElement": "SPDXRef-Package-gson-2.8.9",
            "relationshipType": "DEPENDS_ON"
        },
        {
            "spdxElementId": "SPDXRef-Package-helloworld",
            "relatedSpdxElement": "SPDXRef-Package-commons-pool2-2.11.1",
            "relationshipType": "DEPENDS_ON"
        },
        {
            "spdxElementId": "SPDXRef-Package-helloworld",
            "relatedSpdxElement": "SPDXRef-Package-hamcrest-core-1.3",
            "relationshipType": "DEPENDS_ON"
        },
        {
            "spdxElementId": "SPDXRef-Package-helloworld",
            "relatedSpdxElement": "SPDXRef-Package-slf4j-api-1.7.36",
            "relationshipType": "DEPENDS_ON"
        },
        {
            "spdxElementId": "SPDXRef-Package-junit-4.12",
            "relatedSpdxElement": "SPDXRef-Package-hamcrest-core-1.3",
            "relationshipType": "DEPENDS_ON"
        },
        {
            "spdxElementId": "SPDXRef-Package-jedis-4.3.1",
            "relatedSpdxElement": "SPDXRef-Package-slf4j-api-1.7.36",
            "relationshipType": "DEPENDS_ON"
        },
        {
            "spdxElementId": "SPDXRef-Package-jedis-4.3.1",
            "relatedSpdxElement": "SPDXRef-Package-commons-pool2-2.11.1",
            "relationshipType": "DEPENDS_ON"
        },
        {
            "spdxElementId": "SPDXRef-Package-jedis-4.3.1",
            "relatedSpdxElement": "SPDXRef-Package-gson-2.8.9",
            "relationshipType": "DEPENDS_ON"
        }
    ]
}

```

As expected, results are lacking important information and components from the final SBOM.

## Conclusion

In regards to SBOM generation, the Java community using Maven is fairly covered by open source generators that can generate quality outputs. We would recommend **Trivy** for most scenarios, while preferring native `pom.xml` cataloger. The runner up and most easy to use would be **cdxgen** pas it provides the most extensive format coverage, they both generate a quality output, however, if you need SPDX, stick with Trivy.

Syft and offline-only Trivy supporting `gradle.lock` files would be your best bet if you do not require license data, yet again, Trivy provides an accurate dependency tree, where Syft doesn’t.

Unfortunatly, its safe to say, that as for today, the **spdx-sbom-generator** should not be used as it provides poor results compared to others.
