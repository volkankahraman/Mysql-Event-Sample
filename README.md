# Mysql-Event-Sample

Track Database Activity with NodeJs
Based on this [package](https://www.npmjs.com/package/@rodrigogs/mysql-events).

**Connection**
``` javascript
const connection = mysql.createConnection({
host: 'localhost',
user: 'root',
password: '12345678',
});
```
**Instance**
``` javascript
const instance =  new MySQLEvents(connection, {
	startAtEnd: true,
	excludedSchemas: {
		mysql: true,
	},
});
```
**Instance Trigger**
``` javascript
instance.addTrigger({
	name: 'TEST', // Database name
	expression: '*',
	statement: MySQLEvents.STATEMENTS.ALL, // e.g STATEMENTS.ALL
	onEvent: (event) => { // You will receive the events here
		console.log(event);
		event.affectedRows.forEach(element => {
			console.log(element.after);// List added or updated rows
			console.log(element.before); // List deleted or updated rows
		});
	},
});
```
