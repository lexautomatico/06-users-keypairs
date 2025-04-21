# Security To-Do for Users Keypairs

## Environment Variables Setup

This file outlines the environment variables that need to be set up for secure deployment of the Users Keypairs application.

### Required Environment Variables

The following environment variables should be configured:

- **VITE_ALCHEMY_ID**: API key for Alchemy blockchain development platform
- **VITE_WALLETCONNECT_PROJECT_ID**: Project ID for WalletConnect integration

### Implementation Steps

1. Create a `.env` file in the project root with the following template:
   ```
   VITE_ALCHEMY_ID=your_alchemy_api_key_here
   VITE_WALLETCONNECT_PROJECT_ID=your_walletconnect_project_id_here
   ```

2. Update your code in src/App.tsx, src/AppMod.tsx, and src/AppMod2.tsx to use these environment variables:
   ```typescript
   // Replace hardcoded values like:
   const alchemyId = "LGrHZsmYREYuc2mHcQKQShIRUuNIXqH9";
   const walletConnectProjectId = "8cafecf4df9c83503b82e35f86f56dfb";
   
   // With environment variables:
   const alchemyId = import.meta.env.VITE_ALCHEMY_ID;
   const walletConnectProjectId = import.meta.env.VITE_WALLETCONNECT_PROJECT_ID;
   ```

3. Ensure the `.env` file is added to `.gitignore` to prevent committing secrets:
   ```
   # .gitignore
   .env
   .env.local
   .env.development
   .env.production
   ```

4. For production deployment, set these environment variables in Vercel:
   - Go to your project in the Vercel dashboard
   - Navigate to Settings → Environment Variables
   - Add the variables VITE_ALCHEMY_ID and VITE_WALLETCONNECT_PROJECT_ID with their respective values
   - Redeploy your application

### Additional Steps for This Project

1. **Rotate API Keys Immediately**:
   - Generate a new Alchemy API key to replace `LGrHZsmYREYuc2mHcQKQShIRUuNIXqH9`
   - Generate a new WalletConnect Project ID to replace `8cafecf4df9c83503b82e35f86f56dfb`
   - The existing keys should be considered compromised

2. **Check All Files**:
   - The credentials were found in:
     - `.env`
     - `src/App.tsx` (line 24-25)
     - `src/AppMod.tsx` (line 15-16)
     - `src/AppMod2.tsx` (line 16-17)
   - Make sure to update all instances

3. **TypeScript Support**:
   - Update your `vite-env.d.ts` to include type definitions for the environment variables:
   ```typescript
   /// <reference types="vite/client" />
   interface ImportMetaEnv {
     readonly VITE_ALCHEMY_ID: string;
     readonly VITE_WALLETCONNECT_PROJECT_ID: string;
   }
   
   interface ImportMeta {
     readonly env: ImportMetaEnv;
   }
   ```

### Security Best Practices

- Never commit sensitive credentials to version control
- Rotate API keys periodically and after suspected exposure
- Use different API keys for development and production
- Implement proper access controls for all services
- Consider using a secrets management service for production