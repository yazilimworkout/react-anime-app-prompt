# YazilimWorkout | Anime: Sıfırdan Uygulama İsteği

Bu brief’e göre çalışan anime keşif sitesini sıfırdan oluştur. Projeyi kur, sayfaları ve işlevleri uygula, ardından üretim derlemesini çalıştır.

## Teknoloji ve başlangıç

- Vite ile yeni bir React + TypeScript uygulaması oluştur. Bileşen ve veri dosyalarını TSX/TS olarak yaz.
- Tailwind CSS’i kurup yapılandır. İkonlarda Lucide React kullan.
- `/signin` ve `/signup` sayfaları için React Router kullan.
- Anime kataloğunu `src/data/anime.ts` içinde, aşağıdaki JSON verisini temel alarak oluştur.
- TanStack Query’yi yalnızca geçici fragman isteğinin yükleme durumunda kullan.

## Tasarım

Marka adı **YazilimWorkout | Anime**. Arayüz siyah, beyaz ve Netflix kırmızısı (`#E50914`) üzerine kurulu olsun. Sıkı aralıklar, küçük tipografi ve keskin köşeler kullan; rengi anime görselleri getirsin.

Üstte ince ve sabit bir navbar olsun. Marka, Discover, Top 6, Films, Hidden Gems, tür filtresi, arama, kayıtlılar ve hesap bağlantısını içersin. Mobilde gezinme kolayca kullanılabilsin.

Navbarın hemen altında tam genişlikte **A Silent Voice** hero alanı yer alsın. Arka plan görseli alanın tüm genişliğini ve yüksekliğini kaplasın. Başlık ve bilgiler görselin üzerine konumlansın; okunurluk için koyu degrade ekle. `heroFeature` kaydındaki görseli, puanı ve metinleri kullan.

## Katalog

JSON’daki 11 bölümü belirtilen sırayla göster. Her bölüm başlığının altında, `itemIds` içinde listelenen her anime için bir poster kartı render et. Yalnızca başlık gösterip kartları boş bırakma. Toplam 102 bölüm-kart yerleşimi vardır.

- `ranked` bölümlerinde posterlerin altına büyük sıra numaraları koy.
- `grid` bölümlerinde masaüstünde altı sütun kullan; tablet ve telefonda sütun sayısını azalt.
- `strip` bölümlerinde daha kısa, yatay kartlar kullan.
- Bölümdeki anime kimliklerini katalogdaki kayıtlarla eşleştir. Her kartta görsel, başlık, puan ve tür göster.
- Görsel yüklenmezse kırık resim veya boş kutu yerine anime adını gösteren yedek sun.
- `ranked-two` bölümünden sonra Frieren bandını, `action` bölümünden sonra Spy × Family bandını yerleştir.

Sayfa uzunsa kullanıcı aşağı kaydırdıkça yeni bölümleri ekle ve içerik bitmeden küçük bir yükleme göstergesi çıkar. Büyük siyah boşluk bırakma. Kartlar görünür alana yaklaşınca hafifçe belirebilir; gözlemci çalışmasa veya hızlı kaydırmada olay kaçsa bile kartlar görünür kalmalı. Hareket azaltma tercihini destekle.

Kart seçilince seçilen animeye ait görsel ve temel bilgileri içeren modal aç. Fragman alanı şimdilik geçici olsun: TanStack Query ile `https://example.com` adresini iste; yanıt beklenirken spinner göster, yanıt geldikten sonra fragman verisinin henüz bağlanmadığını belirt. Jikan veya YouTube araması ekleme; fragman kaynağını daha sonra biz belirleyeceğiz.

## Giriş, kayıt ve hesap menüsü

`/signin` ve `/signup` sayfalarını ekli görselin düzenine göre hazırla: ekranı kaplayan anime kolajı, koyu katman, ortada siyah form paneli, üstte YazilimWorkout | Anime logosu, beyaz etiketler, koyu alanlar ve kırmızı ana buton. Kolaj görsellerini aşağıdaki katalogdan al.

- Giriş sayfası kullanıcı adı veya e-posta, parola, göster/gizle kontrolü, parola kurtarma açıklaması ve kayıt bağlantısı içersin.
- Kayıt sayfası kullanıcı adı, e-posta, parola, parola onayı ve giriş bağlantısı içersin.
- Hesapları ve oturumu şimdilik `localStorage` içinde tut. Parolaları düz metin yerine tuzlanmış PBKDF2 özeti olarak sakla. Girişte kullanıcı adı veya e-posta kabul et.
- Oturum kapalıyken navbar’da Sign In göster. Oturum açılınca kullanıcının adını avatarın hemen soluna yaz. Avatar olarak şu görseli kullan: https://i.pinimg.com/736x/c0/35/c9/c035c9f1ce89541ff98670867ea2534f.jpg.
- Avatara tıklanınca Sign Out seçeneği olan bir hesap menüsü aç. Dışarı tıklama veya Escape menüyü kapatsın. Sign Out oturumu `localStorage` içinden silsin ve navbarı oturum kapalı görünümüne döndürsün.
- Kayıt veya giriş başarılı olunca Discover’a dön. `/signin` ve `/signup` adreslerinin doğrudan açılması ve yenilenmesi çalışmalı.

## README dosyaları

`README.md` ve `READMEç.md` dosyalarını da oluştur. İkisi de Türkçe ve İngilizce içerik sunsun. Her iki dosyanın en üstünde `Türkçe | English` dil seçimi bulunsun; bağlantılar dosyanın aşağısındaki ilgili dil bölümüne atlasın. Kurulum, çalıştırma ve derleme komutlarını, teknoloji yığınını, ana özellikleri, rotaları ve yerel hesap davranışını iki dilde açıkla. Bağlantıların doğru bölümlere gittiğini kontrol et.

## Veri kaynağı

Proje kökündeki `json-data.json` dosyası katalog verilerinin tek ve asıl kaynağıdır. Önce bu dosyayı oku ve doğrula: 48 anime kaydı, 11 bölüm ve 2 öne çıkan bant olmalı; her bölümdeki anime kimlikleri katalog kayıtlarıyla eşleşmeli. Dosyadaki başlık, puan, görsel, tür ve sıralamaları değiştirme.

JSON içeriğini güçlü TypeScript tipleriyle `src/data/anime.ts` içinde uygulamanın kullanacağı veri setine dönüştür. Uygulama bileşenleri katalog ve bölüm verilerini bu TypeScript modülünden alsın. `json-data.json` dosyasını proje kökünde koru ve dönüşümün tekrarlanabilir olmasını sağla. Katalog için uzak API kullanma.
## Tamamlandı sayılması için

- 11 bölümün tümü doğru sırada ve 102 bölüm-kart yerleşimi eksiksiz görünmeli.
- Hero ve iki bant doğru görselleri kullanmalı; başarısız poster görselleri yedek göstermeli.
- Arama, tür filtresi, navbar, kart modalı, aşağı kaydırdıkça bölüm ekleme, giriş, kayıt, hesap menüsü ve çıkış çalışmalı.
- Masaüstü ve mobilde yatay taşma ya da siyah boş bölüm olmamalı.
- Uygulamanın üretim derlemesini çalıştır ve derleme hatalarını gider.