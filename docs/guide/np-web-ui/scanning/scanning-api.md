# Scanning an API

To scan an API –
1. Use either an Open API specification (Swagger) or a Postman collection – `*.yml` / `*.yaml` / `*.json` (see [supported versions](#supported-versions)).
To do so, select **Open API** in the **Discovery Type** field, as shown below –\
![Scan-API](media/scan-api-1.png ':size=45%')
2. Select whether to scan an **Open API specification** or a **Postman collection**.
3. Fill in the required extra headers for your scan. To add more than one, use the ![Plus-Button](media\plus-button.png ':size=3%') button on the right. If you selected to scan a Postman collection, then you have the option to add the relevant variables.\
![Scan-API-2](media/scan-api-2.png ':size=45%')
4. Select the file to scan. You can either upload a file from your computer by clicking ![Clip-Button](media/clip-button.png ':size=4%') and then filling in the textbox to the left, or import a file from a link by clicking ![Link-Button](media/link-button.png ':size=4%') and then pasting a link in the textbox to the left.\
![Scan-API-3](media/scan-api-3.png ':size=45%')

## Supported versions
| **Schema** | **Supported Versions** |
| :--------: |:----------------------:|
| Swagger    | 2+                     |
| OpenAPI    | 3+                     |
| Postman    | 2+                     |