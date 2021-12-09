# Run your own DeSo node

Running your own DeSo node is as easy as 1-2-3:

1. [Install Docker and Docker Compose](https://docs.docker.com/get-docker/) if you don't have it already
    * On Mac and Windows, Docker comes with Docker Compose
    * On Linux you need to install Docker Engine and Docker Compose separately
2. Execute `./run.sh`
    * Optionally, use `docker-compose up` arguments like `./run.sh -d` to run a daemon
3. Visit http://deso.run. This domain is aliased to your local machine so it will
   allow you to interact with your local node.

## Check sync progress

You can check on the sync progress of your local node in the admin panel.

1. Create a new user OR sign in with your existing seed phrase
2. Head to the Admin panel to see your sync status. The tooltips should explain what
   most things mean.

## Reset your node

If your node fails to sync or you want to try syncing from scratch you can run:

```bash
docker-compose -f docker-compose.dev.yml down --volumes
```
## What's next?
Once your node is synced, you have access to the full firehose of DeSo
data in real time! Below are some tips on how take full advantage of your node.
* Go to your Admin tab and watch the unfiltered feed update as your node
  syncs. It's like a time machine!
  - Note: If your node is having trouble syncing for some reason, try updating
    the CONNECT_IPS flag in dev.env to deso-seed-2.io or deso-seed-4.io and set
    IGNORE\_INBOUND\_PEER\_INV\_MESSAGES to true while you sync. This will pick
    a fairly reliable node as a sync peer and disregard messages from other
    peers.
* Try to whitelist some posts in the Admin tab and see that they've made their way
  onto your global feed.
* Read through the flags available in the [dev.env](https://github.com/deso-protocol/run/blob/main/dev.env)
  file. You can adjust these flags however you want, but note that we strongly
  recommend keeping your node in read-only mode for now. Turning read-only mode
  off could cause users who visit your node to make transactions that are not
  ultimately confirmed.
* Set ADMIN\_PUBLIC\_KEYS to your public key so that the Admin tab is only
  visible to your username.
* Set SUPER\_ADMIN\_PUBLIC\_KEYS to your public key so that the super admin tab is only
  visible to your username.
* Whitelist some posts and verify that they show up on the global feed.
* Deploy your node on any cloud provider with a static IP to make it accessible
  to anyone on the internet.
  - If you do this, you must replace deso.run with your domain in nginx.dev so
    that your traffic is routed to core and frontend properly.
  - If you want to customize which domains your frontend is allowed to connect to
    you must copy the [Caddyfile from frontend](https://github.com/deso-protocol/frontend/blob/main/Caddyfile)
    into this directory and set the `CADDY_FILE` variable in [dev.env](https://github.com/deso-protocol/run/blob/main/dev.env).
* Add the necessary nginx configuration for your SSL certificates generated by letsencrypt
* Set the TWILIO\* flags to allow new users to get some starter DeSo.
* Set a SUPPORT\_EMAIL so your users can contact you if they run into trouble.
* Play with the logging verbosity by increasing GLOG\_V.

## Need help?
The dev community is active on Discord and generally available to answer any
questions you might have, or any issues you run into. If you're having trouble, just
message in `#nodes-discussion` on the [DeSo Community Discord](https://discord.com/invite/deso).
