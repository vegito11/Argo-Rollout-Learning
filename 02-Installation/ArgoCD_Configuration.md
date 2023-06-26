## Argocd Configuration

###  Configure a new OAuth Client ID
   
   - Go to your Google API Credentials console, and make sure you're in the correct project.
   
   - Click on "+Create Credentials"/"OAuth Client ID"
   
   - Select "Web Application" in the Application Type drop down menu, and enter an identifying name for your app (e.g. Argo CD)

   - Fill `Authorized JavaScript origins` with your Argo CD URL,   
      
      ```bash
      https://myargocd.mydomain.com
      ```

  - Fill `Authorized redirect URIs` with your Argo CD URL plus /api/dex/callback
     
     ```bash
     https://myargocd.mydomain.com/api/dex/callback
     ```
  
  - Values file
     
     ```yaml
     configs:
      cm:
        # -- Argo CD's externally facing base URL (optional). Required when configuring SSO
        url: "https://argocd.mydomain.io"
    
        # Dex configuration
        dex.config: |
          connectors:
            - type: oidc
              id: google
              name: Google
              config:
                issuer: https://accounts.google.com
                clientID: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX.apps.googleusercontent.com
                clientSecret: XXXXX-XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
     ```

-------------------------------------

## Refs:

- [Argocd OIDC config](https://argo-cd.readthedocs.io/en/stable/operator-manual/user-management/google/)