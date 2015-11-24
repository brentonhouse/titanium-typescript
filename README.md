# Titanium Typescript

Ambient declarations for the **Appcelerator Titanium SDK v5.0.0 and Appcelerator Alloy 1.7.x**.


## Build

*Run the following commands from inside the source folder.*

----------

##### Install [Microsoft TypeScript](https://github.com/Microsoft/TypeScript "Microscript TypeScript")

```
	npm install -g typescript
```
##### Install dependencies

	npm install

##### Build the project and generator the file `Generator.js`

    tsc -m commonjs -t ES5 -sourcemap References.ts

##### Obtain the documentation json files

Download the `api.json` and `alloy_api.json` files for the target Appcelerator Titanium and Alloy versions from [here](http://docs.appcelerator.com/titanium/data/index.html) and place them in the same directory as the Generator.js file.


##### Generate the _Appcelerator Titanium Mobile_ definitions:

    node Generator.js api.json > titanium.d.ts

##### Generate the _Appcelerator Alloy_ definitions:

    node Generator.js alloy_api.json > alloy.d.ts

## Known issues

*	In `Titanium.Map.View` there is a conflict with the property `animate` and two methods with the same id. The property `animate` has been taken out from the definition.
*	In `Database.ResultSet` the property `fieldCount` has been removed. Instead you can use the method `getFieldCount()`.
*   Methods that accept an arbitrary number arguments are not detected as such because Appcelerator's `api.json` does not appear to contain this information.
*   All callbacks are `(...args : any[]) => any`

## Manual Corrections

*	Methods that `...extraPaths: string[]` should be appended to their argument signature: Titanium.Filesystem.getFile, Titanium.Filesystem.openStream
*   Find `export enum R {` and replace with `export interface R {`
*   Find `show (animated: boolean, view: any) : void;` and replace with `show () : void;`
*   Find `declare enum FailureResponse {` and replace with `declare class FailureResponse {code: Number; error: string; success: boolean;`

## Future work

For future work, it would be interesting to implement **interface inheritance** in order to avoid
repeated inherited methods or properties in subclasses.