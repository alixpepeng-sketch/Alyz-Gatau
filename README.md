
# Kyxzan Controller - WhatsApp & DDOS Management System

## 📖 Deskripsi
Sistem manajemen WhatsApp dengan fitur bug attack & DDOS panel & fitur yang lain, yang terintegrasi dengan Telegram bot untuk kontrol jarak jauh.

## ✨ Fitur
- 🤖 Telegram Bot Controller
- 📱 WhatsApp Session Management
- 💥 Bug Attack System (3 methods)
- ⚡ DDOS Attack Panel
- 👤 User Authentication System
- 🎵 Background Music Player
- 📊 Real-time Dashboard
- 📳 Kill wifi Dashboard
- 📛 Track Via Foto
- 🛜 Ngl Spammer
- 📶 Track Location & Lihat muka

## 🛠️ Tech Stack
- **Backend**: Node.js, Express.js
- **WhatsApp**: Baileys Library
- **Bot**: Telegraf (Telegram)
- **Frontend**: HTML, CSS, JavaScript
- **Database**: JSON File System

## 📋 Prerequisites
- Node.js v18+ 
- NPM/Yarn
- Telegram Bot Token
- VPS Ubuntu (untuk deployment)

## 🚀 Installation

### Local Development
```bash
# Clone repository
git clone <repository-url>
cd ky

# Install dependencies
npm install

# Configure environment
cp config.js.example config.js
# Edit config.js dengan Bot Token dan Owner ID

# Run application
npm start
```

### 🐧 VPS Ubuntu Deployment dengan Nginx (REKOMENDASI) 

#### 1. Setup Server
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install Node.js 18+
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Install PM2 untuk process manager
sudo npm install -g pm2

# Install Nginx
sudo apt install nginx -y

# Install Git
sudo apt install git -y
```

#### 2. Clone & Setup Project
```bash
# Clone project
git clone <repository-url> /var/www/ky
cd /var/www/ky

# Install dependencies
npm install

# Set permissions
sudo chown -R $USER:$USER /var/www/ky
sudo chmod -R 755 /var/www/ky
```

#### 3. Configure PM2
```bash
# Create PM2 ecosystem file
cat > ecosystem.config.js << 'EOF'
module.exports = {
  apps: [{
    name: 'nted-controller',
    script: 'server.js',
    instances: 1,
    autorestart: true,
    watch: false,
    max_memory_restart: '1G',
    env: {
      NODE_ENV: 'production',
      PORT: 5000
    }
  }]
}
EOF

# Start with PM2
pm2 start ecosystem.config.js
pm2 save
pm2 startup
```

#### 4. Configure Nginx
```bash
# Create Nginx config
sudo tee /etc/nginx/sites-available/ky << 'EOF'
server {
    listen 80;
    server_name ;
    
    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_cache_bypass $http_upgrade;
        proxy_connect_timeout 60s;
        proxy_send_timeout 60s;
        proxy_read_timeout 60s;
    }
}
EOF

# Enable site
sudo ln -s /etc/nginx/sites-available/ky /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

#### 5. Setup SSL (Optional)
```bash
# Install Certbot
sudo apt install certbot python3-certbot-nginx -y

# Generate SSL certificate

```

#### 6. Configure Firewall
```bash
# Allow necessary ports
sudo ufw allow 22      # SSH
sudo ufw allow 80      # HTTP
sudo ufw allow 443     # HTTPS
sudo ufw enable
```

## ⚙️ Configuration

### config.js
```javascript
module.exports = {
  Token: "YOUR_TELEGRAM_BOT_TOKEN",
  owner: "YOUR_TELEGRAM_USER_ID"
};
```

### acc.json (Default Users)
```json
[
  {
    "username": "admin",
    "password": "admin123", 
    "role": "ADMIN",
    "expired": ""
  }
]
```

## 🎛️ Telegram Bot Commands

```
/start - Show bot menu
/create <username> <password> <role> <expired> - Create user
/listakun - List all users
/delakun <username> - Delete user
/pairing <number> - Pair WhatsApp number
/listpairing - List active sessions
/delpairing <number> - Remove session
and lihat aja sendiri masi banyak!!!, bisa colong sender juga btw
```

## 🔧 Methods Available

### Bug Attack Methods
- `uibug` - UI freeze bug
- `delay` - Delay/lag bug
- `ios` - iOS specific bugs

### DDOS Methods
- Banyak lihat aja sendiri Males nulis nya

## 📊 Monitoring

### Check Application Status
```bash
# PM2 status
pm2 status
pm2 logs nted-controller

# Nginx status
sudo systemctl status nginx
sudo nginx -t

# Check ports
sudo netstat -tlnp | grep :80
sudo netstat -tlnp | grep :5000
```

### Performance Monitoring
```bash
# Monitor resources
pm2 monit

# Check logs
pm2 logs nted-controller --lines 100

# Restart if needed
pm2 restart nted-controller
```

## 🔄 Updates & Maintenance

### Update Application
```bash
cd /var/www/ky
git pull origin main
npm install
pm2 restart ky
```

### Backup Data
```bash
# Backup sessions and accounts
tar -czf backup-$(date +%Y%m%d).tar.gz sessions/ acc.json sessions.json
```

## 🛡️ Security Notes

1. **Change Default Passwords**: Update `acc.json` dengan password yang kuat
2. **Firewall**: Hanya buka port yang diperlukan
3. **SSL**: Gunakan HTTPS untuk production
4. **Telegram**: Jaga kerahasiaan bot token
5. **VPS Access**: Gunakan SSH key authentication

## ⚠️ Disclaimer

Tool ini dibuat untuk tujuan **educational** dan **testing** saja. Penggunaan untuk tujuan yang merugikan atau melanggar hukum adalah tanggung jawab pengguna sepenuhnya.

## 📞 Support

- **Telegram**: @RoufzzzNotDev
- **Channel**: @informasihdravvctinvistus

## 📄 License

This project is for educational purposes only.
