# pp-helm-charts

## Requirements

- git
  - Manage the code
- helm
  - Manage the helm charts e.g. CRUD operations, packaging charts, etc.
- kubectl
  - Deploy the helm charts into the cluster
- minikube
  - Spawn a cluster locally within the development machine

## Use (read) the helm charts

- If setting up initially:
```bash
$ helm repo add pearlpay https://nponcian.github.io/pp-helm-charts/packages/
$ helm repo list  # View the added repo
$ helm search repo pearlpay  # View the helm charts inside the repo
$ helm show values pearlpay/app-service  # View the values of a helm chart
```

- If already exists but it had some changes e.g. URL source
```bash
$ helm repo update pearlpay
```


## Create or update a helm chart

- Setup a static site hosting service that can serve the helm chart packages such as GitHub Pages (used here).


- Download the code
```bash
$ git clone git@github.com:nponcian/pp-helm-charts.git
```

- Go to the code
```bash
$ cd pp-helm-charts/
```

- If a new helm chart is needed, then create one
```bash
$ helm create app-service
```

- Update the files in the helm chart as needed


- Package the helm chart
```bash
$ helm lint app-service/  # just to verify that the chart is well-formed
$ helm package app-service/
$ mv app-service.tgz packages/  # for a cleaner repo, put the packages in its own directory
```


- Create or update an index for the packages
```bash
$ helm repo index --url https://nponcian.github.io/pp-helm-charts/packages/ .
$ mv index.yaml packages/  # put the index in the same directory as the packages
```


- Update the static site server with the updated files. When using GitHub pages (used here), just push the changes and point the branch `gh-pages` to it (or the branch that was configured for the GitHub pages).
```bash
$ git checkout gh-pages  # Use the flag -b if gh-pages hasn't been created yet
$ git add .
$ git commit -m "Some commit message here"
$ git push origin gh-pages
```
