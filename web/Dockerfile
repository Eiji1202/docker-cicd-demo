FROM node:18 AS base
CMD [ "bash" ]

# Build
# /workspace にコピー
# /workspace に移動
# /workspace でnpmコマンドを実行
# /workspace 配下に /build ディレクトリが作成される
FROM base AS test-and-build
COPY . /workspace
WORKDIR /workspace
ARG REACT_APP_API_SERVER
RUN npm ci && npm  run test && npm run build

# Deploy
# buildで作成したファイルを /var/www にコピーする
# nginx.confをコピーしてnginxの設定を行う
FROM nginx:latest AS production
COPY --from=test-and-build /workspace/build /var/www
COPY nginx.conf /etc/nginx/conf.d/default.conf
