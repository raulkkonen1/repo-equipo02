# 🚀 Despliegue Neuromotion en Azure ☁️

**➕ Paso 1: Agregar el repositorio Helm de Neuromotion**

```bash

helm repo add neuromotion https://rmcabrera.github.io/neuromotion-charts/;

helm repo update

```

**⬇️ Paso 2: Instalar los pre-requisitos**

```bash

helm install ms-prerequisites neuromotion/ms-prerequisites

```

**🗄️ Paso 3: Instalar las bases de datos**

```bash

helm install mysql-doctores neuromotion/mysql-doctores -n ms-app;

helm install mysql-usuarios neuromotion/mysql-usuarios -n ms-app

```

**🚀 Paso 4: Instalar los microservicios**

```bash

helm install ms-doctores neuromotion/ms-doctores -n ms-app;

helm install ms-usuarios neuromotion/ms-usuarios -n ms-app

```

**🖥️ Paso 5: Instalar el Frontend**

```bash

helm install neuromotion-frontend neuromotion/neuromotion-frontend -n ms-app

```

**🌍 Paso 6: Exponer el Frontend con LoadBalancer**

```bash

kubectl patch svc neuromotion-frontend-service -n ms-app -p '{"spec": {"type": "LoadBalancer"}}'

```

**✔️ Paso 7: Verificar el estado de los servicios**

```bash

kubectl get svc -n ms-app

```

**✔️ Paso 8: Obtener la IP pública del Frontend**

```bash

kubectl get svc neuromotion-frontend-service -n ms-app

```

**🌐 Paso 9: Acceder al Frontend a través de la IP pública proporcionada**

**Para Finalizar el cluster

az aks stop --name myAKSCluster --resource-group aks-resource-group