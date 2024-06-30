FROM gradle:7 AS base
CMD ["bash"]

# Build
# /workspace にコピー
# /workspace に移動
# /workspace でgradlewコマンドを実行
# /workspace 配下に /build ディレクトリが作成される
FROM base AS test-and-build
COPY . /workspace
WORKDIR /workspace
RUN ./gradlew build

# Deploy
# buildで作成した api-0.0.1-SNAPSHOT.jar ファイルを /api.jar にコピーする
FROM openjdk:17 AS production
COPY --from=test-and-build /workspace/build/libs/api-0.0.1-SNAPSHOT.jar ./api.jar
CMD ["java", "-jar", "api.jar"]

