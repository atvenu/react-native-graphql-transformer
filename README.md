# react-native-graphql-transformer

Fork of [bamlab's original transformer](https://github.com/bamlab/react-native-graphql-transformer)

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

    npm i --save-dev react-native-graphql-transformer

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
  },
};
```

### Step 3: Write GraphQL code!

## License

MIT
