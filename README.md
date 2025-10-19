# 🌸 CV One Page - Manar Darghouthi


## But
Publier un CV one-page en HTML/CSS via GitHub Pages, conteneuriser l'app et la déployer localement avec Docker Compose, puis déployer sur K3S.
## Arborescence
- index.html
- style.css
- Dockerfile
- docker-compose.yml
- README.md
- assets
- cv-deployment.yaml
- cv-service.yaml


## Étapes principales
# Partie 1 — CV, Git, Docker, Docker Hub, docker-compose
1. `git init` → `git commit -m "Version 1"`
2. Création du repo GitHub: `manardarghouthi.github.io`
3. `git push origin main` & `git push origin dev`
4. Build Docker image: `docker build -t manardarghouthi/cv:v1 .`
5. Push to Docker Hub: `docker push manardarghouthi/cv:v1`
6. docker-compose: `docker compose up -d` (port 8005)
# Partie 2 — K3s (Controller + 2 workers) et déploiement
7. K3S: installer  `curl -sfL https://get.k3s.io | sh -`
8. Récupération du token pour les workers `sudo cat /var/lib/rancher/k3s/server/node-token`
9. Installation de K3s sur les workers `curl -sfL https://get.k3s.io | K3S_URL=https://IP_controller:6443 K3S_TOKEN=<token_du_master> sh -`
8. Accès au cluster depuis la machine physique (Windows)`sudo cat /etc/rancher/k3s/k3s.yaml``scp /etc/rancher/k3s/k3s.yaml user@host:/home/user/.kube/config` 
9. Création des manifests Kubernetes cv-deployment.yaml et cv-service.yaml:`kubectl apply -f cv-deployment.yaml kubectl apply -f cv-service.yaml`
10. Test d’accès: `http://<IP_du_master>:nodePort`
## Captures d'écran
![Docker build](assets/docker.png)
![Docker push](assets/docker.png)
![page HTML](assets/pagehtml.png)
![github](assets/github.png)
![branches](assets/branches.png)
![localhost:8005](assets/test.png)
![Installer K3S:controller](assets/controller.png)
![Installer K3S — Agents sur chaque worker](assets/worker.png)
![sur le controller:kubectl get nodes](assets/kubectl_get_nodes.png)
![Accès au cluster depuis la machine physique](assets/machine_physique.png)
![manifests Kubernetes cv-deployment](assets/manifests-Kubernetes.png)
![manifests Kubernetes cv-service](assets/manifests-Kubernetes.png)
![Testez l'accès à votre CV déployer sur K3S via un navigateur](assets/Teste-navigateur.png)


