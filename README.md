# Parcel simple Node.js bundling demo

This is a minimal example that shows how to use Parcel to bundle all of your dependencies into a single file.

## Try it out!

```
npm i
npm run build
```

You should see a new file, `dist/index.js`, which contains the bundled code. 

## Using it in another project

### The `main` field
The `main` field in `package.json` refers to the entrypoint of your package. If you run `node .` in a folder with a `package.json`, Node will run the file listed in `main`. 

When building libraries aimed at other developers, it is often convenient to build and commit a "ready to go" or "distribution" copy of the code. For example, if you use Typescript to develop a Javascript library, you must either release built/compiled copy of your file, or require the end-user/developer to build it. The latter would involve a [`postinstall` script](https://docs.npmjs.com/cli/v6/using-npm/scripts#npm-install), in which case Typescript moves from  `devDependencies` to a `dependencies`. It's usually easier to go with the former solution and commit a "distribution" file. This usually lives in the "dist" folder, and this is what you should point the `main` field to if you use this solution. 

Parcel uses the `main` field as the target to build to, so in an existing project you should rename `main` to `source`, which will become the entrypoint for Parcel. `main` should then point to the target that Parcel will build to. 

By default, [Parcel does not bundle `node_modules` for library targets](https://parceljs.org/features/targets/#library-targets), but in this exercise, we'd like to do that. Tell Parcel to bundle `node_modules` by adding `"includeNodeModules": true` to your target in `package.json`. 

```
  "targets": {
    "main": {
      "includeNodeModules": true
    },
  },
```