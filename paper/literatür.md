**Model Bağlam Protokolü (MCP) Ekosisteminin Eleştirel Bir Güvenlik İncelemesi**

### Özet
Model Bağlam Protokolü (MCP), LLM’ler ile harici araçlar/kaynaklar arasında çift yönlü, şema odaklı iletişimi ve dinamik keşfi standartlaştırır. Entegrasyon parçalanmasını azaltırken, araç zehirleme, prompt enjeksiyonu, açıkta sunucu ve yanlış yapılandırma gibi yeni riskler üretir. Literatür, MCP sunucu yaşam döngüsünü (oluşturma, dağıtım, işletim, bakım) 16 faaliyet ve 16 tehdit senaryosuyla sınıflandırır; 1.899 sunucu taramasında %7,2 genel açık, %5,5 araç zehirleme riski ve %66 kod kokusu raporlanır.

### 1. Mimari Bileşenler ve Sınırlar
- **Host/Client:** LLM’yi barındırır, araç/kaynak keşfi yapar; harici veriye açılan yüzey.
- **Server:** Araçları/kaynakları JSON-RPC ile sunar; kimlik doğrulama ve izolasyon kalitesi kritik.
- **Tools:** Harici işlevler; açıklama alanları prompt enjeksiyonuna ve araç zehirlemeye açık.
- **Taşıma:** StdIO veya HTTPS/SSE; şifreleme ve OAuth/mTLS uygulaması saldırı yüzeyini belirler.

### 2. Tehdit Taksonomisi (4 Aktör, 16 Senaryo)
- Kötü niyetli geliştirici: Araç zehirleme, gölge sunucu/isim çakışması.
- Dış saldırgan: Dolaylı prompt enjeksiyonu, kurulum sahtekârlığı, açık sunucu istismarı.
- Kötü niyetli kullanıcı: STAC (ardışık düşük riskli araçlarla yüksek etkili eylem), sandbox kaçışı, oturum yeniden kullanımı.
- Yazılım/konfigürasyon hatası: Kimlik bilgisi sızıntısı, komut enjeksiyonu, zayıf TLS/OAuth ayarları.

### 3. Ampirik Bulgular
- 1.899 açık kaynak MCP sunucusunda: %7,2 genel açık, %5,5 araç zehirleme, %66 kod kokusu, %14,4 hata kalıbı (Hasan vd., 2025).
- Geleneksel statik analiz MCP-özel açıkları kaçırıyor; MCP’ye özgü tarama araçlarına ihtiyaç var.

### 4. Performans ve Benchmark’lar
- **MCPGAUGE:** MCP entegrasyonu her zaman fayda getirmiyor; düşük proaktivite, yüksek maliyet/gider.
- **MCP-Universe, LiveMCP-101:** Gerçek sunucularda frontier modeller < %60 başarı; uzun bağlam ve bilinmeyen araç hataları belirgin.
- **MCPToolBench++:** 4k+ sunucu, geniş araç kullanımı; format çeşitliliği ve bağlam penceresi dar boğaz.
- **Red team:** AutoMalTool mevcut savunmaları aşabiliyor; MCP-Guard çok katmanlı tespitte %96 doğruluk.

### 5. Savunma Stratejileri
- **IFC + taint-tracking:** Zehirli girdilerin kritik eylemleri tetiklemesini engelle.
- **Sandboxing:** Araç erişimini dosya/ağ/sistem komutlarıyla sınırla; dağıtıma özel profil.
- **Kimlik/taşıma:** TLS/mTLS, OAuth 2.1 + kaynak göstergeleri; scoped, kısa ömürlü token.
- **Gözlem:** Plan tabanlı testler (LiveMCP-101), detaylı günlük/anomali takibi, periyodik kırmızı takım.
- **Tedarik zinciri:** İmzalı paket, sürüm pinleme, SBOM; açıklama/şema bütünlük doğrulaması.

### 6. Öneriler
1) CI/CD’de MCP-özel tarama (açıklama zehirleme + şema tutarlılığı, semantik tespit).  
2) İmzalı paket, sürüm pinleme, SBOM ve her yayında bütünlük doğrulaması.  
3) Yüksek etkili eylemlerde guard modeli + insan onayı; araç başına kapsam/kuota ve scoped kimlik bilgisi.  
4) Canlıya çıkmadan plan tabanlı stres testleri ve AutoMalTool tarzı kırmızı takım koşuları.  
5) OpenAPI’den otomatik sunucu üretimiyle manuel yapıştırma hatalarını azalt; spek kalitesini iyileştir.

### Kaynaklar (18 çalışma)
Hou 2025; Krishnan 2025; Ehtesham 2025; Hasan 2025; Flotho 2025; Mastouri 2025; Fan 2025; Xing 2025; Song 2025; Luo 2025; Yin 2025; Chhetri 2025; Tokal 2025; He 2025; Singh 2025; Bhandarwar 2025; Coppolino 2025; Korinek 2025.
