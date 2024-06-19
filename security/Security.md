# Security

## Overview

Security in application development involves ensuring that data and resources are protected from unauthorized access and misuse. This includes implementing protocols and mechanisms for identification, authentication, authorization, and data integrity.

## OAuth 2

OAuth 2 is an authorization framework that enables applications to obtain limited access to user accounts on an HTTP service, such as Facebook, GitHub, or Google. It works by delegating user authentication to the service that hosts the user account and authorizing third-party applications to access the user account. OAuth 2 uses several components:

- **Resource Owner:** Typically the end-user who owns the data.

- **Resource Server:** The server hosting the user data.

- **Client:** The application requesting access to the user's account.

- **Authorization Server:** The server issuing access tokens to the client after successfully authenticating the resource owner and obtaining authorization.

### Protocol Flow

1. The client requests authorization from the resource owner.
2. The client receives an authorization grant, which is a credential representing the resource owner's authorization.
3. The client requests an access token by presenting the authorization grant to the authorization server.
4. The authorization server authenticates the client, validates the authorization grant, and issues an access token.

### Grants

OAuth 2 supports several types of grants for different scenarios:

- **Authorization Code:** Used with server-side applications where the client can securely store the client secret.

- **Client Credentials:** Used for application API access where the client is also the resource owner.

- **Device Code:** Used for devices that lack a browser or have limited input capability.

- **Implicit:** Was previously used for clients implemented in a browser using a scripting language but is less recommended due to security concerns.

- **Password:** Used when the application has a high degree of trust with the user but is generally not recommended due to security risks.

### Tokens

Tokens in OAuth 2 are essential components used to secure communication between clients and resource servers by proving an identity or permission set. These are issued by the authorization server and come in two main forms:

- **Access Token:** The token that applications use to make API requests on behalf of the user.

- **Refresh Token:** Used to obtain a new access token when the current access token expires without requiring the user to re-authenticate.

## JSON Web Token (JWT)

JWT is a compact, URL-safe means of representing claims to be transferred between two parties. It is often used in OAuth 2.0 and OpenID Connect (OIDC) as a way to convey the identity of the authenticated party.

- **Debugging:** [jwt.io](https://jwt.io)

### Structure

A JWT is structured into three parts:

- **Header:** Contains metadata about the token such as the type of token and the hashing algorithm used.

- **Payload:** Contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims: registered, public, and private.

- **Signature:** Used to verify that the sender of the JWT is who it says it is and to ensure that the message wasn't changed.

## Keycloak

Keycloak is an open-source Identity and Access Management solution aimed at modern applications and services.

### Key Concepts

- **Users:** Entities typically representing individuals or services that can access applications.

- **Roles:** Collections of permissions that can be assigned to users or other entities in Keycloak.

- **Realms:** The primary partition in Keycloak, which typically corresponds to one organization. It contains users, credentials, roles, and groups. A master realm is created by default.

- **Clients:** Entities that can request Keycloak to authenticate a user. Most often, clients are applications that want to secure with Keycloak.

- **Access Token:** Tokens that are granted to clients after successful user authentication, which the client uses to prove their identity to other services.
