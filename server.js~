var express = require('express');                                                
var app = express();
var path=require('path');
var bodyParser = require('body-parser');
    var mysql = require('mysql');
var con = mysql.createConnection({
  host: "testbed2.riktamtech.com",
  user: "root",
  password: "lkgukg",
  database: "test1"
});
   var departments;
con.connect(function(err) {
  if (err) throw err;
  console.log("Connected!");
});

var PORT = process.env.PORT || 3000;

app.use(express.static(__dirname));
app.use(bodyParser.json());
//app.get("/", function(req, res) {
  //  res.sendFile(path.join(__dirname+'/index.html'));
//});
app.get('/departments', function(req, res) {
  console.log("request for s  listing");
 
  con.query("SELECT * FROM departments ",function(err, rows, fields) {
        if (err) throw err;
    console.log("listing");
//console.log(JSON.stringify(rows, null,2 ));
	res.send(JSON.stringify(rows, null,2 ));
});  
     
    
});

app.post('/departments/:depname', function(req, res) {
    var productName = req.body.depname;
    
    console.log(productName);
var da = {
            depname: req.params.depname,
        }
  con.query("INSERT INTO departments SET ?",da , function(err, result) {
    if (err) throw err;

    console.log("1 record inserted");
    console.log(da.depname);
  });
    res.send('Successfully created product!');

});

app.put('/departments/:depid/:depname', function(req, res) {

   // var id = req.params.depid;
    var newName = req.params.depname;
    var da = {
      depname: req.params.depname,
      };
    console.log("update me");
   
     con.query("UPDATE departments SET ? WHERE depid = " + req.params.depid, da, function(err, result){

     });
    res.send('Succesfully updated product!');
});

app.delete('/departments/:depid', function(req, res) {
con.query("DELETE FROM departments WHERE depid = " + req.params.depid, function(err, result) {
    if (err) throw err;
    
  });     
    console.log("1 record deleted");

    res.send('Successfully deleted product!');
});
//////////////////////////////////////////////////////

app.get('/students/:depid', function(req, res) {
  
 
  con.query("SELECT * FROM students WHERE sdepid = " + req.params.depid, function(err, result) {
        if (err) throw err;
    console.log("listing students");
res.send(JSON.stringify(result, null,2 ));
});  
     
    
});

app.post('/students/:sname/:depid', function(req, res) {
    var sname = req.body.sname;
   
    
    console.log("in add student server query "+ sname);
var da = {
            sname : req.params.sname,
    	   
            sdepid: req.params.depid
            }
  con.query("INSERT INTO students SET ?",da , function(err, result) {
    if (err) throw err;

    console.log("1 student record inserted");
  
  });
   res.send('Successfully created student!');

});

app.put('/students/:id/:sname/:sdepid', function(req, res) {

    var id = req.params.id;
    
    var da = {
     sname : req.params.sname,
     sdepid: req.params.sdepid};
    console.log("update me" +req.params.sname);
     
     con.query("UPDATE students SET ? WHERE id = " + req.params.id, da, function(err, result){

     });
    res.send('Succesfully updated product!');
});

app.delete('/students/:id', function(req, res) {
    //var depid = req.params.depid;
con.query("DELETE FROM students WHERE id = " + req.params.id, function(err, result) {
    if (err) throw err;
    
  });     
    console.log("1 record deleted");

    res.send('Successfully deleted product!');
});
////////////////////////////

app.listen(PORT, function() {
    console.log('Server listening on ' + PORT);
});
