const NodePolyfillPlugin = require("node-polyfill-webpack-plugin");

module.exports = {
  plugins: [
    new NodePolyfillPlugin()
  ],
  resolve: {
    fallback: {
      "global": require.resolve("global"),
      "crypto": require.resolve("crypto-browserify"),
      "stream": require.resolve("stream-browserify")
    }
  }
};
