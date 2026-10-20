# XOD 2 plugin catalog

This public GitHub repository is the plugin catalog and package store used by XOD 2's plugin manager. Copy `registry.json` to the repository root and configure the IDE with this repository's `owner/name`.

## Add a plugin

1. Publish the plugin in its own public GitHub repository.
2. Include a valid root `xod-plugin.json` manifest and attach `xod-plugin.zip` to a GitHub Release. The archive must contain the manifest and the bundle named by its `entry` field.
3. In XOD 2, sign in with GitHub and submit the plugin repository. XOD validates the source and release, copies the bundle into this catalog repository, and opens a pull request for review.

The corresponding `registry.json` entry is:

```json
{
  "id": "publisher.plugin-name",
  "repository": "publisher/plugin-name",
  "version": "1.0.0",
  "bundlePath": "plugins/publisher.plugin-name/1.0.0/xod-plugin.zip"
}
```

The manager validates the plugin repository's manifest and matching version before showing it. Users can install plugins without signing in. Plugin installation requires user approval and plugins run in XOD's sandbox.

## Registry format

`registry.json` is public and has this shape:

```json
{
  "schemaVersion": 1,
  "plugins": []
}
```

Only add public repositories. The IDE downloads package bundles from this catalog repository. The source link and release remain in the plugin author's repository.

## GitHub authorization

The desktop app uses GitHub OAuth Device Flow. Register an OAuth App with Device Flow enabled and enter its client ID in the Plugins manager. Publishing requests `read:user` and `public_repo`, which GitHub uses to identify the publisher and create a fork and pull request. The access token stays in memory for the current app session.
