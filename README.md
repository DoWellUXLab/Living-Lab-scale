# LivingLab Scales API Documentation

Welcome to the LivingLab Scales API documentation. The LivingLab Scales API provides a comprehensive set of features and capabilities to help you effectively manage and analyze various types of statistical scales. With these features, you can easily create, configure, and analyze NPS scales, Likert scales, Staple scales, Percentage scales, Percent Sum scales, Guttman scales, and many more.

## Key Features

1. **Create and Configure Statistical Scales**: The API allows you to create statistical scales with specific settings tailored to your requirements. You can choose from 15 different types of scales, including NPS scales, Likert scales, Staple scales, Percentage scales, Percent Sum scales, Guttman scales, and more. By customizing the settings, you can define the scale's appearance, labels, response options, and other visual elements.

2. **Retrieve and Update Scale Settings**: You can retrieve and update the settings of existing statistical scales using the update scale end-points. This feature enables you to make modifications to the scale configuration as needed. Whether you want to change the orientation, update the colors, or modify the labels, the API provides a convenient way to manage and maintain your statistical scales.

3. **Generate Scale Instances**: The API offers functionality to dynamically generate scale instances. You can specify the number of instances to create, and the API will generate unique instances of the selected statistical scale. This feature is useful when you need to distribute the scale to multiple users or gather feedback from a large number of respondents.

4. **Collect Responses to Scale Instances**: With the LivingLab Scales API, you can collect responses to individual scale instances. When a user or respondent interacts with the statistical scale, you can capture their feedback and store it in the database. The API allows you to provide responses, including the instance ID, brand name, product name, and score.

5. **Retrieve Scale Reports and Response Data**: The API enables you to fetch detailed reports and response data for your statistical scales. You can retrieve data for a particular scale using its template or scale name. Additionally, you can access response data for all scales of the same type or retrieve data for a specific scale instance using its unique ID.

## Getting started
To start utilizing the robust features of the LivingLab API, follow these simple steps to consume the API effectively:

**Step 1: Obtain the API key**

