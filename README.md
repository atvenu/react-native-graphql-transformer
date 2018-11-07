# react-native-graphql-transformer

[![All Contributors](https://img.shields.io/badge/all_contributors-4-orange.svg?style=flat-square)](#contributors)

Seamlessly use GraphQL files with react-native >= 0.45

## Foreword

This package is inspired by the
[react-native-typescript-transform](https://github.com/ds300/react-native-typescript-transformer)
repository.

## Goal

Use `.gql`or `.graphql` files with React Native packager for better readability
and separation of concerns.

**Exemple of a `.gql` file with import statement:**

```gql
#import "fragments/BasePost.gql"

query PostListItemQuery($id: ID) {
  Post(id: $id) {
    ...BasePost
  }
}
```

## Usage

### Step 1: Install

    yarn add -D react-native-graphql-transformer

### Step 2: Configure the react native packager

Add this to your rn-cli.config.js (make one if you don't have one already):

#### react-native 0.57 or later

```js
const { getDefaultConfig } = require('metro-config');

module.exports = (async () => {
  const {
    resolver: { sourceExts },
  } = await getDefaultConfig();
  return {
    transformer: {
      babelTransformerPath: require.resolve('react-native-graphql-transformer'),
    },
    resolver: {
      sourceExts: [...sourceExts, 'gql', 'graphql'],
    },
  };
})();
```

#### react-native 0.56 or earlier

```js
module.exports = {
  getTransformModulePath() {
    return require.resolve('react-native-graphql-transformer');
  },
  getSourceExts() {
    return ['gql', 'graphql'];
  }
};
```

If you need to run the packager directly from the command line, run the
following

    react-native start --transformer node_modules/react-native-graphql-transformer/index.js --sourceExts gql,graphql

### Step 3: Write GraphQL code!

## Contributors

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
| [<img src="https://avatars1.githubusercontent.com/u/16262904?v=4" width="100px;"/><br /><sub><b>Thomas Pucci</b></sub>](https://github.com/tpucci)<br />[💻](https://github.com/bamlab/react-native-graphql-transformer/commits?author=tpucci "Code") [📖](https://github.com/bamlab/react-native-graphql-transformer/commits?author=tpucci "Documentation") [💡](#example-tpucci "Examples") | [<img src="https://avatars2.githubusercontent.com/u/13785185?v=4" width="100px;"/><br /><sub><b>TychoTa</b></sub>](https://twitter.com/TychoTa)<br />[💻](https://github.com/bamlab/react-native-graphql-transformer/commits?author=tychota "Code") | [<img src="https://avatars2.githubusercontent.com/u/9041221?v=4" width="100px;"/><br /><sub><b>Clément Taboulot</b></sub>](https://github.com/taboulot)<br />[💻](https://github.com/bamlab/react-native-graphql-transformer/commits?author=taboulot "Code") | [<img src="https://avatars0.githubusercontent.com/u/5304092?v=4" width="100px;"/><br /><sub><b>arolson101</b></sub>](https://github.com/arolson101)<br />[💡](#example-arolson101 "Examples") |
| :---: | :---: | :---: | :---: |
<!-- ALL-CONTRIBUTORS-LIST:END -->

## License

MIT
