
tags: #project #sloth-app #raspberry-pi #docker #tailscale

###### Tailscale
- Raspberry PI tailscale IP address - 100.77.36.76
- funnel URL - https://raspberry-david.tailab87be.ts.net/


### Useful Maintenance Commands
#### View logs:
```
cd ~/Projects/evolu-relay 
docker compose logs -f
```

#### Restart relay:
```
docker compose restart
```

#### Update to latest version:
```
docker compose pull
docker compose up -d
```

#### Check disk usage:
```
du -sh data/ logs/
```

#### Disable tailscale funnel:
```
 tailscale funnel --https=443 off
```