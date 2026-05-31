# Swagger (OpenAPI) Changelog

## [Unreleased] - 2026-05-31
### Added
- Added OAuth authorization server metadata discovery, including advertised token/introspection endpoints, supported `private_key_jwt` authentication methods, supported assertion signing algorithms, and JWKS location.
- Added a JWKS discovery endpoint for PCM issuer public keys.
- Added `private_key_jwt` client authentication support for `/introspect`, in addition to bearer-token caller authentication.
- Added explicit RFC 8707 resource-indicator behavior for token issuance, including one access token per resource server and `invalid_target` for requests with multiple resource targets.
- Added HealthcareService flows for registering against an existing catalog service and requesting a new service when no suitable catalog entry exists.
- Added pending catalog and pending provider-instance examples for new-service registration responses.
- Added OperationOutcome examples for catalog update requests that are accepted for asynchronous processing or rejected because they require a new-service registration.
- Added documented HEAD checks for resource existence across the supported FHIR resources.
- Added `patient:identifier` as a documented Consent search parameter.

### Changed
- Clarified that mTLS is a transport-level requirement while OAuth2 client authentication uses `private_key_jwt`; mTLS certificate evidence may be linked through `cnf` policy but is not advertised as the OAuth client authentication method.
- Updated token and introspection examples to use ES384-style client assertions and to distinguish PCM management tokens from data-source access tokens.
- Clarified introspection response semantics, including HealthcareService instance context, data-source audience values, and certificate confirmation evidence.
- Reframed service governance around HealthcareService lifecycle state and OperationOutcome responses instead of public approval resources.
- Clarified HealthcareService search visibility for active and inactive catalog/instance services, including authorization limits for inactive records.
- Reworked HealthcareService creation so providers either submit a minimal instance registration with `basedOn` for an existing catalog service, or submit a full new-service request that creates pending catalog and instance resources.
- Clarified that external clients do not directly create immediately active canonical catalog services; activation and review happen outside the public FHIR operation.
- Clarified HealthcareService update behavior for instance deactivation, reactivation requests, asynchronous catalog updates, and material catalog changes that must go through the new-service flow.
- Clarified Consent creation rules so consent requests must reference an existing active HealthcareService instance, not a catalog service or inactive instance, and token issuance repeats the service-state check.
- Updated submit examples to show server-accepted request payloads without client-supplied `meta.profile` where profiles are illustrative rather than sent on the wire.
- Normalized the patient bucket-change extension URL to `ext-allow-patient-bucket-change`.
- Refreshed the CapabilityStatement, FHIR examples, and generated Redocly documentation to match the current public API behavior.

### Removed
- Removed public VerificationResult approval endpoints and examples.

## [Unreleased] - 2026-01-28
### Added
- Split OpenAPI specs into `openapi-fhir.yaml` and `openapi-oauth.yaml`, with a combined `openapi.yaml`.

### Changed
- OpenAPI documentation refreshed.
