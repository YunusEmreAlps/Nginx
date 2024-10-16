# Nginx'e Giriş ve Temel Kurulum

Nginx yüksek performanslı bir web sunucusu ve reverse proxy sunucusudur. Genellikle statik içerik sunmak, yük dengelemek (load balancing) ve ters proxy olarak işlev görmek için kullanılır.

## Tarihçe

Nginx 2002 yılında Igor Sysoev tarafından oluşturulmuştur. Başlangıçta, bir sunucunun 10.000 eşzamanlı bağlantıyı idare etme yeteneğini ifade eden C10k sorununu çözmek için geliştirilmiştir. Nginx yüksek performansı, kararlılığı ve düşük kaynak tüketimi ile bilinir. Yüksek trafikli web siteleri ve web uygulamaları tarafından yaygın olarak kullanılmaktadır.

## Özellikler

Nginx, web sunucuları ve ters proxy'ler için popüler bir seçim haline getiren çok çeşitli özellikler ve yetenekler sunar. Nginx'in temel özelliklerinden bazıları şunlardır:

- **Yüksek Performans**: Çok sayıda eş zamanlı bağlantıyı minimum kaynakla verimli bir şekilde yönetir.
- **Reverse Proxy**: İstemci isteklerini diğer sunuculara/uygulamalara iletir.
- **Yük Dengeleme(Load Balancing)**: Performansı ve güvenilirliği artırmak için trafiği birden fazla sunucuya dağıtır.
- **Önbellekleme(Caching)**: Yükü azaltmak ve hızı artırmak için statik içeriği depolar.
- **SSL/TLS Sonlandırma**: Güvenli bağlantıları yönetir, şifreleme ve şifre çözme işlemlerini gerçekleştirir.
- **WebSockets Desteği**: Gerçek zamanlı istemci-sunucu iletişimini etkinleştirir.
- **HTTP/2 Desteği**: HTTP/1.1'e göre performansı ve verimliliği artırır.
- **Modüler Mimari**: Güvenlik, izleme ve daha fazlası için çeşitli modüllerle kolayca genişletilebilir.
- **Esnek Yapılandırma**: Basit, sezgisel bir yapılandırma dili ile özelleştirilebilir.
- **Açık Kaynak**: Aktif topluluk desteği ile 2 maddelik BSD lisansı altında yayınlandı.
- **Ölçeklenebilirlik ve Güvenlik**: Web uygulamalarını güvenlik açıklarına karşı ölçeklendirmek ve güvence altına almak için tasarlandı.

## Kullanım Örnekleri

Nginx, aşağıdakiler de dahil olmak üzere çeşitli senaryolarda yaygın olarak kullanılır:

- **Web Sunucusu**: Web siteleri ve web uygulamaları için statik ve dinamik içerik sunma.
- **Reverse Proxy**: İstekleri arka uç hizmetlerine veya diğer sunuculara iletme.
- **Yük Dengeleyici(Load Balancer)**: Trafiği birden fazla arka uç sunucusuna dağıtma.
- **Önbellekleme(Caching)**: Performansı artırmak için önbelleğe alınmış içeriği saklama ve sunma.
- **SSL/TLS Sonlandırma**: İstemciler ve sunucular arasındaki şifreli bağlantıları yönetme.
- **WebSockets**: Uygulamalarda gerçek zamanlı veri alışverişini destekleme.
- **Mikro Hizmetler Ağ Geçidi**: İstekleri farklı mikro hizmetlere yönlendirme.
- **İçerik Dağıtımı**: Önbelleğe alma yoluyla içerik dağıtımını hızlandırmak için bir CDN olarak hareket etme.
- **Yüksek Kullanılabilirlik**: Güvenilir, hata toleranslı kurulumlarla çalışma süresinin sağlanması.
- **Güvenlik Geliştirmeleri**: Yaygın web güvenlik açıklarına karşı koruma.
- **İzleme ve Günlükleme**: Trafik, hatalar ve performans ölçümleri için ayrıntılı günlükler yakalama.
- **DevOps Entegrasyonu**: Bulut ve konteyner ortamlarında dağıtım ve sunucu yönetimi görevlerini otomatikleştirme.

## Gelişmiş Yetenekler

