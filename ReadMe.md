Simple app to demonstrate running a multi-tiered web app on CloudRun

Instructions to run the app:
1. In the GCP project, enable Firestore native mode
2. Clone this repo in cloudshell
3. In cloud shell, go to the Internal folder and type (Change PROJECT-ID to your project ID):
  gcloud builds submit --tag gcr.io/PROJECT-ID/int:v1 .
4. Go to External folder and type:
  gcloud builds submit --tag gcr.io/PROJECT-ID/ext:v1 .
5. Create a cloud run service for the internal container
  - Set container port to 8082
  - Once deployed, can test with URL/events
6. Create a cloud run service for the external container
  - Set container port to 8080
  - Create an environment variable named SERVER, set value to URL of the internal service
7. Once deployed, visit the external URL in a browser. The app should work - it allows you to create events and like existing events.
8. Can now change the external service. 
Edit the external/views/layouts/default.hbs and change something on the page
9. Build the docker container again and publish to GCR:
    gcloud builds submit --tag gcr.io/PROJECT-ID/ext:v2 .
10. In cloud run, deploy a new verison using the new gcr.io url 
9. Can do traffic splitting between versions

