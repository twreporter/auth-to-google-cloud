# auth-to-google-cloud

This GitHub Action authenticates to Google Cloud via [Workload Identity Federation](https://cloud.google.com/iam/docs/workload-identity-federation), which is the recommended approach as it obviates the need to export a long-lived Google Cloud service account key and uses short-lived access tokens instead. The short-lived access token is only valid for a single job, then automatically expires.

With short-lived access tokens, applications can impersonate the service account and access GCP Services like Compute Engine, Cloud Storage...etc, which the service account has the permission to access to.

GitHub's OpenID Connect(OIDC) provider allows the workflows to exchange short-lived access tokens directly from cloud provider, Google Cloud Platform.
For more information about how GitHub's OIDC provider integrates with workflows and cloud provider, please refer to the [overview diagram](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect#getting-started-with-oidc).

The main idea about authenticating with workload identity federation can be described as below:
1. Create a Google Cloud service account and grant IAM permissions
2. Create and configure a Workload Identity Provider for GitHub on Google Cloud Platform
3. Exchange the GitHub Actions OIDC token for a short-lived Google Cloud access token

This repo only focus on the third part, to configure the others, please follow the [setup instructions](https://github.com/google-github-actions/auth#setting-up-workload-identity-federation).

After running `google-github-actions/setup-gcloud@v0` in the workflow, the short-lived access token is exported as `GOOGLE_APPLICATION_CREDENTIALS` and can be utilized in the applications directly. 
