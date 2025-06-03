# directus-marketplace-cluster-check
Validate if Directus propagates extensions downloaded from Marketplace to all other instances in a cluster

## Steps to reproduce
1. Run `docker compose up -d` to start all the services
1. Run `docker compose exec redis redis-cli` to gain access to redis for verification purposes
1. Login to any of the directus instance by specifying the exact port that was exposed, and login.
1. Verify in `redis-cli` that Redis is in used by Directus via `KEYS *`
1. Go to Marketplace and download an extension (e.g. `Display Link` by `jacoborus`) and reload page as needed
1. Verify that the extension exists in the extension management page
1. Login to a different directus instance in the cluster by changing to a different exposed port in the url
1. Verify that the extension does not exist in the extension management page
1. Run `docker compose exec directus1 ls -al extensions/.registry`, for `directus1`, `directus2`, and `directus3`. Verify that only one of the instance has the folder.
