## Pixelfy automation

### Purpose
The purpose of this document to is to how to configure and monitor the amazon products for pixelfy tracking links.

### How does the automation works?
The automation works by,
1. <b>Reading the configuration from google sheets</b>
2. Login to pixelfy website
3. Iterate through each products in configuration
4. For every configuration:
    1. Read the configuration details
    2. Open the specific <i>edit tracking link</i> page
    3. Remove the existing tracking links
    4. Add the new tracking links extracted from Google sheets
    5. Save the added tracking links
    6. Extract the pixelfy tracking link
    7. Open in browser and check if it redirects to amazon website
    8. Update the status in configuration sheet
5. close/log out from the website

### How do I add a new product in the configuration?
1. The configuration file is a Google sheet that contains which products are added to pixelfy tracking. The location of the configuration file is sensible information and is available [here](https://github.com/gtotradingpartners/automation-scripts/blob/master/docs/configuration_details.md). In the table, search for `pixelfy configuration` name
<br><b>Note:</b> Only people who have credentials can access the link  
2. Open the config file, and you will already see a list of products (atleast one) added
3. In an empty row (after the last product), Add your configuration. The configuration file have below columns: This is a one time setup for any new products
    1. <b><i>Sl.No:</i></b> A serial number for just self verification in the sheet
    1. <b><i>Product name:</i></b> The product for which you have to update the tracking links
    1. <b><i>File key:</i></b> Usually the list of urls to update will be available in another google sheet. So, specify the file key of the Google sheet. <br>
   <i>Example:</i> For google sheet: https://docs.google.com/spreadsheets/d/123456789/edit#gid=42 <i>123456789</i> is the file key
    1. <b><i>Sheet id:</i></b> Usually the list of urls to update will be available in another google sheet. So, specify the sheet id of the Google sheet. <br>
   <i>Example:</i> For google sheet: https://docs.google.com/spreadsheets/d/123456789/edit#gid=42 <i>42</i> is the sheet id
   <br>The Google sheet you usually use will be in format https://docs.google.com/spreadsheets/d/<<file_key>>/edit#gid=<<sheet_id>>
    1. <b><i>Tracking link:</i></b> The tracking link id of the product. The tracking link will be available when you log in [pixely website](https://app.pixelfy.me/) and select the tracking link you want. You will find it in the url as https://app.pixelfy.me/edit-tracking-links?trlinkID=<<tracking_link_id>>. An example is provided in the configuration file comment already.
    1. <b><i>Status: (Do not edit)</i></b> The status of the script run which will be automatically updated by script. Currently, there are 2 status (`Success`, `Error`)
    1. <b><i>Last updated: (Do not edit)</i></b> The script automatically updates the sheet, and it records the last updated time in format `day-month-year Hour:minutes`
    1. <b><i>Comments: (Do not edit)</i></b> The script provides status about the script execution periodically. The script runs every 15 minutes once.
4. save the file
5. Please do not disturb other configurations
6. If every thing is fine, you will the automatic update on column `Status`, `Last updated` and `Comments`


### FAQS

#### 1. How is this script running?
This script is running in a dedicated server through a scheduler

#### 2. Is there a frequency in which this happens?
Yes, Normally the script runs every 15 minutes once. But if the links provided in the input sheet is same as the one already available in the website, then the script only checks if the current link is still valid.

#### 3. What happens, If the column Status shows `Error`?
Mostly, it should be because of below reasons:
1. <i>Wrong configuration : </i> Please check your configuration, and the url lists you configured once
2. <i>Pixelfy website : </i> Check if everything is fine with the website
3. <i>Comments column : </i> Check the `comments` column to see if there is any extra information is available

#### 4. What happens, If the `last updated` column never got updated?
This will not happen usually. If this happened, then the automation is not running or some problem with the scheduling or server. This should be checked by the developer.
