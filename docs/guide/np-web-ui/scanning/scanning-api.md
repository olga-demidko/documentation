# Scanning an API

To scan an API, follow these steps:
1. Select **Open API** in the **Discovery Type** section to use either an Open API specification (Swagger) or a Postman collection – `*.yml` / `*.yaml` / `*.json`.

    >[!NOTE|label:Note]
The supported versions of the API schemas are Swagger 2+, OpenAPI 3+ and Postman 2+.

    ![open-api](media/open-api.png ':size=45%')

2. Select whether to scan an **Open API specification** or a **Postman collection**.
3. Fill in the required extra headers for your scan. To add more than one, use the ![Plus-Button](media\plus-dark.png ':size=3%') button on the right. If you selected to scan a Postman collection, then you have the option to add the relevant variables.

    ![extra-headers](media/extra-headers.png ':size=45%')

4. Select the API schema file to scan. You can either upload a file from your computer by clicking ![Clip-Button](media/clip.png ':size=4%') and then filling in the field to the left, or import a file from a link by clicking ![Link-Button](media/link.png ':size=4%') and then pasting a link in the field to the left.

    ![upload-file](media/upload-file.png ':size=45%')

    Once you have uploaded a schema file, the **Shema Editor** tab appears in the left pane. Use this tab to modify the uploaded schema before running a scan. 

    ![schema-tab](media/schema-editor-tab.png ':size=45%')

## Editing an Uploaded API Schema
To edit the uploaded API schema before running a scan, follow these steps:
1. In the **Schema Editor** tab, select the node with the data you want to edit.

    ![select-endpoint](media/select-endpoint.png ':size=45%')

2. In the **Endpoint data editor** field, make the changes you need and proceed with the [setup](guide/np-web-ui/scanning/creating-new-scan.md).
