# Currency Exchange API – NodeJS

docker run -d -p 8080:8080 u1ih/nodejs-api

At the terminal, type in the following codes
`curl -i http://localhost:8080/fx`

<p>Everything below here, I understand in theory but not practical.</p>

<hr>

## 1. Creating a project on GCP

1. I went to GCP console and created a new project.
2. Make sure to enable *Google Cloud Build API* and *Artifact Registry API* .
3. Go to Uli's github to fork the repo. Get the [link](https://github.com/jlchiam/nodejs-api.git)
4. Return to GCP terminal and create the docker container.

    `docker run -d -p 8080:8080 u1ih/nodejs-api`

6. Push the container to artifact registry.
7. 



CI/CD pipeline implemented using GitHub Actions:

* create docker container
* push to gcr.io container registry
* deploy to Google Cloud Run (knative / PaaS)

Live endpoint available at: [https://nodejsapi-tgihgzgplq-uc.a.run.app/](https://nodejsapi-tgihgzgplq-uc.a.run.app/)

[https://nodejsapi-tgihgzgplq-uc.a.run.app/fx](https://nodejsapi-tgihgzgplq-uc.a.run.app/fx)


The CI/CD build workflow needs documentation. For now, here is how you connect it to GCP: [https://gcp-examquestions.com/ci-cd-solutions-deploy-to-google-cloud-run-using-github-actions/](https://gcp-examquestions.com/ci-cd-solutions-deploy-to-google-cloud-run-using-github-actions/)

In order for this to be provisioned on your Google Cloud instance, you need to make sure you create/update these GitHub secrets:

* GCP_APPLICATION
* GCP_CREDENTIALS
* GCP_EMAIL
* GCP_PROJECT

You'll also need to activate a couple of APIs in Google Cloud, the first deployment will probably fail and point you into the right direction. Alternatively, you could deploy the first version manually.
