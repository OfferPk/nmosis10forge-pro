# NMOSIS10Forge Pro (v1.0.0)

### AMWA NMOS IS-10 & BCP-003-02 API Security & OAuth 2.0 Authorization Studio

---

## Overview

**NMOSIS10Forge Pro** is a high-precision broadcast engineering workbench and automation utility built for SMPTE ST 2110 IP facility engineers, broadcast security architects, OB van integrators, and equipment manufacturers. It provides OAuth 2.0 token minting, claim construction, RFC 8414 authorization server discovery, RFC 7517 JWKS public key verification, node guard simulation, and 10-point normative compliance verification across:

- **AMWA NMOS IS-10 v1.0.0**: Authorization Specification for NMOS APIs  
- **AMWA BCP-003-02**: Authorization in NMOS Systems (Best Current Practice)  
- **RFC 7519**: JSON Web Tokens (JWT)  
- **RFC 7517**: JSON Web Key Sets (JWKS)  
- **RFC 8414**: OAuth 2.0 Authorization Server Metadata  
- **RFC 6749**: The OAuth 2.0 Authorization Framework  
- **EBU R143 & EBU R148 / JT-NM Tested**: Broadcast Cybersecurity Frameworks

---

## Key Capabilities

1. **NMOS OAuth 2.0 Token Mint**:  
   - Visual and programmatic generation of RFC 7519 JWT Bearer access tokens with standard AMWA claims (`iss`, `sub`, `aud`, `exp`, `nbf`, `iat`, `jti`, `scope`, `x-nmos-auth`).  
2. **Standard NMOS Scope Management**:  
   - Configures fine-grained permission scopes including `registration:write`, `query:read`, `connection:write`, `connection:read`, `events:write`, `channelmapping:write`, and `system:read`.  
3. **Authorization Server Discovery & JWKS Generator**:  
   - Synthesizes compliant RFC 8414 `/.well-known/oauth-authorization-server` metadata and RFC 7517 `/.well-known/jwks.json` key sets.  
   - Outputs RFC 6763 DNS-SD resource records for `_nmos-auth._tcp`.  
4. **Node Guard Simulator & Resource Server Emulator**:  
   - Simulates media node protection pipelines against incoming API calls.  
   - Evaluates signature integrity, temporal validity, audience matching, and scope permissions, returning standard HTTP 200, 401 Unauthorized, or 403 Forbidden responses.  
5. **10-Point Normative Compliance Auditor**:  
   - Automated pass/fail validation covering JWT headers, cryptographic algorithms, key ID bindings, issuer schemes, temporal ordering, and scope formatting.  
6. **Production Python CLI (`is10-cli.py`)**:  
   - Headless CLI for broadcast CI/CD automation, supporting `mint`, `verify`, `metadata`, and `audit` operations.

---

## Getting Started

### Web Studio

Open `source-code/index.html` in any web browser. Runs 100% locally with zero external network or cloud dependencies.

### Command-Line Interface

\# Mint a signed test NMOS Bearer token

python3 build/is10-cli.py mint \\

  \--sub "bcs-controller-01" \\

  \--aud "https\://node-1.prod.tv/x-nmos/connection/v1.1" \\

  \--scopes "connection:write connection:read"

\# Verify a token against a target endpoint

python3 build/is10-cli.py verify \\

  \--token "\<RAW\_TOKEN\>" \\

  \--aud "https\://node-1.prod.tv/x-nmos/connection/v1.1" \\

  \--scope "connection:write"

\# Generate OAuth server metadata and JWKS

python3 build/is10-cli.py metadata \--host "auth.prod.tv"

\# Execute normative security compliance audit

python3 build/is10-cli.py audit

### Automated Testing

python3 test\_is10.py