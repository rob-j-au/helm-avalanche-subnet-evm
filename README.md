## Avalanche with subnet-evm plugin

Demo Chart for Avalanche with subnet-evm

Uses custom docker image

- https://hub.docker.com/r/robjau/avalanche-subnet-evm
- https://github.com/rob-j-au/avalanche-subnet-evm

## Installation

```
helm install --namespace blockchain avalanche-subnet-evm ./helm-avalanche-subnet-evm
```

Args
```
args:
  - "--plugin-dir=/avalanchego/plugins"
  - "--db-dir=/data"
  - "--network-id=mainnet"
  - "--http-host=0.0.0.0"
  - "--http-port=9650"
  - "--http-allowed-hosts=*"
  - "--http-allowed-origins=*"
  - "--staking-port=9651"
  - "--api-metrics-enabled=true"
  - "--log-level=info"
  ```

Ports
```
service:
  type: ClusterIP
  ports:
    - name: api
      port: 9650
      targetPort: 9650
      protocol: TCP
    - name: p2p
      port: 9651
      targetPort: 9651
      protocol: TCP
```

Volumes

```
# PVC for avalanche data persistence
persistence:
  enabled: true
  size: 30Gi
  storageClass:
  accessModes:
    - ReadWriteOnce
  mountPath: /data
  name: avalanche-subnet-evm-data
```