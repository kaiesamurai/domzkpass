## DomZKPass Dapp Connector

This application facilitates users in generating zero-knowledge proofs (using [zkPass](https://zkpass.org/) or [Reclaim protocol](https://reclaimprotocol.org/)) from external websites. These proofs are then securely sent to the user’s Verida Wallet using the Verida inbox messaging system.

## Use Case Examples
- Verify trading volume exceeding limits on Binance
- Confirm ownership of a Discord account
- Validate the existence of an Uber account
- Authenticate credentials from zkPass and Reclaim protocol

## Setup
### Setting up zkPass Account
- Follow the [quick start guide](https://zkpass.gitbook.io/zkpass/developer-guides/quick-start) for creating a zkPass account.
- Create a new application and register required [schemas](https://zkpass.gitbook.io/zkpass/developer-guides/schema).
- Obtain `APP_ID` and update `NEXT_PUBLIC_ZKPASS_APP_ID` in the .env file located at `src/config/providers.ts`.

### Setting up Reclaim Account
- Visit https://dev.reclaimprotocol.org/dashboard.
- Create a new app and register necessary providers.
- Update provider data in `src/config/providers.ts` and set `NEXT_PUBLIC_RECLAIM_APP_ID` and `RECLAIM_SECRET_KEY` in the .env file.

### Adding PRIVATE_KEY for Verida Messaging
- Update `PRIVATE_KEY` in the .env file to enable sending messages via the Verida messaging system.

### Adding VERIDA_SEED for Verida Messaging
- Obtain `VERIDA_SEED` from Verida Wallet and update it in the .env file.

## Running the Application
```bash
yarn install
yarn build
yarn start
```
- Visit http://localhost:3000/add-credential?schemaId=[schemaId]&veridaDid=[veridaDid]
- Visit http://localhost:3000/add-credential?veridaDid=[veridaDid]

## Verifying Credentials from zkPass and Reclaim Protocol
- Navigate to http://localhost:3000/verify
- Connect to your Verida Wallet and click `Request credential`.

### How It Works
The system initiates a data request to the connected wallet's inbox. Once the user provides their credentials, the backend system verifies their validity based on credential types such as zkPass or Reclaim.

## Deployment
Deployment is handled via AWS Amplify. Ensure all environment variables are configured in the Amplify console and added to amplify.yml for server-side rendering.

Example:
```yaml
    commands:
      - env | grep -e NEXT_PUBLIC_ZKPASS_APP_ID -e PRIVATE_KEY -e NEXT_PUBLIC_RECLAIM_APP_ID -e RECLAIM_SECRET_KEY -e VERIDA_SEED >> .env
```

For more details, refer to the [AWS Amplify SSR Environment Variables Guide](https://docs.aws.amazon.com/amplify/latest/userguide/ssr-environment-variables.html).
