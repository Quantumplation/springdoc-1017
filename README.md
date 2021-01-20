# springdoc-1017
This repository contains a fairly minimal reproduce of Springdoc issue #1017.

```
pi ~/p/springdoc-1017 (main)> mvn -v
Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
Maven home: /usr/local/Cellar/maven/3.6.3_1/libexec
Java version: 1.8.0_265, vendor: Amazon.com Inc., runtime: /Library/Java/JavaVirtualMachines/amazon-corretto-8.jdk/Contents/Home/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "mac os x", version: "10.15.6", arch: "x86_64", family: "mac"
```

It's extracted from a much much larger project, but I tried to remove as many superflous
dependencies as I could; I'm pretty unfamiliar with Java pom files, though, so it's
possible this could be yet simpler.

When running `mvn verify`, the small Springboot service is started, and a request to
`/api-docs.yaml` is made, and the result is persisted to `sample/api.yaml`.  Notice that
the schema for the response for the one controller contains a property:

`exampleSetFlag: false`.

This property is not part of the OpenAPI spec, and inhibits the ability for the springdoc
output to be pipelined to other tools.  I have a temporary hacky solution which uses
`grep -v` to filter out this line, but that isn't very robust.
