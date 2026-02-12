# k8s-tests

## Pod Topology Spread Constraints

### Deployment.v1.apps

The field `spec.topologySpreadConstraints.labelSelector` references the field `spec.template.metadata.labels` of the `Deployment`.

```
spec.topologySpreadConstraints.labelSelector -> spec.template.metadata.labels
```

### Test
```
# scale deployment
k -n default scale deployment/k8s-test-k8s-tests --replicas=<number-of-replicas>
deployment.apps/k8s-test-k8s-tests scaled

# verify nodes where pods are scheduled
for p in $(k -n default get pod --no-headers | awk '{print $1 }'); do echo "Pod: $p"; echo "Node: $(k -n default get pod/$p -o jsonpath='{.spec.nodeName}')"; done
Pod: k8s-test-k8s-tests-7f66f9f7f-g8czd
Node: ip-44-126-78-165.eu-central-1.compute.internal
Pod: k8s-test-k8s-tests-7f66f9f7f-snt6z
Node: ip-44-126-74-230.eu-central-1.compute.internal
```

## Pod Disruption Budgets

### Deployment.v1.apps and PodDisruptionBudget.v1.policy

The field `spec.selector.matchLabels` of the `PodDisruptionBudget` references the field `spec.template.metadata.labels` of the `Deployment`.

```
spec.selector.matchLabels -> spec.template.metadata.labels
```

## Notes

The include "k8s-tests.labels" includes the include "k8s-tests.selectorLabels".
