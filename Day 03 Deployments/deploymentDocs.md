```markdown
# Kubernetes Deployment Process

## Deployment Configuration

### `deployment1.yml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: testpod1
  name: testpod1
  annotations:
    info: "satish deployment"
    email: "satishpaul"
    owner: "satishpaul"
spec:
  replicas: 6
  selector:
    matchLabels:
      app: testpod1
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: testpod1
    spec:
      containers:
      - image: kiran2361993/kubegame:v2
        name: kubegame
      - image: kiran2361993/mydb:v1
        name: mysqldb
        env: 
          - name: DB_NAME
            value: "mysqldb"
          - name: DB_PORT
            value: "3306"
          - name: DB_URL
            value: "weewewe"
```

## Commands Executed

1. **Apply the Deployment:**
   ```bash
   kubectl apply -f deployment1.yml
   ```

2. **Get the List of Pods:**
   ```bash
   kubectl get pod
   ```

3. **Check All Resources:**
   ```bash
   kubectl get all
   ```

4. **Execute a Command in a Pod:**
   ```bash
   kubectl exec -it testpod1-75b54d87bf-4k7nx /bin/bash
   ```

5. **Expose the Deployment:**
   ```bash
   kubectl expose deployment testpod1 --name svc --port 8000 --target-port 80 --type NodePort
   kubectl expose deployment testpod1 --name svc2 --port 5000 --target-port 5000 --type NodePort
   ```

6. **Describe the Service:**
   ```bash
   kubectl describe svc svc
   ```

7. **Dry Run for New Service:**
   ```bash
   kubectl expose deployment testpod1 --name svc3 --port 8000 --target-port 80 --type NodePort --dry-run=client -o yaml
   ```

8. **Delete the Deployment:**
   ```bash
   kubectl delete deployment testpod1
   ```

9. **Reapply the Deployment:**
   ```bash
   kubectl apply -f deployment1.yml
   ```

## Status Check

### All Resources After Deployment
```bash
kubectl get all
```

## Explanation of Deployment Strategy

- **Deployment Strategy:**
  - `RollingUpdate`: Replaces old pods gradually.
  - `Recreate`: Kills all existing pods before creating new ones.

## Conclusion

The deployment was successfully created, and the services were exposed as intended.
```
