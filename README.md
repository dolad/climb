# climb
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
		<title>Untitled Document</title>
		<link href="jquery-3.1.1.js" rel="stylesheet" type="text/css" />
		<link href="css/bootstrap.css" rel="stylesheet" type="text/css" />
		<script type="text/javascript" src="jquery-3.1.1.js"></script>
		<script type="text/javascript" src="bootstrap-4.0.0-alpha.6-dist/js/bootstrap.js"> </script>
</head>
<body>

	<style>
.legend{ position:absolute;
		 left:250px;
		 top:150px;
		 background-color: #F8F8FF;
		 color:	#191970;
		 padding: 50px;
		 border-color:blue;
		 border-style: solid;
		 outline-color: red;
}
.display{
	position: absolute;
	left:1000px;
	top: 150px;
	background-color:#F8F8FF; 
	color:	#191970;
	border-style: solid;
	 border-color:blue;
}


</style>
</head>
<body>
	<div class="col-sm-6 legend">
		<form class="form-horizontal">
		  <div class="form-group">
			   			   <label class="control-label col-sm-2" for="email">FirstName</label>
						   <div class="col-sm-10">
					      		<input type="text" class="form-control" id="firstname" placeholder="Enter first name">
					       </div>
		  </div>
		  		  <div class="form-group">
			   			   <label class="control-label col-sm-2" for="email">lastName</label>
						   <div class="col-sm-10">
					      		<input type="text" class="form-control" id="last" placeholder="Enter last name">
					       </div>
		  </div>
		  <div class="form-group">
		    				<label class="control-label col-sm-2" for="pwd">Phone number:</label>
		    				<div class="col-sm-10"> 
		      				    <input type="text" class="form-control" id="phonenumber" placeholder="Enter valid phonenumber">
		    				</div>
		  </div>
		 
		  
		  <div class="form-group"> 
		    			<div class="col-sm-offset-2 col-sm-10">
		      				<button class="btn btn-info bot" id="btn1" >Add</button>
		    			</div>
		  </div>
	</form>
		
			<ul class='display' id="contactList">
  			</ul>
  		
		
	</body>
	<script>

	
	function contact(id, first, last, phone) {
    this.id = id;
    this.first = first;
    this.last = last;
    this.phone = phone;
 
}

var contacts = new Array();

window.onload = init;

function init() {
    var submitButton = document.getElementById("btn1");
    submitButton.onclick = submitFrom;

    
}
function parsecontactItems(contactJSON) {
    if (contactJSON == null || contactJSON.trim() == "") {
        return;
    }
    var contactArray = JSON.parse(contactJSON);
    if (contactArray.length == 0) {
        console.log("Error: the to-do list array is empty!");
        return;
    }
    for (var i = 0; i < contactArray.length; i++) {
        var contactItem = contactArray[i];
        contacts.push(contactItem);
    }
}
function addcontactsToPage() {
    var ul = document.getElementById("contactList");
    var listFragment = document.createDocumentFragment();
    for (var i = 0; i < contacts.length; i++) {
        var contactItem = contacts[i];
        var li = createNewContact(contactItem);
        listFragment.append(li);
    }
    ul.appendChild(listFragment);
}
function addcontactToPage(contactItem) {

    var ul = document.getElementById("contactList");
    var li = createNewContact(contactItem);
    ul.appendChild(li);	

    
   
}
//this add a new contact item to the page but i dont know why it is not always showing am stuck at this point
function createNewContact(contactItem) {
    var li = document.createElement("li");  
    var span= '<span>'+contactItem.last+'</span>';

    li.appendChild(span)
  
    return li;
}
   // this collect data from the form   
function submitFrom() {

    var task = document.getElementById("firstname").value;
    if (checkInputText(task, "Please enter your firstname")) return;

    var who = document.getElementById("last").value;
    if (checkInputText(who, "Please enter ur lastname")) return;

    var date = document.getElementById("phonenumber").value;
    if (checkInputText(date, "Please enter a phonenumber")) return;
    
    var id = contacts.length;
    var contactItem = new contact(id, first, last, phone);
    contacts.push(contactItem);
    addcontactToPage(contactItem);
    savecontactItem(contactItem);

}
//this display an alert to the previous function created
function checkInputText(value, msg) {
    if (value == null || value == "") {
        alert(msg);
        return true;
    }
    return false;
}
// this save my data from the form to the local storage
function savecontactItem(contactItem) {
    if (localStorage) {
        var key = "contact" + contactItem.id;
        var item = JSON.stringify(contactItem);
        localStorage.setItem(key, item);
        
    }
    else {
        console.log("Error: you don't have localStorage!");
    }
}
	</script>