Before diving into the API integration, make sure that you have the necessary API key. You can generate your API key through the [DoWell API Key](https://ll05-ai-dowell.github.io/100105-DowellApiKeySystem/) Software

**Step 2: Set the base URL**

To make requests to the API, set the base url as `https://100035.pythonanywhere.com/api/scales/`

**Step 3: Attach the query string parameters to the base URL**

The API expects two parameters in the base URL -- `scale_type` and `type` based on the values of which you can avail the different functionalities offered by the API.
-  scale type :
The `scale_type` query parameter is included to specify the fundamental type of statisical scale that the user wishes to work with. It allows users to choose from a variety of pre-defined scale types.

    Possible values for `scale_type`: `nps`, `npslite`, `stapel`, `likert`, `percent`, `percent_sum`

- type: The `type` query parameter govers the functionalities or the actions to be taken for the chosen `scale_type`.
    
    Possible values for `type` :

    1. `settings`: 

    Assign this value when you wish to create and customize a scale from scratch. With this option, one can define various parameters such as orientation, scale color, time, scale labels, and other attributes to create a scale according to their on will.

    2. `response` :

    Assign this value when you wish to provide a rating or response to an existing scale in the database. By specifying this option, you can easily submit numerical and textual  responses within the defined range of the selected scale.

By expertly leveraging the `scale_type` and `type` query parameters, you can unlock the full potential of the LivingLab Scale API, effortlessly tailoring its capabilities to suit your unique requirements. 

**Syep 4: Structure Your Requests**

Craft your API requests by incorporating the chosen `scale_type` and `type` values into the URL and using the appropriate ```POST```,```PUT```,```GET``` request method along with the desired request body. 

**Step 5: Handle Errors Gracefully**
The API follows standard HTTP status codes for error handling. Be sure to implement error handling in your code to gracefully manage potential errors and informative error messages.

**Step 6: Parse API Responses**
When you receive a response from the API, ensure you parse the data accurately to extract the relevant information you need.

## API Functionality Overview
### 1. Create your scale from scratch
```python
REQUEST METHOD : POST
type = settings
```

For creating a scale from scratch you would need to provide the necessary 'settings' for the scale in the request body.

***Note that the input parameters for creating a scale are subjective to a particular scale type.*** 

An example of the request body for each scale is mentioned below.

1.  scale_type = nps, type = settings
```python
{
    "api_key":<str: your-api-access-key>,       
    "username": <str: username>,# your username
    "orientation": "vertical",  # orientation of the scale-- "horizontal"/"vertical"
    "scalecolor": "#8f1e1e",    # scale background color
    "roundcolor": "#938585",    # colour of the buttons in the scale
    "fontcolor": "#000000",     # colour of the fonts
    "time": "60",               # time (in seconds) within which the respondent should provide an answer. Set "00" to disable time restrictions
    "name": "scalename",        # unique name identifier for the scale
    "left": "very good",        # textual label for the lowest score
    "right": "very good",       # textual label for the highest score
    "center":"neutral",         # textual label for a neutral score
    "fomat": "text",            # format of the labels inside each button-- text, emoji, image
    "label_images": {"0": "imagefile", "1": "imagefile", "2": "imagefile"},     # image file path for the images to be displayed if "image" format is selected 
    "custom_emoji_format": {"0": "😎", "1": "🤓", "2": "😊"}                   # emojis to be displayed if "emoji" format is selected
    "fontstyle": "Arial, Helvetica, sans-serif",    # font style for texts in the scale
    "no_of_scales":5,           # number of instances of the scales you wish to create with the same settings
    "user":"no",                # assign "yes" when the inputs are coming through an end user
    "allow_resp":"yes",         # set "no" when you wish to disable the scale at any position
    "show_total_score":"yes",   # decides if the repsondent should be able to see the total score after they have provided a response for all the instances
}
```
2. scale type = npslite, type = settings
```python
{  
    "api_key":<str: your-api-access-key>,
    "username": <str: username>,# your username
    "orientation": "horizontal",# orientation of the scale-- "horizontal"/"vertical"  
    "scalecolor": "#CCCCCC",    # scale background color
    "roundcolor": "#938585",    # colour of the buttons in the scale
    "fontcolor": "#000000",     # colour of the fonts
    "fontstyle": "Arial, Helvetica, sans-serif",    # font style for texts in the scale
    "fomat": "text",            # format of the labels inside each button-- text, emoji
    "custom_emoji_format": {"0": "😎", "1": "🤓", "2": "😊"}     # emojis to be displayed if "emoji" format is selected
    "time": 60,                 # time (in seconds) within which the respondent should provide an answer. Set "00" to disable time restrictions
    "name": "My first scale",   # unique name identifier for the scale
    "left": "very good",        # textual label for the lowest score
    "right": "very good",       # textual label for the highest score
    "center":"neutral",         # textual label for a neutral score
    "no_of_scales": 5           # number of instances of the scales you wish to create with the same settings
    "user":"no",                # assign "yes" when the inputs are coming through an end user
    }
```
3. scale type = stapel, type = settings
```python
{
    "api_key":<str: your-api-access-key>,
    "username": <str: username>,# your username
    "orientation": "horizontal",# orientation of the scale-- "horizontal"/"vertical"
    "spacing_unit": 3,          # intervals between two score values. Can be an integer between 1 and 5
    "scale_upper_limit": 10,    #highest score value in the scale
    "scalecolor": "#CCCCCC",    # scale background color
    "roundcolor": "#938585",    # colour of the buttons in the scale
    "fontcolor": "#000000",     # colour of the fonts
    "fomat": "text",            # format of the labels inside each button-- text, emoji, image    
    "label_images": {"0": "imagefile", "1": "imagefile", "2": "imagefile"},     # image file path for the images to be displayed if "image" format is selected
    "custom_emoji_format": {"0": "😎", "1": "🤓", "2": "😊"}                  # emojis to be displayed if "emoji" format is selected
    "time": "60",               # time (in seconds) within which the respondent should provide an answer. Set "00" to disable time restrictions
    "name": "scalename",        # unique name identifier for the scale
    "left": "very good",        # textual label for the lowest score
    "right": "very good",       # textual label for the highest score
    "fontstyle": "Arial, Helvetica, sans-serif",    # font style for texts in the scale
    "no_of_scales": 5           # number of instances of the scales you wish to create with the same settings
}
```
4. scale type = likert, type = settings
```python
{
    "api_key":<str: your-api-access-key>,    
    "username" : <str: username,# your username
    "scale_name" : "test_scale",# unique name identifier for the scale
    "number_of_scales" : 5,     # number of instances of the scales you wish to create with the same settings
    "orientation" : "vertical", # orientation of the scale-- "horizontal"/"vertical"
    "font_color" : "#4a4a4a",   # colour of the fonts
    "round_color" : "fffff",    # colour of the buttons in the scale
    "fomat" : "text",           # format of the labels inside each button-- text, emoji, image
    "label_scale_selection" : 2,#sub type of the likert scale-- 2 point, 3 point, 4 point, 5 point, 7 point, 9 point
    "label_scale_input" : ["Agree", "Disagree"],    #textual labels for each button. Labels should be as many as the "label_scale_selection" value
    "time" : 100                # time (in seconds) within which the respondent should provide an answer. Set "00" to disable time restrictions
}
```
5. scale type = percent_sum, type = settings
```python
{
    "api_key":<str: your-api-access-key>,    
    "username" : <str: username,# your username
    "time" : "00",              # time (in seconds) within which the respondent should provide an answer. Set "00" to disable time restrictions
    "scale_name" : "envue 2 scale",# unique name identifier for the scale
    "number_of_scales" : 10,    # number of instances of the scales you wish to create with the same settings
    "orientation" : "vertical", # orientation of the scale-- "horizontal"/"vertical"
    "scale_color" : "ffff",     # scale background color
    "product_count" : 3,        # total number of products you wish to rate
    "product_names" : ["brand2", "brand4", "brand5"],   #name of each product
    "user":"no",                # assign "yes" when the inputs are coming through an end user
}
```
6. scale type = percent, type = settings
```python
{   
    "api_key":<str: your-api-access-key>,    
    "username" : <str: username,# your username
    "orientation": "horizontal",# orientation of the scale-- "horizontal"/"vertical"
    "scalecolor": "#1beb00",    # scale background color
    "time": 33,                 # time (in seconds) within which the respondent should provide an answer. Set "00" to disable time restrictions
    "number_of_scales": "99",   # number of instances of the scales you wish to create with the same settings
    "name": "Name",             # unique name identifier for the scale
    "product_count" : 3,        # total number of products you wish to rate
    "product_names" : ["brand2", "brand4", "brand5"],   #name of each product
}
```
### 2. Customize an existing scale

If you ever wish to customize a scale that was already created you can do it by updating the settings parameters.

```python
REQUEST METHOD : PUT
type = settings
```
The request body and an example for scale customization are mentioned in the [API Documentation](https://documenter.getpostman.com/view/24860974/2s9XxsVwUY) 

### 3. Collecting score/ rating for a scale

Now that you have created and customized a scale the last step would be to send responses (ratings) to the scale. 
```python
REQUEST METHOD : POST
type = response
``` 
The request body and an example for creating responses for an existing scale are mentioned in the [API Documentation](https://documenter.getpostman.com/view/24860974/2s9XxsVwUY)

### 4. Retrieve Scale Information 

The LivingLab Scales API also supports ```GET``` requests for fetching scale information from our cloud database. You can use ```GET``` requests to retrieve details of existing statistical scales, including their configurations, response data, and other relevant information.

Examples of this can be found in the [API Documentation](https://documenter.getpostman.com/view/24860974/2s9XxsVwUY)


## Error Handling

The API follows standard HTTP status codes to indicate the success or failure of each request. If an error occurs, you will receive an appropriate status code along with a descriptive error message. Please refer to the [API Documentation](https://documenter.getpostman.com/view/24860974/2s9XxsVwUY) for detailed information on error handling and common error codes.

## Data Privacy and Security

At LivingLab Scales, we prioritize the security and privacy of your data. All API requests and responses are transmitted over secure HTTPS connections to protect your information. We do not share your data with third parties, and we adhere to strict data protection policies to ensure the confidentiality and integrity of your data.


If you have any further questions or need assistance, please don't hesitate to contact our support team. We are here to help you make the most of the LivingLab Scales API.

---

We hope this documentation provides you with the necessary information to get started with the LivingLab Scales API. If you have any feedback or suggestions, please let us know. We are committed to continuously improving our API to meet your needs and deliver a seamless experience.
