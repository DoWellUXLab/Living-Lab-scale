# 100035-DowellScale-Function
# Steps to follow:
- Create a new branch from the main branch.
- Branch name should be Task thet you are working + your name.

*Note: You should not push the code to main branch.*

## NPS Scale APIs for data retrieval

## SETTINGS

### 1. Create a scale with a specific setting

#### Request METHOD : POST, PUT, GET
#### End-Point : https://100035.pythonanywhere.com/api/nps_settings_create/
#### If request METHOD : GET

```python
    {
    "scale_id": "63e8b4c87f4aa8f650162b7a",   #scale_id that you would wish to retrieve its details
    }
    
```
## Update Scale through Settings(PUT)
#### Request METHOD: GET
#### URL: https://100035.pythonanywhere.com/nps-editor/settings/<str:Mongodb_ID>
#### Example: https://100035.pythonanywhere.com/nps-editor/settings/63e8b4c87f4aa8f650162b7a


#### If request METHOD : PUT
#### pass any field you would love to update when calling the PUT request
#### Example of body. Its not a must all fields are provided, only provided fields will be updated without looasing the previous saved settings
```python
{
"scale_id": "63e8b4c87f4aa8f650162b7a" ,    #Scale ID is mandatory when sending PUT request.

"username": "your name",        #your username

"orientation": "horizontal",    #orientation of the scale- horizontal/ vertical

"scalecolor": "#8f1e1e",        #bg color of the scale

"roundcolor": "#938585",        #color of the buttons in the scale

"fontcolor": "#000000",        #color of the text inside the buttons

"fomat": "numbers",            #format in which you wish the response to be recorded- numbers, stars, emojis

"time": "60",                 #time limit in seconds that you wish to assign for providing each response- any natural no.

"name": "testAPI",            #name you wish to assign to the scale

"left": "good",               #label for the lowest rating (zero)- text

"right": "best",              #label for the highest rating (10)- text

"center": "neutral",          #label for  neutral ratings- text
}    
```

#### Example of the body to be sent in the API : POST

```python

{
"username": "your name",        #your username

"orientation": "horizontal",    #orientation of the scale- horizontal/ vertical

"scalecolor": "#8f1e1e",        #bg color of the scale

"roundcolor": "#938585",        #color of the buttons in the scale

"fontcolor": "#000000",        #color of the text inside the buttons

"fomat": "numbers",            #format in which you wish the response to be recorded- numbers, stars, emojis

"time": "60",                 #time limit in seconds that you wish to assign for providing each response- any natural no. Put time to 0 is you dont want timing on scale generated.

"name": "testAPI",            #name you wish to assign to the scale

"left": "good",               #label for the lowest rating (zero)- text

"right": "best",              #label for the highest rating (10)- text

"center": "neutral",          #label for  neutral ratings- text
}                                

```
### Response to API

```python
#Success
{
    "success": "{\"isSuccess\": true, \"inserted_id\": \"63e4c9676d29b0d8177814a4\"}",
    "payload": {
        "event_id": "FB1010000000167593814551606998",
        "settings": {
            "orientation": "horizontal",
            "numberrating": 10,
            "scalecolor": "#8f1e1e",
            "no_of_scales": 1,
            "roundcolor": "#938585",
            "fontcolor": "#000000",
            "fomat": "numbers",
            "time": "60",
            "template_name": "TestDic8931",
            "name": "TestDic",
            "text": "good+neutral+best",
            "left": "good",
            "right": "best",
            "center": "neutral",
            "scale-category": "nps scale",
        }
    },
    "scale_urls": "http://127.0.0.1:8000/nps-scale1/TestDic8931?brand_name=your_brand&product_name=product_name"
}

#Failure 
Response=({"error": "Invalid data provided."},status=status.HTTP_400_BAD_REQUEST)
```


### 2.Fetch the settings data for a particular scale using the template/ scale name
#### Request METHOD : GET/name (here, name is the scale name)
#### End-Point : https://100035.pythonanywhere.com/api/nps_settings/<str: template_name>


# RESPONSE (SCALE REPORTS)
### 1. Provide a response to a particular scale instance using the corresponding scale details
#### Request METHOD :  POST
#### End-Point : https://100035.pythonanywhere.com/api/nps_responses_create


### Example of the body to be sent in the API : 

```python
{

"template_name": "scale name",
#name of the parent scale


"instance_id":6 ,
#instance id of the instance you wish to provide a response to


"brand_name":"brand_name",
#name of the brand the scale is being used for


"product_name":"product_name",
#name of the product the scale is being used for


"score":7,
#the score you wish to assign as a response


"username": "your name"
#your user name

}


```

