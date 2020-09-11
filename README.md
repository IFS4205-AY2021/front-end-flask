## Frontend Docker Configration

## Production
For production, first build the project:
```
# Note the build process is integrited into docker image building process.
# i.e npm run build

# Deploy using docker:
docker build . -t frontend
docker run -d -p 80:80 frontend
```

## Development
### Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
