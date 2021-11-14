## Dart dev notes

[Full stack demo with Dart, Flutter, and Cloud Run](https://www.youtube.com/watch?v=v3rOI9lkftw)

From there take the idea for a Dockerfile like this

```Dockerfile
################
FROM google/dart:2.12

WORKDIR /app
COPY pubspec.yaml /app/pubspec.yaml
RUN dart pub get
COPY . .
RUN dart pub get --offline

RUN dart pub run build_runner build --delete-conflicting-outputs
RUN dart compile exe bin/server.dart -o bin/server

########################
FROM subfuzion/dart:slim
COPY --from=0 /app/bin/server /app/bin/server
EXPOSE 8080
ENTRYPOINT ["/app/bin/server"]
```