### 1. Dynamically generate instances
#### Request METHOD : POST 
#### End-Point : https://100035.pythonanywhere.com/api/nps_create_instance
```python
{   
    "scale_id":"63e8b9757f4aa8f650162bcc",       #scale_id you wish to generate instance
    "no_of_documents": 2                         #can be optional. If it is not provided the scale will only create one instance per request.
}

```
### 2. Fetch the response data for a single scale from the database
#### Request METHOD : GET/_id (here, the _id is the default mongo db _id)
#### End-Point : https://100035.pythonanywhere.com/api/nps_responses/<str: _id>

### 3.Fetch the response data for all NPS scales
#### Request METHOD : GET
#### End-Point : https://100035.pythonanywhere.com/api/nps_responses


## TOTAL SCORE

### 1.Fetch/calculate all scores of all instances of a particular scale using the unique template name
#### Request METHOD : GET/name (here, name is template_name)
#### End-Point : https://100035.pythonanywhere.com/api/total_responses/<str: template_name>

## NPS Scale APIs for data retrieval

## CUSTOM CONFIGURATIONS

### 1. Create/Retrieve/Update custom configurtions

#### Request METHOD : POST, PUT, GET
#### End-Point : https://100035.pythonanywhere.com/api/nps_custom_data_all
#### If request METHOD : GET

```python
    {
        "template_id": "47576",                              #template Id to retrieve all elements present in a template
    }
    
```
#### Request METHOD : POST, PUT, GET
#### End-Point : https://100035.pythonanywhere.com/api/nps_custom_data/
#### If request METHOD : GET

```python
    {
    "scale_id": "63e8b4c87f4aa8f650162b7a",   #scale_id that you would wish to retrieve its details
    }
    
```
#### If request METHOD : POST

```python
    {

        "template_id": "27289",                                          #Template id for the editor
        "scale_id": "63e8b4c87f4aa8f650162b7a",                          #Id for the current scale     
        "custom_input_groupings": {'t1': 'id', 'i1': 'id'}   #Groupings of elements related to the scale 
        "scale_label": "scale_label"                                     #Scale Label Provided by the user
    }
    
```

#### if request METHOD : PUT 
```python
    {

        "custom_input_groupings": {'t1': 'id', 'i1': 'id'}               #Groupings of elements related to the scale 
        "scale_label": "scale_label"                                     #Scale Label Provided by the user
    }
```

# 100035-DowellScale-Function

## NPS Scale APIs for data retrieval

## SETTINGS

### 1. Create a scale with a specific setting

#### Request METHOD : POST, PUT, GET
#### End-Point : https://100035.pythonanywhere.com/api/nps_settings_create/
#### If request METHOD : GET

```python
    {
    "scale_id": "63e8b4c87f4aa8f650162b7a",   #scale_id that you would wish to retrieve its details
    }
    
```
## Update Scale through Settings(PUT)
#### Request METHOD: GET
#### URL: https://100035.pythonanywhere.com/nps-editor/settings/<str:Mongodb_ID>
#### Example: https://100035.pythonanywhere.com/nps-editor/settings/63e8b4c87f4aa8f650162b7a


#### If request METHOD : PUT
#### pass any field you would love to update when calling the PUT request
#### Example of body. Its not a must all fields are provided, only provided fields will be updated without looasing the previous saved settings
```python
{
"scale_id": "63e8b4c87f4aa8f650162b7a" ,    #Scale ID is mandatory when sending PUT request.

"username": "your name",        #your username

"orientation": "horizontal",    #orientation of the scale- horizontal/ vertical

"scalecolor": "#8f1e1e",        #bg color of the scale

"roundcolor": "#938585",        #color of the buttons in the scale

"fontcolor": "#000000",        #color of the text inside the buttons

"fomat": "numbers",            #format in which you wish the response to be recorded- numbers, stars, emojis

"time": "60",                 #time limit in seconds that you wish to assign for providing each response- any natural no.

"name": "testAPI",            #name you wish to assign to the scale

"left": "good",               #label for the lowest rating (zero)- text

"right": "best",              #label for the highest rating (10)- text

"center": "neutral",          #label for  neutral ratings- text
}    
```

#### Example of the body to be sent in the API : POST

