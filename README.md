# kexi

kexi is a short-hand tool for some kubectl / oc commands and one to export all manifest files of an app deployed on Kubernetes / OpenShift based on a label selector. 

You can of course also build a native executable if you have current (GraalVM-ce installed)[https://quarkus.io/guides/building-native-image] by issuing the following command:

```bash
$ ./gradlew build -Dquarkus.native.enabled=true
```

## Executing
```bash
$ java -jar ./build/quarkus-app/quarkus-run.jar app [-n <namespace>] -s app=cat-server -o ./test.yaml
```

## Building
You have several options to use kexi. First of all you have to build it using maven with a Java 21 JDK. If you're downloading and using GraalVM-CE as Java 21 JDK, you're even able to build a native executable, which speeds things up.

### Building an uber-JAR
Best option if you want to just play a bit with kexi.

```bash
$ mvn clean package -Dquarkus.package.jar.type=uber-jar
$ java -jar ./target/kexi-0.0.1-runner.jar app -n <namespace> -s app=cat-server -o ./test.yaml
```

### Building and using a GraalVM-ce compiled native executable
Use this option if you want to use kexi in a much easier form.

```bash
$ mvn clean package -Dnative
$ ./target/kexi-0.0.1-runner app -n <namespace> -s app=cat-server -o ./test.yaml
```

## Using kexi
Right now, kexi can do the following:
- Exporting a list of pods
- Exporting the yaml of one pod
- Exporting a list of OpenShift routes
- Exporting the yaml of one route
- Exporting a list of Deployments
- Exporting the yaml of one Deployment
- Exporting all yaml of one app, which is identified by a selector label
- Deleting a list of projects 

By default, kexi is using the current kubeconfig located in ~/.kube/config to connect to the Kubernetes cluster. 
### Pods
```bash
$ kexi pods -n <namespace> [-r pod name]
```

### Routes
```bash
$ kexi routes -n <namespace> [-r route name]
```

### Deployments
```bash
$ kexi deployments -n <namespace> [-r deployment name]
```

### Services
```bash
$ kexi services -n <namespace> [-r service name]
```

### Delete project list
```bash
$ kexi delete [project1, project2, ...]
```

### App export
```bash
$ kexi app -n <namespace> -s app=cat-server [-o <output>]
```


