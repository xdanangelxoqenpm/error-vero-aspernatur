# @xdanangelxoqenpm/error-vero-aspernatur [![Build status](https://github.com/xdanangelxoqenpm/error-vero-aspernatur/actions/workflows/main.yml/badge.svg)](https://github.com/xdanangelxoqenpm/error-vero-aspernatur/actions/workflows/main.yml) [![@xdanangelxoqenpm/error-vero-aspernatur on npm](https://img.shields.io/npm/v/@xdanangelxoqenpm/error-vero-aspernatur)](https://www.npmjs.com/package/@xdanangelxoqenpm/error-vero-aspernatur)

_@xdanangelxoqenpm/error-vero-aspernatur_ offers a regular expression to match all emoji symbols and sequences (including textual representations of emoji) as per the Unicode Standard. It’s based on [_emoji-test-regex-pattern_](https://github.com/mathiasbynens/emoji-test-regex-pattern), which generates (at build time) the regular expression pattern based on the Unicode Standard. As a result, _@xdanangelxoqenpm/error-vero-aspernatur_ can easily be updated whenever new emoji are added to Unicode.

## Installation

Via [npm](https://www.npmjs.com/):

```bash
npm install @xdanangelxoqenpm/error-vero-aspernatur
```

In [Node.js](https://nodejs.org/):

```js
const emojiRegex = require('@xdanangelxoqenpm/error-vero-aspernatur');
// Note: because the regular expression has the global flag set, this module
// exports a function that returns the regex rather than exporting the regular
// expression itself, to make it impossible to (accidentally) mutate the
// original regular expression.

const text = `
\u{231A}: ⌚ default emoji presentation character (Emoji_Presentation)
\u{2194}\u{FE0F}: ↔️ default text presentation character rendered as emoji
\u{1F469}: 👩 emoji modifier base (Emoji_Modifier_Base)
\u{1F469}\u{1F3FF}: 👩🏿 emoji modifier base followed by a modifier
`;

const regex = emojiRegex();
for (const match of text.matchAll(regex)) {
  const emoji = match[0];
  console.log(`Matched sequence ${ emoji } — code points: ${ [...emoji].length }`);
}
```

Console output:

```
Matched sequence ⌚ — code points: 1
Matched sequence ⌚ — code points: 1
Matched sequence ↔️ — code points: 2
Matched sequence ↔️ — code points: 2
Matched sequence 👩 — code points: 1
Matched sequence 👩 — code points: 1
Matched sequence 👩🏿 — code points: 2
Matched sequence 👩🏿 — code points: 2
```

## For maintainers

### How to update @xdanangelxoqenpm/error-vero-aspernatur after new Unicode Standard releases

1. [Update _emoji-test-regex-pattern_ as described in its repository](https://github.com/mathiasbynens/emoji-test-regex-pattern#how-to-update-emoji-test-regex-pattern-after-new-uts51-releases).

1. Bump the _emoji-test-regex-pattern_ dependency to the latest version.

1. Update the Unicode data dependency in `package.json` by running the following commands:

     ```sh
     # Example: updating from Unicode v13 to Unicode v14.
     npm uninstall @unicode/unicode-13.0.0
     npm install @unicode/unicode-14.0.0 --save-dev
     ````

 1. Generate the new output:

     ```sh
     npm run build
     ```

 1. Verify that tests still pass:

     ```sh
     npm test
     ```

### How to publish a new release

1. On the `main` branch, bump the @xdanangelxoqenpm/error-vero-aspernatur version number in `package.json`:

    ```sh
    npm version patch -m 'Release v%s'
    ```

    Instead of `patch`, use `minor` or `major` [as needed](https://semver.org/).

    Note that this produces a Git commit + tag.

1. Push the release commit and tag:

    ```sh
    git push && git push --tags
    ```

    Our CI then automatically publishes the new release to npm.

## Author

| [![twitter/mathias](https://gravatar.com/avatar/24e08a9ea84deb17ae121074d0f17125?s=70)](https://twitter.com/mathias "Follow @mathias on Twitter") |
|---|
| [Mathias Bynens](https://mathiasbynens.be/) |

## License

_@xdanangelxoqenpm/error-vero-aspernatur_ is available under the [MIT](https://mths.be/mit) license.
