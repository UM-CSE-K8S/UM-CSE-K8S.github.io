# Kubernetes Configuration Files

This directory contains example Kubernetes YAML configurations for setting up priority-based scheduling on a GPU cluster.

## Files Overview

### priority-classes.yaml
Defines four priority classes for GPU workloads:
- **high-priority-gpu** (value: 1000000) - For critical GPU workloads
- **medium-priority-gpu** (value: 500000) - For standard GPU workloads
- **low-priority-gpu** (value: 100000) - For batch GPU workloads
- **best-effort-gpu** (value: 0) - Default for non-critical workloads

### high-priority-pod.yaml
Example pod configuration with high priority that:
- Uses the `high-priority-gpu` priority class
- Requests 1 GPU
- Runs nvidia-smi to verify GPU access

### medium-priority-job.yaml
Example Kubernetes Job with medium priority that:
- Uses the `medium-priority-gpu` priority class
- Runs a PyTorch container
- Verifies CUDA availability
- Requests 1 GPU

### low-priority-deployment.yaml
Example Deployment with low priority that:
- Uses the `low-priority-gpu` priority class
- Creates 2 replicas
- Each replica requests 1 GPU
- Runs nvidia-smi periodically

## Usage

1. First, apply the priority classes:
```bash
kubectl apply -f priority-classes.yaml
```

2. Deploy example workloads:
```bash
# Deploy high priority pod
kubectl apply -f high-priority-pod.yaml

# Deploy medium priority job
kubectl apply -f medium-priority-job.yaml

# Deploy low priority deployment
kubectl apply -f low-priority-deployment.yaml
```

3. Verify priority scheduling:
```bash
# Check pod priorities
kubectl get pods -o custom-columns=NAME:.metadata.name,PRIORITY:.spec.priority,PRIORITY-CLASS:.spec.priorityClassName,NODE:.spec.nodeName

# Watch scheduling events
kubectl get events --sort-by='.lastTimestamp' | grep -i preempt
```

## Testing Preemption

To test that high-priority pods can preempt low-priority ones:

1. Fill the cluster with low-priority pods:
```bash
kubectl scale deployment low-priority-batch --replicas=4
```

2. Deploy a high-priority pod:
```bash
kubectl apply -f high-priority-pod.yaml
```

3. Watch for preemption events:
```bash
kubectl get events --watch
```

You should see the scheduler preempting low-priority pods to make room for the high-priority one.

## Customization

Feel free to modify these configurations for your specific needs:
- Adjust priority values to match your requirements
- Change resource requests/limits
- Add additional labels and annotations
- Configure node selectors or affinity rules
