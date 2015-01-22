Labs
===========

 

##Access the API using CURL

In this lab exercise we are going to work with teh type system. If you are familiar with JSON syntax this should be easy for you to follow. (If not we recommend that you read )

At the end of this lab you will have accomplished the following:  
1. Made a basic query against the API  
2. Create a new type  
3. Query the type definition  
4. Post data to the type  
5. Query data from the type you have created  
6. Extend the type  

To use the following examples you must replace the following

your_namespace with your namespace
username with your user name
password with your password

These examples use the basic auth 


###Query the type system

````
curl -X GET -H Content-Type:application/json -u username:password https://api.redbookcloud.com/your_namespace/types   
````

###Create a type

````  
curl -X POST -H Content-Type:application/json -u username:password -d '{
  "name": "team_member",
  "storage_name": "team_member",
  "interface": {},
  "views": {},
  "version": "1",
  "namespace": "your_namespace",
  "properties": {
    "EmployeeId": {
      "required": true,
      "type": "String"
    },
     "EmployeeName": {
      "required": true,
      "type": "String"
    },
    "Store": {
      "required": true,
      "type": "String"
    },
    "Position": {
      "required": true,
      "type": "String"
    },
    "State": {
      "required": true,
      "type": "String"
    },
    "HireDate": {
      "required": true,
      "type": "String"
    }
  }
}' https://api.redbookcloud.com/your_namespace/types
````  

###Check the type was created

````   
curl -X GET -H Content-Type:application/json -u username:password https://api.redbookcloud.com/your_namespace/types/team_member
```` 

###Query data from the type


````   
curl -X GET -H Content-Type:application/json -u username:password https://api.redbookcloud.com/your_namespace/resources/team_member | json_pp
```` 
**Note: ** You should get an empty array returned, because you have not posted any data yet.


###Post data to the type


````   
curl -X POST -H Content-Type:application/json -u username:password -d '{
    "EmployeeId": "100",
    "EmployeeName": "Rick Deckard",
    "Store": "store1",
    "Position": "Manager",
    "State": "Active",
    "HireDate": "2014-06-21"
}' https://api.redbookcloud.com/your_namespace/resources/team_member
```` 


###Query data from the type


````   
curl -X GET -H Content-Type:application/json -u username:password https://api.redbookcloud.com/your_namespace/resources/team_member
```` 



###Extend the schema

````
curl -X PUT -H Content-Type:application/json -u username:password -d '{
  "name": "team_member",
  "storage_name": "team_member",
  "interface": {},
  "views": {},
  "version": "1",
  "namespace": "your_namespace",
  "properties": {
    "EmployeeId": {
      "required": true,
      "type": "String"
    },
     "EmployeeName": {
      "required": true,
      "type": "String"
    },
    "Store": {
      "required": true,
      "type": "String"
    },
    "Position": {
      "required": true,
      "type": "String"
    },
    "State": {
      "required": true,
      "type": "String"
    },
    "HireDate": {
      "required": true,
      "type": "String"
    },
     "PromotionDate": {
      "required": false,
      "type": "String"
    }
  }
}' https://api.redbookcloud.com/your_namespace/types
````

###Update the data

````
curl -X PUT -H Content-Type:application/json -u username:password -d '{
    "EmployeeId": "100",
    "EmployeeName": "Rick Deckard",
    "Store": "store1",
    "Position": "Manager",
    "State": "Active",
    "HireDate": "2014-06-21",
    "PromotionDate": "2014-07-21"
}' https://api.redbookcloud.com/your_namespace/resources/team_member
````

###Query data from the type


````   
curl -X GET -H Content-Type:application/json -u username:password https://api.redbookcloud.com/your_namespace/resources/team_member
```` 




##Access the API using Bodhi command line

In this lab exercise we are going to work with the type system using Bodhi CLI. 

At the end of this lab you will have accomplished the following:  
1. Made a query against the API to display all types in the system  
2. List the properties of a type  
3. Create a new type  
4. Quicky create a data file to populate the type 
5. Post data to the type   

To use the following examples you must set up your project.json file as described in the set up instructions for the Bodhi CLI.


bodhi-types --help
bodhi-types ls
bodhi-types get team_member
bodhi-types lp team_member
bodhi-types new survey --KFC-UK
bodhi-types set-prop survey name
bodhi-types set-prop survey name -S
bodhi-types set-prop survey survey_date -T
bodhi-types set-prop survey survey_rating -I
bodhi-types set-prop survey survey_comments -S
bodhi-types post survey
bodhi-types get survey 
bodhi-types gen-instance survey