- **HTTP/2**: Daha hızlı web performansı için optimize edilmiş iletişim.
- **WebSocket Desteği**: Gerçek zamanlı, çift yönlü iletişim.
- **SSL/TLS**: Gelişmiş şifreleme özellikleriyle güvenli bağlantılar.
- **Özelleştirilebilir Modüller**: Güvenlik, logging ve caching modülleri ile işlevselliği genişletin.
- **Entegrasyon**: Docker, Kubernetes ve CI/CD pipeline gibi diğer hizmetlerle sorunsuz uyumluluk.

Bu laboratuvarda, bir Linux sunucusunda Nginx'in temel kurulumunu ve yapılandırmasını ele alacağız.

## Kurulum

- **Ubuntu/Debian**:

```bash
  sudo apt install nginx
```

- **CentOS/RHEL**:

```bash
  sudo yum install nginx
```

- **macOS**: (Bu senaryoda macOS kullanmıyoruz, ancak yerel makinenize kurmak isterseniz aşağıdaki komutu kullanabilirsiniz)

```bash
  brew install nginx
```

- **Docker**: (Docker kullanarak Nginx'i çalıştırmak için)

```bash
  docker pull nginx

  # Nginx konteynerini çalıştır
  docker run -d -p 80:80 nginx

  # Nginx konteynerine eriş
  docker exec -it <container_id> /bin/bash

  # Nginx konteynerini durdur
  docker stop <container_id>

  # Nginx konteynerini kaldır
  docker rm <container_id>

  # Nginx imajını kaldır
  docker rmi nginx

  # Nginx loglarını kontrol et
  docker logs <container_id>

  # Nginx konteyner durumunu kontrol et
  docker ps -a | grep nginx
```

## Temel Yapılandırma Dosyaları

Ana yapılandırma ayarları genellikle **/etc/nginx/nginx.conf** dosyasında bulunur. Siteye özel yapılandırmalar için **/etc/nginx/sites-available/**  ve **/etc/nginx/sites-enabled/** dizinleri kullanılır.

## Nginx'i Başlatma ve Durdurma

- **Nginx'i Başlatma**:

```bash
  sudo systemctl start nginx
```

- **Nginx'i Durdurma**:

```bash
  sudo systemctl stop nginx
```

- **Nginx'i Yeniden Başlatma**:

```bash
  sudo systemctl restart nginx
```

- **Nginx Durumunu Kontrol Etme**:

```bash
  sudo systemctl status nginx
```

## Statik Bir Web Sitesi Sunma

Nginx, statik bir web sitesi sunmak için oldukça basit bir yapılandırmaya sahiptir. Öncelikle, Nginx yapılandırma dosyasını düzenleyin ve aşağıdaki gibi bir yapılandırma ekleyin:

```bash
  # Nginx yapılandırma dosyasına git
  cd /etc/nginx

  # Tüm dosyaları listele
  ls

  # Mevcut yapılandırma dosyası üzerine yazmak yerine, yeni bir dosya oluşturun
  # İsterseniz mevcut yapılandırma dosyası üzerine yazabilirsiniz
  mv nginx.conf old.nginx.conf
  
  # Nano metin düzenleyiciyi kullanarak yapılandırma dosyasını düzenleyin
  apt-get install nano
  nano /etc/nginx/nginx.conf

  # Veya Vim metin düzenleyiciyi kullanarak yapılandırma dosyasını düzenleyin
  apt-get install vim
  vim /etc/nginx/nginx.conf
```

- **nginx.conf**:

```nginx
events {}

http {
  server {
    listen 80;
    server_name localhost;

    root /var/www/html;
    index index.html;
  }
}
```

- **Yapılandırma dosyasını test etme**:

```bash
  sudo nginx -t
```

- **index.html dosyası oluşturma**:

```bash
  sudo nano /var/www/html/index.html
```

- **index.html**:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Welcome to Nginx</title>
</head>
<body>
  <h1>Welcome to Bulut Bilişimciler!</h1>
  <p>This is a sample website served by Nginx.</p>
</body>
</html>
```

Yukarıdaki yapılandırma, Nginx'in **/var/www/html** dizinindeki **index.html** dosyasını sunmasını sağlar. Yapılandırmayı oluşturduktan sonra, değişiklikleri uygulamak için Nginx'i yeniden başlatın.

- **Restart Nginx**:

```bash
  sudo systemctl restart nginx
```

- **Access the website**:

```bash
  curl http://localhost:80.bulutbilisimciler.com
```
