# scalingPipelines
The script needs the following options:

* --concurrent   optional,
                 the default value is 100

* --total        optional,
                 the default value is 10000

* --job          optional,
                 the default value is
                 https://raw.githubusercontent.com/tektoncd/pipeline/main/examples/v1/pipelineruns/using_context_variables.yaml

* --debug        optional,
                 the default value is false


Also, you need to apply pipelines, tasks, config, secret, and PVC before running the benchmark:
```
kc apply -f pipeline.yaml
```

Install the Gnu Parallel

e.g. in Fedora 38+
```
sudo dnf install -y parallel
```

## Example run
```
## Creating new namespace for benchmarking
kubectl create ns benchmark
kubectl config set-context --current --namespace=benchmark
## Applying resources to run benchmarking runs/jobs
kc apply -f pipeline.yaml
## Running benchmark
time ./benchmark-tekton.sh --total 100 --concurrent 10
```
