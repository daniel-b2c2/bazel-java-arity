# [minimal-reproduction-template](https://github.com/renovatebot/renovate/discussions/31313)

While `groupId:artifactId:version` is the most common way of defining co-ordinates for 99% of usecases, there are occasionally more complex co-ordinates that involve specifying the packaging and classifier. 

The full set of valid co-ordinate patterns can be seen here for bazel, the problem is that renovate only comprehends the 3-arity form, and [speculating] either doesn't support 4,5-arity, or there is a bug in 4,5-arity.

![image](https://github.com/user-attachments/assets/3bc9c52f-aef0-42c9-9dd8-371f53fd0dfa)

Spec:
https://github.com/bazelbuild/rules_jvm_external/blob/master/specs.bzl#L132

Using this particular maven artifact as a great example of 5-arity: https://repo1.maven.org/maven2/io/netty/netty-transport-native-epoll/4.1.113.Final/

It is necessary to specify the packaging as jar and the classifier linux-x86_64 as part of the co-ordinates so

`"io.netty:netty-transport-native-epoll:jar:linux-x86_64:4.1.87.Final` (5-arity) is valid in a `maven_install` file.


## Current behavior

when renovate raises a PR for a 5-arity entry, it incorrectly offers `io.netty:netty-transport-native-epoll:4.1.113.Final:linux-x86_64:4.1.87.Final` as the upgrade replacing the third element (`jar`) with the new version.

## Expected behavior

when renovate raises a PR for a 5-arity entry, it should offer `io.netty:netty-transport-native-epoll:jar:linux-x86_64:4.1.113.Final` with the last element in the array being upgraded.

## Link to the Renovate issue or Discussion

[Put your link to the Renovate issue or Discussion here.](https://github.com/renovatebot/renovate/discussions/31313)
