# Reporting API: Overview

## API Usage

The api has one main endpoint `/report` and accepts both post and get requests. A post request is used to create a report job. A get request is used to retrieve a report from the Performix reporting tool.



~ Note
Usage of the API is authorized by using a bearer token. Please contact Biometix for a valid auth token.
~


### Creating a report job

The Performix reporting tool is designed to be stateless. Therefore all data and associated specification files must be provided in the form-data of the post request.

The reporting tool requires:

- a blueprint yaml file that specifies the analyses to be performed.
- a template file that specifies the format of the report as a word docx document.
- one or more data files in csv format.

For further information on how to set up the blueprint and template files please see the [Blueprint Specification](blueprint-specification) document.

A post to `/report` accepts a multipart/form-data content type with 3 named keys:

- blueprint - for the yaml blueprint configuration file.
- termplate - for the docx template file.
- data - for csv data files

If there is a problem with creating the job, such as incorrect file types, the post request will return an error messages. Otherwise if the job creation is successful a job id will be returned.

### Getting a report

To retrieve the report from the Performix Reporting tool a get request is used on the `/report` endpoint. This get request must have the id of the report being retrieved given as a url argument.

If the report job is incomplete the status of the job is returned. If the report job is done then the report document is returned.

### Swagger Usage

Accessing `/swagger` endpoint of the Performix API within a browser opens the swagger interface that provides an interactive GUI that can be used to trigger the reporting API. Swagger provides an online form to fill in with the required parameters for posting and getting a report along with an authorize button to set up the authentication bearer token.

On the deployed version of Performix this url can be accessed via `http://performix.biometix.com/api/report/swagger/`

