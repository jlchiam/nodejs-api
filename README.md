# Currency Exchange API – NodeJS

docker run -d -p 8080:8080 u1ih/nodejs-api

At the terminal, type in the following codes
`curl -i http://localhost:8080/fx`

<p>Everything below here, I understand in theory but not practical.</p>

<hr>

## 1. Creating a project on GCP

1. I went to GCP console and created a new project.
2. Make sure to enable *Google Cloud Build API* .
3. Go to Uli's github to fork the repo. Get the link [https://github.com/jlchiam/nodejs-api.git](https://github.com/jlchiam/nodejs-api.git)
4. change directory to the nodejs-api directory

    `cd nodejs-api`

6. Return to GCP terminal, build the container

    `docker build . -t mynodejs-api`

7. Run Container

    `docker run -d -p 8080:8080 mynodejs-api`

8. Connect Cloud Build to Github Repo
9. Create a Trigger, push event, configuration choose Dockerfile
10. Make changes to the codes
11. At terminal, go back to the root directory of the repo. In this case is `jchiamrp/nodejs-api`
12. Use the following commands to commit and push.
    `git add --all
    git commit -m "some message"
    git push`

13. Verify in Cloud Build History

    <img width="595" alt="200 nodejs cloudbuild history" src="https://user-images.githubusercontent.com/11884697/159163111-62f07e85-0bbb-4fc0-ba38-45d6df46bb36.PNG">

14. At Github actions page, create a new workflow -> set up a workflow yourself -> main.yml

15. At Github settings page, create the following environment secrets 
    [link1 - broken images](https://gcp-examquestions.com/ci-cd-solutions-deploy-to-google-cloud-run-using-github-actions/?msclkid=9a048adda84f11ec8e68694d01d9ee84)
    [link2](https://towardsdatascience.com/deploy-to-google-cloud-run-using-github-actions-590ecf957af0)

    GCP_APPLICATION — Your Google service account application name for your Cloud Run service.
    GCP_CREDENTIALS — This is your service account credentials that you will need to generate in the Google Cloud Console. You downloaded these in step one. Copy the contents of the JSON file you created, provide that as a value to this secret, and delete that file.
    GCP_EMAIL — This is the email that identifies the service account that you have provided credentials for in the secret labeled GCP_CREDENTIALS.
    GCP_PROJECT — Your Google Project that you will deploying to Cloud Run.

    <img width="596" alt="250_github env secrets" src="https://user-images.githubusercontent.com/11884697/159164425-0cc9b89d-2f9d-418e-8111-3fe44c09695a.PNG">

16. End outcome still fail, no time to troubleshoot :(

<hr />

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
