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

Intended features include:

### Package Management

Formate: packages/<scheme>/<registry>/<package>[/<path>]

- GET: List the contents of the registry, package, or path (depending on the parameters)
- POST: Create a new package with those parameters from an S3 prefix (fails if the package **does** exist)
- PATCH: Update the package with those parameters from an S3 prefix (fails if the package **does not** exist)
- PUT: Create or update the package with those parameters from an S3 prefix (always succeeds)

### Hash Management

Format: hashes/s3/<bucket>/<prefix>[/]

- GET: Return the hash of the object in the S3 bucket with the given prefix
  - also returns size, hash-algorithm, and last-modified
  - return list if prefix ends in / (all if a folder, one if a file)
- POST: Create a new hash for the object in the S3 bucket with the given prefix (if a file)

### Bucket Management

Simple web interface for managing S3 buckets and their contents.

Format: buckets/s3/<bucket>[/<prefix>]

- GET: List the contents of the bucket or prefix (depending on the parameters)
- POST: Create a new object with that name (fails if the object **does** exist)
- PATCH: Update the object with that name (fails if the object **does not** exist)
- PUT: Create or update the object with that name

### Rules for Event Processing

Format: rules/s3/<bucket>/<prefix>

- GET: List the rules for the bucket or prefix (depending on the parameters)
- POST: Create a new rule for the bucket or prefix
- PATCH: Update the rule with the given parameters
- PUT: Create or update the rule with the given parameters (can only have one rule per bucket/prefix)

## Web Interface

In addition to the REST API, `packaging-server` also provides a simple web interface for directly interacting your packages, hashes, and buckets.
