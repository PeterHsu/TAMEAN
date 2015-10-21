```javascript
var Sequelize = require('sequelize');
var sequelize = new Sequelize('Northwind', 'sa', 'P@ssw0rd', {
  host: 'localhost',
  dialect: 'mssql',
  pool: {
    max: 5,
    min: 0,
    idle: 10000
  },
  dialectOptions:{
	  instanceName:'sqlexpress'
  }
});
sequelize.query('select * from Region where RegionID=1',{type:sequelize.QueryTypes.SELECT})
.then(function(data){
	console.log(data[0].RegionDescription);
});
/*
var User = sequelize.define('Region', {
  RegionID: {
    type: Sequelize.INTEGER,
	primaryKey:true
  },
  RegionDescription:{
	  type: Sequelize.STRING,
  }
},{
	createdAt:false,
	updatedAt:false,
  freezeTableName: true // Model tableName will be the same as the model name
});

User.findByID().then(function(data){
	console.log(data.name);
});
*/
```
