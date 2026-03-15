  * tags: #pbctl #productboard
  * notes:
    * ## Useful commands for pbctl
      * How to run elastic import in pbctl
        * ```javascript
POD_NAME=$(kubectl get pod -l app=pb-backend --field-selector=status.phase=Running --no-headers | awk '{print $1}');
kubectl exec $POD_NAME -- rake 'dev:elasticsearch:refresh[qa-v9-template]'```
      * How fix issue with github username
        * ```javascript
// Add this to .gitconfig
[url "ssh://git@github.com/"]
    insteadOf = https://github.com/```
      * Issue Tom is experiencing
        * ```javascript
tailscale up --accept-routes```