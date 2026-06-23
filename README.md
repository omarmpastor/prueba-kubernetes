# prueba-kubernetes

## Instalar k3s

Instalamos k3s
```bash
curl -sfL https://get.k3s.io | sh -
```

## Configurar kubectl

Por defecto, necesitas usar sudo k3s kubectl. Para usar kubectl directamente:

Copiar kubeconfig
```bash
mkdir -p ~/.kube
sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
sudo chown $(id -u):$(id -g) ~/.kube/config
```

Añadir a .bashrc/.zshrc (opcional pero recomendado)
```bash
export KUBECONFIG=~/.kube/config
```

```bash
source .bashrc
```

## Crear estructura

```bash
sudo mkdir -p /mnt/storage/media/movies
sudo mkdir -p /mnt/storage/media/tv
sudo mkdir -p /mnt/storage/torrents
sudo mkdir -p /mnt/storage/sftpgo

sudo chown -R 1000:1000 /mnt/storage
sudo chmod -R 775 /mnt/storage
```

## Levantar stack

```bash
kubectl apply -f namespace.yaml
kubectl apply -f gateway.yaml
kubectl apply -f traefik-config.yaml

kubectl apply -f download-media
kubectl apply -f heimdall
kubectl apply -f jellyfin
kubectl apply -f pihole
kubectl apply -f sftpgo
kubectl apply -f gitea
```
