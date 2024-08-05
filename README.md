# 42-Inception


sudo apt-get install ntpdat

sudo ntpdate ntp.ubuntu.com






Proje bizden Docker kullanarak bir WordPress sitesi kurmamızı, ve bu siteyi Nginx web sunucusu ve MariaDB veritabanı ile yapılandırmamızı istiyor. Bu, üç ana bileşeni Docker konteynerları olarak çalıştıracağımız anlamına gelir.


WordPress konteyneri: WordPress uygulamasını çalıştırır.

Nginx konteyneri: Web sunucusu olarak hizmet eder ve HTTP isteklerini yönetir.

MariaDB konteyneri: Veritabanı sunucusu olarak hizmet eder.

Bu yapılandırmayı Docker Compose kullanarak kolayca yapabiliriz. Docker Compose, birden fazla konteyneri tanımlayıp yönetmenize olanak tanıyan bir araçtır.

Web Sunucusu:

Web sunucusu, web sitelerinin kullanıcıların tarayıcılarına sunulması için gerekli olan yazılım ve donanım bileşenlerinin bir araya gelmesiyle oluşur. Web sunucusu, kullanıcıların HTTP veya HTTPS protokolleri aracılığıyla yaptıkları istekleri alır ve bu isteklere uygun web sayfalarını veya kaynakları geri gönderir.

Nginx Nedir?

Nginx (Engine-X olarak telaffuz edilir), yüksek performanslı ve açık kaynaklı bir web sunucusudur. Nginx, sadece bir web sunucusu olarak değil, aynı zamanda ters proxy, yük dengeleyici, HTTP önbellekleyici ve e-posta proxy sunucusu olarak da kullanılabilir.

Nginx Özellikleri:

-Yüksek performans

-Düşük Bellek Kullanımı

-Ters Proxy(Nginx, ters proxy olarak çalışabilir. Bu, istemciden gelen istekleri alır ve arka uç sunucularına yönlendirir. Bu şekilde, yük dengeleme ve önbellekleme gibi işlemler gerçekleştirilir)

-Yük Dengeleme(Birden fazla sunucu arasında gelen istekleri dağıtarak yük dengeleme yapabilir)

-SSL/TLS Desteği(Güvenli iletişim için SSL/TLS sertifikaları ile çalışabilir.)


MariaDB nedir?

MariaDB, açık kaynaklı bir veritabanı yönetim sistemi (DBMS) olan MySQL'in bir çatalıdır (fork). Yani, MySQL'in kaynak kodundan türetilmiş ve geliştirilmeye devam edilen bir projedir denilebilir. MySQL'den farklı olarak, MariaDB topluluk tarafından yönetilir ve geliştirilir, bu da onu daha açık ve şeffaf bir proje yapar.

MariaDB özellikleri:

-Açık Kaynak(Herkes kaynak kodunu indirebilir, değiştirebilir, dağıtabilir)

-MySQL ile uyumlu

-Gelişmiş performans ve güvenlik