```python

{
"username": "your name",        #your username

"orientation": "horizontal",    #orientation of the scale- horizontal/ vertical

"scalecolor": "#8f1e1e",        #bg color of the scale

"roundcolor": "#938585",        #color of the buttons in the scale

"fontcolor": "#000000",        #color of the text inside the buttons

"fomat": "numbers",            #format in which you wish the response to be recorded- numbers, stars, emojis

"time": "60",                 #time limit in seconds that you wish to assign for providing each response- any natural no. Put time to 0 is you dont want timing on scale generated.

"name": "testAPI",            #name you wish to assign to the scale

"left": "good",               #label for the lowest rating (zero)- text

"right": "best",              #label for the highest rating (10)- text

"center": "neutral",          #label for  neutral ratings- text
}                                

```
### Response to API

```python
#Success
{
    "success": "{\"isSuccess\": true, \"inserted_id\": \"63e4c9676d29b0d8177814a4\"}",
    "payload": {
        "event_id": "FB1010000000167593814551606998",
        "settings": {
            "orientation": "horizontal",
            "numberrating": 10,
            "scalecolor": "#8f1e1e",
            "no_of_scales": 1,
            "roundcolor": "#938585",
            "fontcolor": "#000000",
            "fomat": "numbers",
            "time": "60",
            "template_name": "TestDic8931",
            "name": "TestDic",
            "text": "good+neutral+best",
            "left": "good",
            "right": "best",
            "center": "neutral",
            "scale-category": "nps scale",
        }
    },
    "scale_urls": "http://127.0.0.1:8000/nps-scale1/TestDic8931?brand_name=your_brand&product_name=product_name"
}

#Failure 
Response=({"error": "Invalid data provided."},status=status.HTTP_400_BAD_REQUEST)
```


### 2.Fetch the settings data for a particular scale using the template/ scale name
#### Request METHOD : GET/name (here, name is the scale name)
#### End-Point : https://100035.pythonanywhere.com/api/nps_settings/<str: template_name>


# RESPONSE (SCALE REPORTS)
### 1. Provide a response to a particular scale instance using the corresponding scale details
#### Request METHOD :  POST
#### End-Point : https://100035.pythonanywhere.com/api/nps_responses_create


### Example of the body to be sent in the API : 

```python
{

"template_name": "scale name",
#name of the parent scale


"instance_id":6 ,
#instance id of the instance you wish to provide a response to


"brand_name":"brand_name",
#name of the brand the scale is being used for


"product_name":"product_name",
#name of the product the scale is being used for


"score":7,
#the score you wish to assign as a response


"username": "your name"
#your user name

}


```

### 1. Dynamically generate instances
#### Request METHOD : POST 
#### End-Point : https://100035.pythonanywhere.com/api/nps_create_instance
```python
{   
    "scale_id":"63e8b9757f4aa8f650162bcc",       #scale_id you wish to generate instance
    "no_of_documents": 2                         #can be optional. If it is not provided the scale will only create one instance per request.
}

```
### 2. Fetch the response data for a single scale from the database
#### Request METHOD : GET/_id (here, the _id is the default mongo db _id)
#### End-Point : https://100035.pythonanywhere.com/api/nps_responses/<str: _id>

### 3.Fetch the response data for all NPS scales
#### Request METHOD : GET
#### End-Point : https://100035.pythonanywhere.com/api/nps_responses


## TOTAL SCORE

### 1.Fetch/calculate all scores of all instances of a particular scale using the unique template name
#### Request METHOD : GET/name (here, name is template_name)
#### End-Point : https://100035.pythonanywhere.com/api/total_responses/<str: template_name>

## NPS Scale APIs for data retrieval

## CUSTOM CONFIGURATIONS

### 1. Create/Retrieve/Update custom configurtions

#### Request METHOD : POST, PUT, GET
#### End-Point : https://100035.pythonanywhere.com/api/nps_custom_data_all
#### If request METHOD : GET

```python
    {
        "template_id": "47576",                              #template Id to retrieve all elements present in a template
    }
    
```
#### Request METHOD : POST, PUT, GET
#### End-Point : https://100035.pythonanywhere.com/api/nps_custom_data/
#### If request METHOD : GET

```python
    {
    "scale_id": "63e8b4c87f4aa8f650162b7a",   #scale_id that you would wish to retrieve its details
    }
    
```
#### If request METHOD : POST

```python
    {

        "template_id": "27289",                                          #Template id for the editor
        "scale_id": "63e8b4c87f4aa8f650162b7a",                          #Id for the current scale     
        "custom_input_groupings": {'t1': 'id', 'i1': 'id'}   #Groupings of elements related to the scale 
        "scale_label": "scale_label"                                     #Scale Label Provided by the user
    }
    
```

#### if request METHOD : PUT 
```python
    {

        "custom_input_groupings": {'t1': 'id', 'i1': 'id'}               #Groupings of elements related to the scale 
        "scale_label": "scale_label"                                     #Scale Label Provided by the user
    }
```

