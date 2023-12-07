# # brave-apis-sandbox-java-client

Brave APIs

- API version: 1.0.0
  - Build date: 2023-11-05

**Brave Data Events Sandbox API**

Brave Data Events is an API that simulates event logging from mobile devices and web applications for analytical data processing. The client can track the status of the data with the corresponding ID via GET endpoint.

**Brave Data Insights Sandbox API**

Brave Data Insights is an API that delivers real-time insights for better risk and fraud decisions. Our API can obtains one or more insights based on data collected from the user's mobile devices or web applications.

<img src='https://developer.circulodecredito.com.mx/sites/default/files/2020-10/circulo_de_credito-apihub.png' height='40' width='220'/>

## Requirements

Building the API client library requires:

1. Java 1.7+
2. Maven/Gradle

## Installation

**Prerequisite**: get access token and access credential settings. Consult the manual **[here](https://github.com/APIHub-CdC/maven-github-packages)**.

To install the API client library to your local Maven repository, simply execute:

```shell
mvn clean install -Dmaven.test.skip=true
```

> **NOTA:** Este fragmento del comando *-Dmaven.test.skip=true* evitará que se lancen las pruebas unitarias.

## Getting Started

### Step 1. Generate key and certificate

Before launching the test, you must have a keystore for the private key and the certificate associated with it. To generate the keystore, execute the instructions found in ***src/main/security/createKeystore.sh*** 

### Step 2. Uploading the certificate within the developer portal

1. Login to Developer Portal https://developer.circulodecredito.com.mx/
2. Click on the section "**Mi cuenta > Apps**". 
3. Select the application or add application.
4. Go to the tab "**View**" and put the button "**Certificados**"
5. Select and load your certificate (.pem). After, download our certificate in your desktop.

> **Nota:** If you have doubts, please contact to technical team of Circulo de Crédito.

### Step 3. Modify configuration file

To make use of the certificate that was downloaded and the keystore that was created, the routes found in **src/main/resources/config.properties**

```properties
keystore_file=your_path_for_your_keystore/keystore.jks
cdc_cert_file=your_path_for_certificate_of_cdc/cdc_cert.pem
keystore_password=your_super_secure_keystore_password
key_alias=your_alias
key_password=your_super_secure_password
```

### Step 4. Modify URL and request data

In the DatasetsApiTest.java file, found at  ***src/test/java/io/brave/dataevents/client/api/***.  The request and URL data for API consumption must be modified as shown in the following code snippet with the corresponding data:

1. Access credentials given by Círculo de Crédito, obtained after affiliation
   
   - usernameCDC: Círculo de Crédito user
   - passwordCDC: Círculo de Crédito password

2. API consumption data
   
   - url: URL of the API exposure
   - xApiKey: Located in the application (created in ** step 2 **) of the Developer Portal and named as Consumer Key in the section "**Credentials**"

> **NOTE:** The data in the following request are only representative.

```java
/**
 * API tests for DatasetsApi
 */
public class DatasetsApiTest {

    private final DatasetsApi api = new DatasetsApi();

    private Logger logger = LoggerFactory.getLogger(DatasetsApiTest.class.getName());

    private String username = "your_username_otorgante";
    private String password = "your_password_otorgante";

    private String url = "the_base_url_of_api";
    private String xApiKey = "your_x_Api_Key";
```

### Step 5. Run the unit test

Having the previous steps, all that remains is to run the unit test, with the following command:

```shell
mvn test -Dmaven.install.skip=true
```

## Documentation for API Endpoints

All URIs are relative to *https://circulodecredito.apigee.net/sandbox/brave/data-events/v1*

| Class         | Method                                                       | HTTP request                      | Description              |
| ------------- | ------------------------------------------------------------ | --------------------------------- | ------------------------ |
| *DatasetsApi* | [**getDatasetStatus**](docs/DatasetsApi.md#getDatasetStatus) | **GET** /datasets/{dataId}/status | Get dataset information  |
| *DatasetsApi* | [**uploadDataset**](docs/DatasetsApi.md#uploadDataset)       | **POST** /datasets/               | Upload dataset of events |

All URIs are relative to *https://circulodecredito.apigee.net/sandbox/brave/data-insights/v1*

| Class        | Method                                                         | HTTP request                       | Description            |
| ------------ | -------------------------------------------------------------- | ---------------------------------- | ---------------------- |
| *InsightApi* | [**getDatasetInsight**](docs/DatasetsApi.md#getDatasetInsight) | **GET** /datasets/{dataId}/insight | Get insight of dataset |

## Documentation for Models

- [Error](docs/Error.md)
- [Errors](docs/Errors.md)
- [GetDataModel](docs/GetDataModel.md)
- [InlineResponse200](docs/InlineResponse200.md)
- [InlineResponse2001](docs/InlineResponse2001.md)
- [Operation](docs/Operation.md)
- [UploadDataModel](docs/UploadDataModel.md)

## Recommendation

It's recommended to create an instance of `ApiClient` per thread in a multithreaded environment to avoid any potential issues.

## Author

api@circulodecredito.com.mx
