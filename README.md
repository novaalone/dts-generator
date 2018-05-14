.d.ts generator
===============
Forks of dts-generator, add params to replace the main module name

## Usage

1. `npm install dts-gen-xx`

2. Generate your `d.ts` bundle:

   Programmatically:

```js
require('dts-gen-xx').default({
		name: 'package-name',
		project: '/path/to/package-directory',
		out: 'package-name.d.ts'
});
```

   Command-line:

```bash
dts-gen --name package-name --project /path/to/package-directory --out package-name.d.ts
```

   Grunt:

```js
module.exports = function (grunt) {
	grunt.loadNpmTasks('dts-gen-xx');
	grunt.initConfig({
		dtsGenerator: {
			options: {
				name: 'package-name',
				project: '/path/to/package-directory',
				out: 'package-name.d.ts'
			},
			default: {
				src: [ '/path/to/package-directory/**/*.ts' ]
			}
		}
	});
};
```

3. Reference your generated d.ts bundle from somewhere in your consumer module and import away!:

```ts
/// <reference path="typings/package-name.d.ts" />

import Foo = require('package-name/Foo');

// ...
```

## Options

* `baseDir?: string`: The base directory for the package being bundled. Any dependencies discovered outside this
  directory will be excluded from the bundle.  *Note* this is no longer the preferred way to configure `dts-generator`, please see `project`.
* `exclude?: string[]`: A list of glob patterns, relative to `baseDir`, that should be excluded from the bundle. Use
  the `--exclude` flag one or more times on the command-line. Defaults to `[ "node_modules/**/*.d.ts" ]`.
* `externs?: string[]`: A list of external module reference paths that should be inserted as reference comments. Use
  the `--extern` flag one or more times on the command-line.
* `types?: string[]`: A list of external @types package dependencies that should be inserted as reference comments. Use
  the `--types` flag one or more times on the command-line.
* `files: string[]`: A list of files from the baseDir to bundle.
* `eol?: string`: The end-of-line character that should be used when outputting code. Defaults to `os.EOL`.
* `indent?: string`: The character(s) that should be used to indent the declarations in the output. Defaults to `\t`.
* `main?: string`: The module ID that should be used as the exported value of the package’s “main” module.
* `moduleResolution?: ts.ModuleResolutionKind`: The type of module resolution to use when generating the bundle.
* `name: string`: The name of the package. Used to determine the correct exported package name for modules.
* `out: string`: The filename where the generated bundle will be created.
* `project?: string`: The base directory for the project being bundled.  It is assumed that this directory contains a `tsconfig.json` which will be parsed to determine the files that should be bundled as well as other configuration information like `target`
* `target?: ts.ScriptTarget`: The target environment for generated code. Defaults to `ts.ScriptTarget.Latest`.
* `replaceModule?: string`: The target main module name in your project.
* `mainModule?: string`: The original main module name in your project.
* `resolveModuleId: (params: ResolveModuleIdParams) => string`: An optional callback provided by the invoker to customize the declared module ids the output d.ts files. For details see [resolving module ids](docs/resolving-module-ids.md).
* `resolveModuleImport: (params: ResolveModuleImportParams) => string`: An optional callback provided by the invoker to customize the imported module ids in the output d.ts files. For details see [resolving module ids](docs/resolving-module-ids.md).


## Thanks

[dts-generator](https://github.com/SitePen/dts-generator) for the open source code.
