# k8s

### Sugestões Cluster k8s

**Criar dois clusters gerenciados (EKS):**
- Cluster 01 - Produção (Apartado)
- Cluster 02 - Staging + Dev (Namespace)

- Cluster 01: Cluster de produção apartado dos demais clusters de staging e dev
    - **Sugestão:** Subir as ferramentas de suporte (containers de monitoramento e observabilidade) em um namespace diferente.
- Cluster 02: Cluster dos ambientes de staging + dev (fazendo uso de namespaces)
    - **Sugestão:** Subir as ferramentas de suporte (containers de monitoramento e observabilidade) em um namespace diferente.

<br>

### Utilizando Docker Registry Privado (Github)

**Comando**
```
kubectl create secret docker-registry ghcr-secret --docker-server=ghcr.io --docker-username=<owner> --docker-password=<PAT_TOKEN>
```

Uma vez criado o secret de autenticação para o repositório privado de imagens do docker, basta referenciar o secret no manifesto de deployment.

**deploytment.yml**
```yaml
  imagePullSecrets:
    - name: ghcr-secret
```

<br>

### Self Healing

#### Liveliness Probe
Serve para verificar a saude do container batendo em um endpoint de health

#### Readiness Probe
Verifica se o container está pronto para receber requisições

#### Startup Probe
Ajusta o tempo de inicialização da aplicação/container