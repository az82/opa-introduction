# OPA APIs

## Data API

This is the API you should use.

### Example Request

```http
POST /v1/data/opa/examples/allow_request HTTP/1.1
Content-Type: application/json
```

```json
{
  "input": {
    "example": {
      "flag": true
    }
  }
}
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "result": true
}
```

## Query API

This API is for use if OPA has to satisfy a predefined request format.

OPA serves POST requests without a URL path by querying for the document at path `/data/system/main`. The content of that document defines the response entirely.

### Example Request

```http
POST /
Content-Type: application/json
```

```json
{
  "user": ["alice"]
}
```

### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
"hello, alice"
```

## Management APIs

- **Policy API**: CRUD endpoints for managing policy modules
- **Bundle Service API**: Defines an endpoint where OPA can periodically download bundles of policy and data from a remote HTTP server
- **Decision Log Service API**: Defines an endpoint where OPA can report decision logs to
- **Status API**: Defines an endpoint where OPA can report status to
- **Monitoring**: OPA by default exposes a Prometheus endpoint
- **Discovery Service API**: Defines an endpoint where OPA can download a bundle that controls the other management APIs

## Advanced

- **Compile API**: Partially Evaluate a Query

## REPL

For developing policies

```bash
./opa run
```
