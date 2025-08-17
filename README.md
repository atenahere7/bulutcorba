# QR Menü Starter (Vite + React + Tailwind)

Bu proje, QR menü uygulamasını hızla **yayına almanız** için hazırlanmış bir iskelettir.

## Kurulum (lokalde çalıştırma)
```bash
npm i
npm run dev
```
Ardından verilen yerel URL'yi tarayıcıda açın.

## Yapılandırma
- Menü verileri: `src/App.jsx` içindeki `MENU` dizisini düzenleyin.
- WhatsApp siparişi: `placeOrder()` içindeki `phone` numarasını `90XXXXXXXXXX` formatında değiştirin.
- Masa numarası için QR: `https://siteniz.com/?table=5` gibi bir QR oluşturun; uygulama `table` parametresini otomatik okur.

## Yayına Alma (her zaman açık site)
### Vercel (önerilen)
1. [Vercel] hesabı açın ve GitHub'a repo olarak gönderdikten sonra **New Project** → repo'yu seçin.
2. Framework: **Vite** otomatik algılanır. Build: `npm run build`, Output: `dist/`
3. Deploy'e basın. 1-2 dk sonra siteniz canlı.
4. Domain: **Settings → Domains** kısmından kendi alan adınızı ekleyin (ücretsiz SSL).

### Netlify
- **New site from Git** → repo'yu seçin.
- Build: `npm run build` , Publish directory: `dist`
- Domain ayarlayın.

### GitHub Pages (static)
- `npm run build` sonrası `dist/` klasörünü `gh-pages` dalına yayınlamak için `gh-pages` paketini kullanabilirsiniz.
- Not: Alt dizin yayınında `base` ayarı gerekebilir.

### Docker + Nginx (opsiyonel)
```
# Dockerfile
FROM node:20 AS build
WORKDIR /app
COPY package*.json ./
RUN npm i
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx","-g","daemon off;"]
```
```
docker build -t qr-menu .
docker run -p 8080:80 qr-menu
```

## PWA (opsiyonel)
Kullanıcıların menüyü çevrimdışı da açabilmesi için bir `manifest.json` ve service worker ekleyebilirsiniz.

## Güvenlik & Uptime İpuçları
- Domain + otomatik SSL (Vercel/Netlify).  
- Uptime monitoring: UptimeRobot, Better Stack vb.  
- Webhook/DB kullanırsanız gizli anahtarları **Environment Variables** olarak ekleyin, koda gömmeyin.  
- Sipariş kayıtlarını saklayacaksanız (KV/DB) KV (Vercel KV), Supabase, Firebase gibi servisleri düşünün.

## Lisans
Örnek ve eğitim amaçlı sunulmuştur; dilediğiniz gibi özelleştirin.