-Ek depolama motorları var(MySQL' e göre)


MariaDB'nin kullanım alanlarından biri web uygulamalarıdır. Sıklıkla WordPress, Joomla, Drupal gibi popüler içerik yönetim sistemleri (CMS) ile kullanılır. Web sitelerinin veritabanı ihtiyaçlarını karşılamak için idealdir.

Veritabanı, verilerin düzenli bir şekilde saklandığı ve yönetildiği bir sistemdir. Bu sistem, verilerin kolayca erişilebilmesi, yönetilebilmesi ve güncellenebilmesi için tasarlanmıştır. Veritabanları, bir veya daha fazla tablodan oluşur ve her tablo, belirli bir türdeki verileri içerir.


MySQL nedir?

MySQL, dünya genelinde yaygın olarak kullanılan, açık kaynaklı bir ilişkisel veritabanı yönetim sistemidir (RDBMS).


MySQL özellikleri:

-İlişkisel Veritabanı

-Açık Kaynak

-Geniş Kullanım Alanı

-Yüksek performans ve güvenlik


Wordpress nedir?

WordPress, dünya çapında milyonlarca web sitesi tarafından kullanılan, açık kaynaklı ve ücretsiz bir içerik yönetim sistemi (CMS)dir. WordPress, ilk başlarda özellikle bloglar ve basit web siteleri oluşturmak için popülerdi, ancak zamanla daha karmaşık ve büyük web siteleri için de kullanılabilir hale gelmiştir. 


Wordpress özellikleri:

-Açık kaynak

-Kullanıcı dostu

-Medya yönetimi

-Güvenlik


Dockerfile:

Dockerfile, Docker konteynerlerini oluşturmak ve yapılandırmak için kullanılan bir metin dosyasıdır. Belirli bir uygulamanın veya hizmetin Docker imajını oluşturmak için adım adım komutlar içerir ve bu sayede uygulamanın herhangi bir ortamda kolayca dağıtılmasını ve çalıştırılmasını sağlar. Dockerfile, Docker ekosisteminin temel yapı taşlarından biridir ve konteyner tabanlı uygulama dağıtımının standartlaştırılmasına katkıda bulunur.


from: oluşturacağı docker imajını hangi temlli ayarlayacağını belirtir.(yemel imajını belirtir)

run: Gerekli paketleri yükler(Docker iamjı oluşturtulurken çalıştıralacak komutları belirtir)

-update: günceller

-install -y: indirir, kurar

-- php-fpm: PHP-FPM (FastCGI Process Manager) sunucusunu çalıştırmak için.

-- php-mysql: PHP'nin MySQL desteği için.

-- sendmail: E-posta göndermek için kullanılır.

-- wget: Dosya indirme aracı.


RUN wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \ && chmod +x wp-cli.phar \ && mv wp-cli.phar /usr/local/bin/wp-cli:WordPress komut satırı aracı olan wp-cli'yi indirip kurar. wget ile wp-cli.phar dosyasını indirir, chmod +x ile çalıştırılabilir yapar ve /usr/local/bin/wp-cli dizinine taşır.

-expose: konteynerin dış dünyaya hangi port üzerinden erişileceğini belirtir.(Docker konteynerin hangi portları dinleyeceğini belirtir.)

-copy: COPY komutu, yapılandırma dosyalarını konteyner içerisine kopyalar. Bu örnekte, www.conf dosyası yerel dizinden konteynerdeki PHP-FPM yapılandırma dizinine kopyalanır. (Konfigürasyon dosyası, bir yazılım uygulamasının veya sistemin çalışma parametrelerini ve ayarlarını belirten bir dosyadır.)

+x yalnızca yürütme (execute) izni ekler.

-entrypoint: Konteyner başlatıldığında çalıştırılacak ana komutu belirtir

-cmd: ENTRYPOINT tarafından belirtilen komut çalıştırıldıktan sonra varsayılan olarak çalıştırılacak komutu belirtir. Bu örnekte, PHP-FPM sunucusu --nodaemonize seçeneği ile başlatılır, yani arka planda çalışmaz, ön planda çalışır.


"PHP, sunucu taraflı dinamik web sayfaları oluşturmak için kullanılan, geniş bir kullanım alanına sahip, güçlü ve esnek bir betik dilidir. WordPress gibi popüler içerik yönetim sistemleri, PHP'nin yeteneklerinden faydalanarak dinamik ve etkileşimli web siteleri oluşturur. PHP'nin veritabanı desteği, geniş kütüphane desteği ve topluluk desteği, onu web geliştirme için ideal bir dil yapar."


"PHP-FPM, WordPress gibi dinamik web uygulamaları için yüksek performans ve verimlilik sağlayan bir PHP işlem yöneticisidir. Nginx ile birlikte kullanıldığında, PHP betiklerinin hızlı ve verimli bir şekilde işlenmesini sağlar, bu da web sitesinin genel performansını ve kullanıcı deneyimini önemli ölçüde iyileştirir. Inception projesinde PHP-FPM'in kullanılması, WordPress'in yüksek performanslı ve ölçeklenebilir bir şekilde çalışmasını sağlamak için kritik bir rol oynar."

***********************************************************

src/wordpress/conf/www.conf:

Bu, PHP-FPM (FastCGI Process Manager) bir yapılandırma dosyasıdır. İçerisinde çalışma ve performans ayarlarını barındırır.

[www] : Bu bölüm, PHP-FPM havuzu yapılandırmasıdır.

user ve group: PHP-FPM işlemlerinin hangi kullanıcı ve grup kimliği altında çalışacağını belirtir. 

listen: PHP-FPM'nin dinleyeceği adres ve portu belirtir. wordpress:9000 burada PHP-FPM'nin wordpress adlı kullanıcıya ve 9000 numaralı bir port üzerinden istekleri dinleyeceğini gösterir.

listen.owner ve listen.group: PHP-FPM'nin dinleme soketinin sahibi (owner) ve grubunu belirtir.

pm: PHP-FPM'nin işlem yönetim modunu belirtir.

pm.max_children: Havuzda aynı anda çalışacak maksimum PHP işlem sayısını belirtir.

pm.start_servers: PHP-FPM başlatıldığında başlangıçta çalışacak işlem sayısını belirtir.

pm.min_spare_servers: Minimum boşta bekleyen işlem sayısını belirtir. Yeni istekler geldiğinde bu sayı kadar işlem başlatılır.

pm.max_spare_servers: Maximum boşta bekleyen işlem sayısını belirtir. Fazla işlem varsa, gereksiz işlemler kapatılır.


src/wordpress/tools/wp.sh:

Bu wp.sh script'i, Docker veya benzeri konteyner ortamlarında, otomatik olarak WordPress'i kurmak ve yapılandırmak için kullanılabilir. Script içinde kullanılan wp-cli aracı, WordPress komut satırı işlemlerini gerçekleştirmek için kullanılır ve bu sayede otomatik kurulum ve yapılandırma işlemleri yapılabilir.

#!/bin/bash: Bu satır, script'in bir bash script'i olduğunu belirtir.

chown -R www-data: /var/www/*; ve chmod -R 755 /var/www/*: /var/www/ dizinindeki tüm dosya ve dizinlerin sahipliğini www-data kullanıcısına ve grubuna (chown) ve izinlerini (chmod) 755 olarak ayarlar. Bu, web sunucunuzun (örneğin Nginx veya Apache) bu dosya ve dizinlere erişebilmesi için önemlidir.

mkdir -p /run/php/; ve touch /run/php/php7.4-fpm.pid;: /run/php/ dizinini oluşturur (varsa yeniden oluşturmaz) ve php7.4-fpm.pid dosyasını oluşturur. Bu, PHP-FPM'nin çalışması için gereklidir ve pid dosyası, PHP-FPM süreçlerini izlemek için kullanılır.

WordPress Kurulumu Bölümü:

if [ ! -f /var/www/html/wp-config.php ]; then: Eğer /var/www/html/wp-config.php dosyası yoksa: mkdir -p /var/www/html;: /var/www/html dizinini oluşturur (varsa yeniden oluşturmaz) ve içine geçer.

WordPress Çekirdeğini İndirme:

wp-cli core download --allow-root;: wp-cli aracını kullanarak WordPress çekirdeğini indirir (wp-cli'nin yüklü olması gerekir).

WordPress Yapılandırma Dosyası Oluşturma:

wp-cli config create --allow-root ...: wp-cli ile WordPress yapılandırma dosyasını oluşturur. Bu adımda MySQL veritabanı adı ($MYSQL_DATABASE_NAME), kullanıcı adı ($MYSQL_USER), şifre ($MYSQL_PASSWORD) ve MySQL sunucu adresi (mariadb) belirtilir.

WordPress Kurulumu:

wp-cli core install --allow-root ...: wp-cli ile WordPress'i kurar. Site URL ($DOMAIN_NAME), site başlığı ($TITLE), yönetici kullanıcı adı ve şifre ($WORDPRESS_ADMIN_NAME, $WORDPRESS_ADMIN_PASSWORD) ve yönetici e-posta adresi ($WORDPRESS_ADMIN_EMAIL) gibi bilgiler belirtilir.

Kullanıcı Oluşturma:

wp-cli user create --allow-root ...: wp-cli ile bir kullanıcı oluşturur. Bu genellikle WordPress yönetici kullanıcısıdır ($MYSQL_USER ve $MYSQL_EMAIL).

wp-cli core download --allow-root: bu tam oalar şunu yapar. Wordpress komut satırı olan wp-cli aracının core modülünü kullanarak Wordpress çekirdek dosyalarının indirir ve root olarak çalışmasına izin verir.


src/mariadb/conf/50-server.cnf:

Bu dosya, MariaDB’nin temel yapılandırma ayarlarını içeriyor.

[mysqld] : Bu satır, bu bölümde yer alan ayarların MySQL veya MariaDB sunucusu (mysqld) için yapıldığını belirtir.

user: MySQL/MariaDB sunucusunun çalıştırılacağı kullanıcıyı belirtir.

socket: Sunucunun MySQL soket dosyasının konumunu belirtir. Soket dosyası, yerel iletişim için kullanılır.

basedir: MySQL/MariaDB kurulumunun temel dizinini belirtir. Program dosyaları (bin ve diğerleri) burada bulunur.

datadir: Veritabanı dosyalarının (*.frm, *.ibd, vb.) depolandığı dizini belirtir.

log_error: MySQL/MariaDB sunucusunun hata ve bildirim kayıtlarının tutulacağı log dosyasının yolunu belirtir. Hatalar ve uyarılar bu dosyaya yazılır.

expire_logs_days: Binary logların kaç gün saklanacağını belirtir. Binloglar, veritabanı üzerindeki değişiklikleri loglamak için kullanılır.

character-set-server: Veritabanı sunucusunun varsayılan karakter setini belirtir. utf8mb4, Unicode karakter seti için genişletilmiş bir formattır ve genellikle modern web uygulamalarında kullanılır.

bind-address: MySQL/MariaDB sunucusunun hangi IP adresi veya arayüzü üzerinden bağlantı kabul edeceğini belirtir. 0.0.0.0 değeri, tüm ağ arayüzlerinden gelen bağlantıları kabul et anlamına gelir. Bu genellikle sunucunun herhangi bir IP adresinden erişilebilir olmasını sağlamak için kullanılır.


src/mariadb/tools/dbstart.sh:

Bu SQL komutları, WordPress için bir veritabanı oluşturur. Yeni bir kullanıcı eklemeyi, kullanıcıya gerekli yetkileri vermeyi ve şifre değişikliği yapmayı sağlar.
Bu betik, MariaDB servisini başlatır, belirli bir veritabanı oluşturur, belirli bir kullanıcıyı ve bu kullanıcıya yetkileri tanır, ardından servisi durdurur. Özellikle otomatik yükleme ve başlangıç senaryolarında kullanılan bir betiktir, çünkü MariaDB sunucusunun ilk yapılandırmasını ve temel veritabanı hazırlıklarını otomatik olarak yapar.
service : komutuyla mariadb servisi başlatılır. Bu komut, MariaDB servisini etkinleştirir ve çalıştırır.
sleep 3 ile işlem duraklatılır. Bu mariaDB servisinin tam olarak başlatılmasını beklemek içindir.


Veritabanı ve Kullanıcı Oluşturma İşlemleri:

mariadb -e "CREATE DATABASE IF NOT EXISTS $MYSQL_DATABASE_NAME;": Belirtilen isimde bir veritabanı oluşturur (eğer zaten yoksa).

mariadb -e "CREATE USER IF NOT EXISTS '$MYSQL_USER'@'%' IDENTIFIED BY '$MYSQL_PASSWORD';": Belirtilen kullanıcıyı ve parolayı yaratır (eğer zaten yoksa).

mariadb -e "GRANT ALL PRIVILEGES ON $MYSQL_DATABASE_NAME.* TO '$MYSQL_USER'@'%';": Veritabanına tam yetki verir.

mariadb -e "FLUSH PRIVILEGES;": MariaDB için güvenlik ayarlarını yeniler.

mariadb -e "SHUTDOWN;": MariaDB servisini durdurur.

exec "$@" : betiğin son komutunu çağırır. "$@" betiğe iletilen tüm argümanları içerir. Bu, genellikle Docker konteynerlerinde veya betiklerde son işlemi belirtmek için kullanılır. (Bundan sonraki sh dosyası çalışsın ayni her şey sırasıyla yapılsın demek)


src/nginx/dockerfile:

CMD [ "nginx", "-g", "daemon off;" ] : nginx: Docker konteyneri başlatıldığında çalıştırılacak olan ana komuttur. Burada nginx, Nginx web sunucusunu başlatmak için kullanılan ana komuttur.
-g "daemon off;": Bu kısım, Nginx'in başlangıç ayarlarını belirtir. -g seçeneği, Nginx'e bir dizi küresel direktifi (global directive) iletmek için kullanılır. "daemon off;" direktifi ise Nginx'in daemon (arkaplan) olarak çalışmasını devre dışı bırakır. Yani Nginx, bu seçenekle birlikte ön planda çalışacaktır.

src/nginx/conf/default:

server { ... }: Bu blok, bir Nginx sunucu yapılandırmasını tanımlar. Her server bloğu, belirli bir sunucu veya sanal ana bilgisayar adını temsil eder.

listen 443 ssl;: Nginx'in 443 numaralı portu üzerinden HTTPS (ssl) trafiği dinlemesini sağlar.

listen [::]:443 ssl;: IPv6 desteği için 443 numaralı portu üzerinden HTTPS trafiği dinlemesini sağlar.

server_name: Bu sunucu bloğunun hangi alan adlarına (hostnamelere) hizmet vereceğini belirtir. Burada buyilmaz.42.fr domaini için yapılandırılmış.(yani bu sunucu ayarları buyilmaz.42.fr doamini için ayarlanmış demek)

SSL Sertifikası Ayarları

 ssl_certificate /etc/ssl/certs/inception.crt;: SSL sertifikasının dosya yolunu belirtir. Bu, HTTPS bağlantılarında kullanılan genel SSL sertifikasıdır.
 
 ssl_certificate_key /etc/ssl/private/inception.key;: SSL sertifikasının özel anahtar dosya yolunu belirtir. Bu, SSL sertifikasının özel anahtarıdır.

 
SSL Protokol Ayarı

 ssl_protocols TLSv1.3;: Nginx'in destekleyeceği SSL/TLS protokollerini belirtir. Burada sadece TLSv1.3 protokolü destekleniyor.
root: Bu direktif, Nginx'in sunacağı dosyaların kök dizinini belirtir. Bu örnekte /var/www/html dizini kök dizin olarak ayarlanmış, yani Nginx bu dizindeki dosyaları sunacak.
index: Bu direktif, istemci isteği üzerine sunucunun hangi dizininde hangi dosyanın varsayılan olarak gösterileceğini belirtir. Burada index.php belirtilmiş, yani Nginx istemci / yolu isteği geldiğinde index.php dosyasını arayacak.

location / { ... }: Bu blok, kök dizinin altındaki istemci isteklerini nasıl yönlendireceğimizi belirtir.

try_files $uri $uri/ =404;: İstemci isteğiyle eşleşen dosya veya dizin varsa direkt olarak sunar ($uri), yoksa 404 hatası döner.

location ~ \.php$ { ... }: Bu blok, .php uzantılı dosyalarla eşleşen istemleri nasıl işleyeceğimizi belirtir.

include snippets/fastcgi-php.conf;: PHP işlemi için gerekli olan FastCGI ayarlarını içeren dosyayı dahil eder.

fastcgi_pass wordpress:9000;: PHP isteklerini işlemek için Nginx'in WordPress'e yönlendireceği FastCGI sunucusunun adresini ve portunu belirtir.

proxy_connect_timeout 300s;, proxy_send_timeout 300s;, proxy_read_timeout 300s;, fastcgi_send_timeout 300s;, fastcgi_read_timeout 300s;: Bu direktifler, sunucu ile Nginx arasındaki bağlantı ve işlem zaman aşımını belirler. Burada her biri 300 saniye olarak ayarlanmış.

Bu yapılandırma, Nginx'i HTTPS üzerinden çalışacak şekilde ayarlar. server bloğu, belirtilen domain için SSL sertifikası ile HTTPS trafiği dinler, PHP dosyalarını işlemek için gerekli ayarları yapar ve statik dosyaları sunar. Bu şekilde, Nginx sunucusu, HTTPS üzerinden gelen istekleri doğru şekilde işleyebilecek yapıya getirilmiş olur.


server 
{
    listen 443 ssl;             # HTTPS trafiğini dinlemek için 443 portunu kullanır
    listen [::]:443 ssl;        # IPv6 desteği için HTTPS trafiğini dinler
    server_name buyilmaz.42.fr; # Bu sunucu ayarlarının buyilmaz.42.fr domaini için geçerli olduğunu belirtir

    ssl_certificate /etc/ssl/certs/inception.crt;   # SSL sertifikası dosya yolu
    ssl_certificate_key /etc/ssl/private/inception.key;  # SSL sertifikası özel anahtar dosya yolu
    ssl_protocols TLSv1.3;     # Kullanılacak SSL/TLS protokolü sürümü

    root /var/www/html;        # Web sayfalarının kök dizini

    index index.php;           # İstemciler / yolunu istediklerinde gösterecek dosya

    location / {
        try_files $uri $uri/ =404;  # İstemci isteğine göre dosyayı veya 404 hatası döndür
    }

    location ~ \.php$ 
    {
        include snippets/fastcgi-php.conf;   # PHP dosyaları için gerekli FastCGI ayarlarını dahil et
        fastcgi_pass wordpress:9000;         # PHP işlemlerini WordPress'e yönlendir
        proxy_connect_timeout 300s;          # Proxy bağlantı zaman aşımı
        proxy_send_timeout 300s;             # Proxy gönderme zaman aşımı
        proxy_read_timeout 300s;             # Proxy okuma zaman aşımı
        fastcgi_send_timeout 300s;           # FastCGI gönderme zaman aşımı
        fastcgi_read_timeout 300s;           # FastCGI okuma zaman aşımı
    }
}

listen 443 ssl;: Sadece IPv4 adreslerinden gelen HTTPS trafiğini dinler.

listen [::]:443 ssl;: Hem IPv4 hem de IPv6 adreslerinden gelen HTTPS trafiğini dinler.

IPv4 ile IPv6 farkı:

-Adres Uzunluğu: IPv4 32 bit, IPv6 ise 128 bit.

-Adres alanı(IPv6 daha geniş)


FastCGI (Fast Common Gateway Interface), web sunucusu (örneğin, Nginx veya Apache) ile CGI programları arasında hızlı ve etkili bir iletişim protokolüdür.


src/nginx/tools/nxstart.sh:

Bu betik, eğer $CERTIFICATES_OUT dosyası zaten mevcut değilse (yani daha önce bir sertifika oluşturulmamışsa), openssl aracılığıyla bir self-signed (öz imzalı) SSL/TLS sertifikası oluşturur. Self-signed sertifikalar genellikle geliştirme veya test amaçları için kullanılır ve gerçek dünya uygulamalarında genellikle güvenilir bir sertifika otoritesinden (CA) alınan sertifikalar kullanılır.Özetle, betik belirtilen domain için bir self-signed SSL/TLS sertifikası oluşturur ve bu işlemi yalnızca belirtilen sertifika dosyası henüz mevcut değilse gerçekleştirir.
openssl req: OpenSSL aracılığıyla bir sertifika isteği oluşturur ve yönetir.

-newkey rsa:2048: Yeni bir RSA 2048 bit anahtarı oluşturur.

-nodes: Anahtarın şifresiz olmasını sağlar (no DES encryption).

-keyout $CERTIFICATES_KEYOUT: Oluşturulan anahtar dosyasının adını ve yolunu belirtir.

-x509: Sertifika talebinin x509 formatında olmasını sağlar.

-days 365: Sertifikanın geçerlilik süresini 365 gün (1 yıl) olarak belirler.

-out $CERTIFICATES_OUT: Oluşturulan sertifika dosyasının adını ve yolunu belirtir.

-subj "/C=TR/ST=KOCAELI/L=GEBZE/O=42Kocaeli/CN=$DOMAIN_NAME": Sertifika altındaki konu (subject) alanını belirler. Bu alan Türkiye (TR), Kocaeli (KOCAELI), Gebze (GEBZE) gibi coğrafi ve kurumsal bilgileri içerir. CN=$DOMAIN_NAME ise sertifikanın geçerli olduğu ana alan adını (Common Name) belirtir.


x509: İmzalı sertifika oluşturur,

days: Geçerlilik süresini belirler,

newkey: Yeni RSA anahtarı oluşturur,

keyout-out: Anahtar ve sertifika çıktı yolunu belirler,

subj: Sertifika bilgilerini belirler

RSA: şifreleme algoritması
