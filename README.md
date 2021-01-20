# springdoc-1017
This repository contains a fairly minimal reproduce of Springdoc issue #1017.

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
