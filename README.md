# actions

## Running inside a Docker container

To start a Github Runner inside a Docker container (e.g. to ensure CUDA version compatibility), you must change two settings in the runner's `run.sh` script. To do so, add those two lines at the beginning of the file:

```
export DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=1 # Avoids errors related to localization
RUNNER_ALLOW_RUNASROOT=1 # Docker uses the root user
```

Then, simply bind the runner's folder to the container:

```
docker run --gpus all --rm --mount type=bind,source="$runner-folder-path",target=/actions "$docker-image" /actions/run.sh
```
