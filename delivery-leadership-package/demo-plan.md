# Friday Demo Plan

**Confirmed in writing to the platform team (Inject #1).** The demo runs locally, on my lab VM. Nothing in it needs the cloud.

## What the audience sees

1. The marketing page, opened with Live Server, with the life-first banner.
2. "Get your quote" opens the app at `http://localhost:5173`.
3. The recent-quotes list, read from the cluster's own database, and one quote saved live that survives a reload.

## What runs behind it

- The kind cluster `evergreen`: three `evergreen-quote-api:2.0` pods and one `mongo` pod.
- `kubectl port-forward svc/evergreen-quote-api 3000:80`, so the app's proxy reaches the cluster without changing a line.
- The client dev server on port 5173.

## Friday morning sequence

The VM shuts down every night, so the cluster is rebuilt on the day from the manifests in the repo:

1. `kind create cluster --name evergreen`
2. `kind load docker-image evergreen-quote-api:2.0 --name evergreen`
3. `kubectl apply -f k8s/mongo.yaml`, then wait for it to be available
4. `kubectl apply -f k8s/`, then `kubectl get pods` until all four are Running
5. Start the port-forward and the client, open the landing page, and save one quote so the list is not empty

**Start by 13:00; verified by 13:30.** The showcase begins at 14:00.

## Fallbacks

- **Plan B:** run the API dev server on port 3000 instead of the cluster. The app works unchanged.
- **Plan C:** the screenshots in `delivery-leadership-package/screenshots/`, one keystroke away.
