# Cloud Service

## Azure

- Azure ACI Private Image Deploy Failure
  - Add `docker.io/` prefix to the `Image`

- Azure App Service Bind Port
  - Settings >> Environment variables >> WEBSITES_PORT: `<port>`

## Google Cloud

- Vertex AI API `403 PERMISSION_DENIED`
  - IAM >> Allow >> Grant access >> New principals: `vertex-express@<project_id>.iam.gserviceaccount.com`; Assign roles: `Vertex AI Platform Express User (Beta)`