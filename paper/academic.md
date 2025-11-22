**Model Bağlam Protokolü (MCP) Ekosisteminin Eleştirel Bir Güvenlik İncelemesi**

| Yazar(lar) | Çalışma | Yayın | Yıl |
| --- | --- | --- | --- |
| Derleme | Literatür sentezi | ArXiv/Preprint | 2025 |

---

### Özet
Model Bağlam Protokolü (MCP), LLM’ler ile harici araçlar/kaynaklar arasında çift yönlü, şema odaklı iletişim ve dinamik keşif sağlayan açık bir standarttır. Protokol, entegrasyon parçalanmasını azaltırken araç zehirleme, prompt enjeksiyonu ve yanlış yapılandırma gibi yeni güvenlik riskleri oluşturur. Bu metin, mimariyi, tehdit taksonomisini (4 aktör, 16 senaryo), 1.899 sunuculuk ampirik bulguları, benchmark sonuçlarını ve savunma/tedarik zinciri önerilerini birleştirir.

---

### 1. Mimari ve Saldırı Yüzeyi
- Bileşenler: Host/Client (LLM), Server (araç/kaynak sağlayıcı), Tools (işlevler), Taşıma (StdIO veya HTTPS/SSE, JSON-RPC 2.0).
- Yaşam döngüsü: Oluşturma → Dağıtım → İşletim → Bakım; her faz yeni açıklar tanıtabilir (özellikle açıklama/şema zehirlemesi, sandbox kaçışı, yapılandırma sapması).
- Görsel referanslar: `protocol.png` (mimari), `model.png` (etkileşim ve risk noktaları), `diagram.png` (akış ve enjeksiyon noktaları).

### 2. Tehdit Taksonomisi (4 aktör, 16 senaryo)
- Kötü niyetli geliştirici: Araç zehirleme (açıklamaya gizli talimat), sahte/shadow server, isim çakışması.
- Dış saldırgan: Dolaylı prompt enjeksiyonu (RAG/issue/dosya), kurulum sahtekârlığı, açıkta sunucu istismarı.
- Kötü niyetli kullanıcı: STAC (ardışık düşük riskli araçlarla yüksek etkili eylem), sandbox kaçışı, yetkisiz erişim/oturum yeniden kullanımı.
- Yazılım hatası/konfigürasyon: Kimlik bilgisi sızıntısı, komut enjeksiyonu, yanlış TLS/OAuth ayarları.

### 3. Ampirik Bulgular (1.899 MCP sunucusu)
- %7,2 genel güvenlik açığı; %5,5 MCP-özel araç zehirleme riski; %66 kod kokusu; %14,4 hata kalıbı. (Hasan vd., 2025)
- Geleneksel statik analiz (örn. SonarQube) MCP-özel açıkları kaçırıyor; MCP’ye özgü tarayıcı ihtiyacı (`mcp-scan`).

### 4. Benchmark ve Dayanıklılık
- MCPGAUGE (Song vd., 20k API): MCP entegrasyonu her zaman performans artışı getirmiyor; düşük proaktivite, maliyet/gider yüksek.
- MCP-Universe, LiveMCP-101: Gerçek sunucularla frontier modeller < %60 başarı; uzun bağlam ve bilinmeyen araç hataları belirgin.
- MCPToolBench++: 4k+ sunucuyla geniş ölçekli araç kullanımı; format çeşitliliği ve bağlam penceresi dar boğaz.
- Red team: AutoMalTool (He vd.) otomatik kötü araç üretimiyle mevcut savunmaları aşabiliyor; MCP-Guard (Xing vd.) çok katmanlı tespitte %96 doğruluk.
- Otomasyon: AutoMCP (Mastouri vd.) OpenAPI→MCP derleyicisi; küçük spek düzeltmeleriyle %99,9 başarı. AgentX (Tokal vd.) FaaS barındırma maliyet/gecikme kıyasları.

### 5. Savunma ve İyi Uygulamalar
- Sistem düzeyi: IFC + dinamik taint-tracking; sandboxing ile dosya/ağ yetkilerini sınırla; plan doğrulama/guard modeliyle yüksek etkili adımlar.
- Taşıma/kimlik: TLS/mTLS, OAuth 2.1 + kaynak göstergeleri (RFC 8707), scoped token ve kısa ömür.
- Gözlem: Plan tabanlı değerlendirme (LiveMCP-101), detaylı günlükleme/telemetri, periyodik kırmızı takım (AutoMalTool benzeri).
- Tedarik zinciri: İmzalı paket, sürüm pinleme, SBOM; açıklama ve şema bütünlük doğrulaması; dağıtıma özel sandbox profilleri.

### 6. Eylem Odaklı Öneriler
1) CI/CD’de MCP-özel tarama (açıklama zehirleme + şema tutarlılığı, semantik tespit). 
2) İmzalı paket + sürüm pinleme + SBOM, her yayında bütünlük doğrulaması. 
3) Yüksek etkili eylemlerde guard modeli + insan onayı; araç başına kapsam/kuota + scoped kimlik bilgisi. 
4) Canlıya çıkmadan plan tabanlı stres testleri ve AutoMalTool tarzı kırmızı takım koşuları. 
5) OpenAPI’den otomatik sunucu üretimiyle manuel yapıştırma hatalarını azalt, spek kalitesini iyileştir.

### 7. Kaynakça (18 çalışma)
Hou 2025; Krishnan 2025; Ehtesham 2025; Hasan 2025; Flotho 2025; Mastouri 2025; Fan 2025; Xing 2025; Song 2025; Luo 2025; Yin 2025; Chhetri 2025; Tokal 2025; He 2025; Singh 2025; Bhandarwar 2025; Coppolino 2025; Korinek 2025.
