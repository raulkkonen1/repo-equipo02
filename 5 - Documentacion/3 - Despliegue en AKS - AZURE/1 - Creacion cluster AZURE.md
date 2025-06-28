# 🚀 Guía de Instalación en Azure ☁️

**Antes de comenzar, ingrese al Cloud Shell de Azure.**

**🔑 Paso 0: Iniciar sesión en Azure Cloud Shell**

Inicie sesión en su cuenta de Azure a través del portal web y seleccione la opción Cloud Shell. Este entorno ya tiene las herramientas necesarias preinstaladas y configuradas.

**✅ Paso 1: Validar y Registrar los proveedores necesarios**

```bash

az provider show --namespace Microsoft.Insights --query "registrationState"

```

**Debe devolver "Registered".

**Ejecuta estos dos comandos para registrar el proveedor:

```bash

az provider register --namespace Microsoft.Insights

az provider register --namespace Microsoft.ContainerService

```

**➕ Paso 2: Crear el grupo de recursos**

```bash

az group create --name aks-resource-group --location brazilsouth

```

```Resultado

{

"id": "/subscriptions/29d22f3b-c14d-4a8d-a355-bdfced5435e5/resourceGroups/aks-resource-group",

"location": "brazilsouth",

"managedBy": null,

"name": "aks-resource-group",

"properties": {

"provisioningState": "Succeeded"

},

"tags": null,

"type": "Microsoft.Resources/resourceGroups"

}

```

**⚙️ Paso 3: Crear el clúster AKS**

```bash

az aks create --resource-group aks-resource-group --name myAKSCluster --node-count 2 --enable-addons monitoring --generate-ssh-keys --location brazilsouth --node-vm-size Standard_D2s_v6

```

**🔑 Paso 4: Obtener las credenciales del clúster AKS**

```bash

az aks get-credentials --resource-group aks-resource-group --name myAKSCluster

```

**✔️ Paso 5: Verificar el estado de los nodos en el clúster**

```bash

kubectl get nodes

```