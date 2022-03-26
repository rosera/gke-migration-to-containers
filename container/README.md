How to build and test the container.

### Environment Variables

Environment variable defined in `gke-migration-to-containers/scripts/create.sh`

| ENV VARS | Value |
|----------|-------|
| ROOT | . |
| VERSION | 0.0.1 |
| BUILD_DATE | $(date) |
| VCS_REF | NO-VCS or $(git rev-parse HEAD) |

### Cloud Build
If building from the container directory change `ROOT` to `..`

 ```bash
   gcloud builds submit "$ROOT/container" \
       --config="${ROOT}/container/cloudbuild.yaml" \
           --substitutions _VERSION="${VERSION}",_BUILD_DATE="${BUILD_DATE}",_VCS_REF="${VCS_REF}"
           ```

### Run Locally

In the below command ensure the environment variable `$GOOGLE_CLOUD_PROJECT` is set

```bash
docker run -p 8080:8080 gcr.io/$GOOGLE_CLOUD_PROJECT/prime-flask:0.0.1
```
