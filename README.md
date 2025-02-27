# Pet Finder

Все любят котиков!

Если ты можешь помочь, ты должен помочь!

Pet project with Flutter + Firebase + Hasura.

![alt text](assets/head.png)

## How to Start

```
$ flutter packages pub run build_runner build --delete-conflicting-outputs
$ cd data && docker-compose up -d
```

## For VSCode Apollo GraphQL (deprecated)

```
$ npm install -g apollo graphql
```

create `./apollo.config.js`

```js
module.exports = {
  client: {
    includes: ['./lib/**/*.dart'],
    service: {
      name: '<project name>',
      url: '<graphql endpoint>',
      // optional headers
      headers: {
        'x-hasura-admin-secret': '<secret>',
        'x-hasura-role': 'user',
      },
      // optional disable SSL validation check
      skipSSLValidation: true,
      // alternative way
      // localSchemaFile: './schema.graphql',
    },
  },
}
```

how to download `schema.json` for `localSchemaFile`

```
$ apollo schema:download --endpoint <graphql endpoint> --header 'X-Hasura-Admin-Secret: <secret>' --header 'X-Hasura-Role: user'
```

## For VSCode Apollo Rover

```
$ npm install -g @apollo/rover
$ rover graph introspect http://localhost:8080/v1/graphql > schema.graphql
```

## Оптимизация времени сборки Firebase iOS SDK

https://github.com/invertase/firestore-ios-sdk-frameworks

## How to save DB-Schema

```
$ cd data
$ rm -rf migrations
$ hasura migrate create "init" --from-server --database-name default
$ rm -rf metadata
$ hasura metadata export
```

## How to restore DB-Schema

```
$ cd data
$ hasura migrate apply
$ hasura metadata apply
```

or

```
$ cd data
$ cat backup.sql | docker exec -i data-postgres-1 psql -U postgres
$ hasura metadata apply
```

## How to backup data

curl --location --request POST 'http://localhost:8080/v1alpha1/pg_dump' --header 'x-hasura-admin-secret: <password>' --header 'Content-Type: application/json' --data-raw '{ "opts": ["-O", "-x", "--schema", "public", "--schema", "auth"], "clean_output": true}' -o backup.sql

## I need a home

![alt text](assets/i_need_a_home.png)

## How to reset build

```
flutter clean
flutter pub get
cd ios
rm -rf Pods
rm Podfile.lock
pod install --verbose
```

...then restart vscode
