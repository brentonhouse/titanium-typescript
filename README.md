# Titanium Typescript

Ambient declarations for the **Titanium Appcelerator API v4.1.0**.

	var ROWS: number = 10;
	var children: Array<Titanium.UI.View> = button.getChildren();
		
	var window: Titanium.UI.Window = Titanium.UI.createWindow({
		title: 'example',
		backgroundColor: 'white'
	});
	
	var tableView: Titanium.UI.TableView = Titanium.UI.createTableView();
	var dataSource: Array<Titanium.UI.TableViewRow> = [];
	
	for (var i: number = 0; i < ROWS; i++) {
		dataSource.push(Titanium.UI.createTableViewRow({
			title: 'Row ' + i,
			hasChild: false
		}));
	}
	
	tableView.data = dataSource;

# Build

Obtain an `api.json` file from [here](http://docs.appcelerator.com/titanium/data/index.html)

To build the project:

    tsc -m commonjs -t ES5 -sourcemap References.ts

The above command line generates the file Generator.js. To generate the _Titanium Mobile_ definitions:

    node Generator.js api.json > titanium.d.ts

# Known issues

*	In `Titanium.Map.View` there is a conflict with the property `animate` and two methods with the same id. The property `animate` has been taken out from the definition.
*	In `Database.ResultSet` the property `fieldCount` has been removed. Instead you can use the method `getFieldCount()`.
*   Methods that accept an arbitrary number arguments are not detected as such because Appcelerator's `api.json` does not appear to contain this information.
*   All callbacks are `(...args : any[]) => any`

# Manual Corrections

*	Methods that `...extraPaths: string[]` should be appended to their argument signature: Titanium.Filesystem.getFile, Titanium.Filesystem.openStream
*   Find `export enum R {` and replace with `export interface R {`
*   Find `show (animated: boolean, view: any) : void;` and replace with `show () : void;`
*   Find `declare enum FailureResponse {` and replace with `declare class FailureResponse {code: Number; error: string; success: boolean;`

# Future work

For future work, it would be interesting to implement **interface inheritance** in order to avoid
repeated inherited methods or properties in subclasses.