# packaging-server

The `packaging-server` repository uses quilt-rs to provide an OpenAPI-compatible REST API for creating and managing packages, then publishes that as a public Docker image you can run:

- on your local machine
- in your private cloud
- as part of your SaaS application
- etc.

## Fargate CDK Deployment

While you can run the Docker container anywhere, for production use we recommed deploying it to AWS Fargate using the included CDK script.

## OpenAPI REST API

The `packaging-server` REST API is documented by and compatible with OpenAPI. You can view the API documentation by running the server and visiting the `/docs` endpoint.

### Resources

The primary resources are:

- `packages` for creating and managing packages
  - Format: packages/s3/"bucket"/"prefix"
- `objects` for managing S3 objects
  - Format: objects/s3/"bucket"[/"prefix"]
- `hashes` for retrieving the hash of an S3 object
  - Format: hashes/s3/"bucket"/"prefix"[/]
- `events` for events that trigger package-creation
  - Format: events/s3/"bucket"/"prefix"
- `alerts` for sending SNS notifications when packages are created
  - Format: alerts/s3/"bucket"/"prefix"
  
### Verbs

These are the HTTP verbs used by the API:

- GET: Retrieve information about the collection, or individual resources
- POST: Create a new resource (error if already exists)
- PATCH: Update an existing resource (error if does not exist)
- PUT: Create or update a resource (always succeeds)

## Web Interface

In addition to the REST API, `packaging-server` also provides a simple web interface for humans to manually interact with those resources.
