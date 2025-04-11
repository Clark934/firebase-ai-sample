# "Planning with the Gemini API" - a Firebase AI sample app

Welcome to the _Planning with the Gemini API_ sample app, an AI-powered web app
for to-do lists! It's an [Angular](https://angular.io/) app built using the
Gemini API and Firebase.

The [Gemini API](https://ai.google.dev/gemini-api) gives you access to Google's latest
generative AI models – the Gemini family of multimodal models.
This _Planning with the Gemini API_ web app calls the Gemini API to generate a task list
from either text or an image provided by the end user.

The backend of _Planning with the Gemini API_ is powered by
[Firebase](https://firebase.google.com/), which is Google's platform for
building fullstack multi-platform apps. This app uses
[Firebase Authentication](https://firebase.google.com/products/auth) for signing-in
and authorizing end users. It also uses
[Firestore](https://firebase.google.com/products/firestore) – a NoSQL realtime database –
to store the to-do list items.

> [!CAUTION] > **In its DEFAULT state, this sample app is for _EXPERIMENTATION and PROTOTYPING ONLY_.**
> It uses the [Google AI SDK for JavaScript](https://ai.google.dev/gemini-api/docs/quickstart?lang=web)
> directly from the client-side which means that you risk potentially exposing your
> Gemini API key to malicious actors if you deploy this app.
>
> If you want to deploy this sample app or use it as a base for a production app,
> **we strongly recommend that you
> [migrate to use the Vertex AI in Firebase SDK](https://github.com/FirebaseExtended/make-it-so-angular/main/README.md#migrate-to-use-vertex-ai-in-firebase),
> which offers security options against unauthorized clients.**

## Explore the app's codebase

- In `src/environments/environments.ts`, you can find important configuration values:

  - Within `firebase`, find the values needed to connect your app to Firebase
    (most importantly `apiKey`, `projectId`, and `appId`).
  - Find your Gemini API key (`gemini_api_key`).

  Note that if you
  [run the sample app in IDX](https://github.com/FirebaseExtended/make-it-so-angular/main/README.md#set-up-and-run-the-app),
  then these config values will be automatically populated into the file for you.

- In `src/app/services/task.service.ts`, you can explore how to make a basic call to
  the Gemini API, including:

  - Importing the Google AI package: `google/generative-ai`.
  - Initializing the Google AI service and the generative model.
  - Calling `generateContent` to send the request to Gemini with the provided prompt
    (and image, if provided).

- In `src/app/app.config.ts` and `src/app/services/task.service.ts`, you can explore
  how to use Firebase, including:

  - Using Firebase Authentication's
    [anonymous authentication method](https://firebase.google.com/docs/auth/web/anonymous-auth)
    to create an authenticated user account.
  - Using Firestore to write and read to-do tasks and subtasks generated by Gemini.

## Set up and run the app

You can either run the sample app in IDX (recommended) or locally.

### Option 1: Run in IDX _(recommended)_

This _Planning with the Gemini API_ web app is best experienced by running it in
[IDX](https://idx.dev/), which is Google's browser-based workspace for
building, shipping, and managing full-stack multiplatform apps.

Firebase provides a custom workflow using IDX to help you quickly experiment with the sample app.
This workflow automatically sets up a new Firebase project with Authentication and Firestore
enabled, opens the sample app in IDX, and sets up the app to use Firebase and the Gemini API.
The project and app are yours to experiment with and explore how Gemini works.

[GET STARTED WITH THE SAMPLE APP IN IDX](https://console.firebase.google.com/?idxSampleProjectTemplateId=gemini&dlAction=IdxSampleProject)

You can also kick-off this custom workflow from the Firebase console in the
_Build with Gemini_ section (find the "Experiment with a Gemini sample app" banner).

Here's some additional information about this custom workflow:

- To somewhat protect your Gemini API key, the workflow has imposed a quota limit on the
  API key of 10 RPM.
- This workflow creates a new IDX workspace. If you run out of workspace quota, go to
  [idx.google.com](idx.google.com) to delete an old workspace.

### Option 2: Run locally

You can also run this _Planning with the Gemini API_ web app locally. You'll just need
to complete some manual setup steps.

#### Prerequisites

- Node.js v20+
- npm v10+
- Angular CLI 18+

#### Setup instructions

1.  Set up Firebase:
    a. Create a new Firebase project in the
    [Firebase console](https://console.firebase.google.com/).
    You can skip setting up Google Analytics.
    b. Enable [Firestore](https://console.firebase.google.com/u/0/project/_/firestore)
    and [anonymous authentication](https://console.firebase.google.com/u/0/project/_/authentication)
    in your new project.
    c. Create a new Firebase web app in your new project.
    You can skip setting up Firebase Hosting.
    d. Copy your Firebase config object, and replace the placeholder values in the
    `src/environments/environments.ts` file of the sample app.

2.  Set up the Gemini API:
    a. [Get a Gemini API key](https://aistudio.google.com/app/apikey) in Google AI Studio.
    Use the Firebase project you just created.
    b. Add your Gemini API key into the `src/environments/environments.ts` file of the sample app.

3.  Run `npm install` to install the app's dependencies.

4.  Serve the app:
    a. Run `ng serve` to start the Angular development server.
    b. Open your browser and navigate to `http://localhost:4200`.

## Interact with the app

**How to Create and Manage Tasks:**

1.  **Start a New Task:**
    *   Select if you want to create a task related to a *location* or a *room* by clicking in the corresponding check box image.
    *   In the "Add a prompt" field, type a brief description of the task you want to plan. For example, "Plan a trip to Paris" or "Organize the living room".
    *   Click the "Go" button next to the prompt field. This will send your prompt to Gemini for processing.

2.  **Review the Generated Task:**
    *   Gemini will generate a main task title and a list of associated subtasks based on your prompt.
    *   The generated task and subtasks will appear in the section below the "Go" button.
    *   If you want to make changes or start over, click the "Reset" button.
    * You can edit the text in the input prompt and click "Go" again to generate a different list.

3.  **Save the Task:**
    *   If you're happy with the generated task, click the "Save" button.
    *   This will add the task to your main dashboard of to-do tasks.

4. **Manage tasks**
    * You can delete tasks.
    * You can mark tasks as completed.

## Migrate to use Vertex AI in Firebase





**In its DEFAULT state, this sample app is for _EXPERIMENTATION and PROTOTYPING ONLY_.**
It uses the [Google AI SDK for JavaScript](https://ai.google.dev/gemini-api/docs/quickstart?lang=web)
directly from the client-side which means that you risk potentially exposing your Gemini API key
to malicious actors if you deploy this app.

If you want to deploy this sample app or use it as a base for a production app,
**we strongly recommend that you migrate to use the
[Vertex AI in Firebase SDK](https://firebase.google.com/docs/vertex-ai), which offers
security options against unauthorized clients.** The sample app's codebase is already set up
to use the Vertex AI in Firebase SDK, and you just need to do a couple extra steps to set up
your Firebase project (as described below).

> [!NOTE]
> The sample app includes a Terraform config file ([`prod.tf.example`](prod.tf.example))
> that sets up Vertex AI in Firebase, including helping you set up billing,
> enabling the required APIs,
> and setting up [Firebase App Check](https://firebase.google.com/products/app-check).

1.  In the Firebase console, go to the
    [**Build with Gemini** page](https://console.firebase.google.com/project/_/genai),
    and then click the _Vertex AI in Firebase_ card to launch a workflow that helps you
    do the following tasks (if they're not already done):

    - Upgrade your project to use the
      [pay-as-you-go Blaze pricing plan](https://console.firebase.google.com/project/_/overview?purchaseBillingPlan=metered).
    - Enable the following two APIs for your project:\
      [Vertex AI API](https://console.cloud.google.com/apis/library/aiplatform.googleapis.com?project=_)
      and
      [Firebase ML API](https://console.cloud.google.com/apis/library/firebaseml.googleapis.com?project=_)

2.  As soon as you start seriously developing your app,
    [set up Firebase App Check](https://firebase.google.com/docs/vertex-ai/app-check)
    to protect your app from abuse by unauthorized clients.

3.  Follow security best practices by cleaning up your Firebase project and sample app:

    - If you're no longer using your Gemini API key, then delete it.

      - In the [**API keys** section of Google AI Studio](https://aistudio.google.com/app/apikey),
        view and delete your Gemini API key.
      - In the sample app's codebase, delete references to the Gemini API key in the following places:
        - `google_apikeys_key` resource entry in `main.tf`
        - `gemini_api_key` in both `src/environments/environments.ts` and `src/environments/environments.ts.tmpl`

    - If you're no longer using the Google AI Gemini API, then disable it in your project
      and delete references to it in your sample app's codebase:
      - Disable the API in the Google Cloud console:
        [generativelanguage.googleapis.com](https://console.cloud.google.com/apis/library/generativelanguage.googleapis.com?project=_)
      - Delete references to `generativelanguage.googleapis.com`, including the
        `google_service_usage_consumer_quota_override` resource entry in `main.tf`.

## Troubleshooting

```
Error when reading or editing Project "<project-id>": Get "https://cloudresourcemanager.googleapis.com/v1/projects/<project-id>?alt=json&prettyPrint=false":
compute: Received 500
```

This error happens because authentication has timed-out. Here's how to resolve it:

1.  In Project IDX, open a new terminal.
2.  In the terminal, run `terraform apply --auto-approve`, and then click continue when prompted to log in.
3.  Wait until the command succeeds.
4.  Reload the web preview, if necessary.

```
Error loading Gemini API key. Please rerun Terraform with terraform apply --auto-approve"
```

This error happens because Terraform failed to provision some resources
during initialization, such as API keys. Here's how to resolve it:

1.  In Project IDX, open a new terminal.
2.  In the terminal, run `terraform apply --auto-approve`, and then click
    continue when prompted to log in.
3.  Wait until the command succeeds.
4.  Reload the web preview, if necessary.

```
Check Firestore permissions in Firebase Console: link
```

This error happens because
[Firestore security rules](https://firebase.google.com/docs/firestore/security/get-started)
are blocking requests from your app. Here's how to resolve it:

1.  Go to the Firebase console using the link provided in the error message.
2.  Check that the security rules are what you expect. In particular,
    `timestamp.date` should be in the future.
3.  Reload the web preview, if necessary.

## Docs

- [Firebase Support](https://firebase.google.com/support)
- [Google AI Gemini API documentation](https://ai.google.dev/gemini-api/docs/quickstart?lang=web)
  (for experimentation and prototyping)
- [Vertex AI in Firebase documentation](https://firebase.google.com/docs/vertex-ai) (for production apps)
