FROM node as build
RUN curl -sfL https://install.goreleaser.com/github.com/tj/node-prune.sh | bash -s -- -b /usr/local/bin
WORKDIR /src
COPY . /src
RUN npm install 
# remove development dependencies
RUN npm prune --production
# run node prune
RUN /usr/local/bin/node-prune

FROM node:current-alpine
COPY --from=build /src/node_modules /dist/node_modules/
COPY index.js /dist/
WORKDIR /dist
CMD ["node", "index.js"]
EXPOSE 8080