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


## MCP ve İlgili Çalışmalar – Özet Listesi

1) **Model Context Protocol (MCP): Landscape, Security Threats, and Future Research Directions** (2025, arXiv:2503.23278) – Hou, X.; Zhao, Y.; Wang, S.; Wang, H.  
   - Abstract (EN): MCP’yi istemci–sunucu yaşam döngüsü ve 16’lı tehdit taksonomisiyle inceler; gerçek saldırı yüzeylerini örnekler ve her aşama için güvenlik önlemleri önerir; ekosistem benimsemesi ve araştırma boşluklarını tartışır.  
   - Özet (TR): MCP’nin dört aşamalı yaşam döngüsünü ve 16 senaryoluk tehdit modelini çıkarır; kötü niyetli geliştirici/kullanıcı, dış saldırgan ve kod hatası kaynaklı riskleri gösterir; her faz için uygulanabilir savunmalar ve gelecek araştırma alanları sunar.

2) **Advancing Multi-Agent Systems Through Model Context Protocol: Architecture, Implementation, and Applications** (2025, arXiv:2504.21030) – Krishnan, N.  
   - Abstract (EN): Çok etmenli sistemlerde bağlam paylaşımı, koordinasyon ve ölçeklenebilirlik için MCP tabanlı çerçeve önerir; kurumsal bilgi, ortak araştırma ve dağıtık problem çözmede vaka çalışmaları ve değerlendirme metodolojisi sunar.  
   - Özet (TR): Çok ajanlı senaryolarda MCP ile standart bağlam/araç paylaşımının verimliliğini gösterir; farklı alan vakalarıyla performans kazanımlarını ve araştırma fırsatlarını raporlar.

3) **A survey of agent interoperability protocols: MCP, ACP, A2A, ANP** (2025, arXiv:2505.02279) – Ehtesham, A.; Singh, A.; Gupta, G. K.; Kumar, S.  
   - Abstract (EN): MCP, ACP, A2A, ANP protokollerini etkileşim biçimi, keşif, güvenlik ve iletişim desenleri açısından karşılaştırır; aşamalı benimseme yol haritası sunar.  
   - Özet (TR): Dört protokolün (MCP/ACP/A2A/ANP) birlikte çalışabilirlik ve güvenlik özelliklerini kıyaslar; araç erişimi → yapılandırılmış mesajlaşma → yetki devri → merkeziyetsiz pazar adımlarını içeren yol haritası önerir.

4) **Model Context Protocol (MCP) at First Glance: Studying the Security and Maintainability of MCP Servers** (2025, arXiv:2506.13538) – Hasan, M. M.; Li, H.; Fallahzadeh, E.; Rajbahadur, G. K.; Adams, B.; Hassan, A. E.  
   - Abstract (EN): 1.899 açık kaynak MCP sunucusunun sağlık, güvenlik ve bakım durumunu inceler; 8 özgün zafiyet, %7.2 genel açık, %5.5 araç zehirlenmesi ve yaygın kod kokuları raporlar.  
   - Özet (TR): Büyük ölçekli tarama, MCP sunucularının yeni saldırı yüzeyleri (özgün zafiyetler, araç zehirleme) barındırdığını ve bakım sorunlarının yaygın olduğunu gösterir; MCP’ye özgü tespit araçlarına ihtiyaç vurgulanır.

5) **MCPmed: A Call for MCP-Enabled Bioinformatics Web Services for LLM-Driven Discovery** (2025, arXiv:2507.08055) – Flotho, M. ve ark.  
   - Abstract (EN): Bioinformatik web servislerini MCP’ye uyarlayarak makine-okunur arayüzler tanımlar; GEO/STRING/UCSC örnekleriyle keşif ve otomasyonu artırır; MCPmed topluluk girişimini önerir.  
   - Özet (TR): Bioinformatik API’lerini MCP katmanıyla zenginleştirerek LLM tabanlı ajanların veri keşfini ve yeniden üretilebilirliği artırmayı savunur; hafif geçiş şablonları sunar.

6) **Making REST APIs Agent-Ready: From OpenAPI to MCP Servers for Tool-Augmented LLMs** (2025, arXiv:2507.16044) – Mastouri, M.; Ksontini, E.; Kessentini, W.  
   - Abstract (EN): OpenAPI sözleşmelerinden otomatik MCP sunucusu üreten AutoMCP derleyicisini tanıtır; 50 API’de %76.5 başarı, küçük düzeltmelerle %99.9’a çıkar; MCP benimseme istatistiklerini sunar.  
   - Özet (TR): MCP sunucu kurulum maliyetini düşürmek için OpenAPI’den otomatik üretim önerir; başarısızlıkların çoğunun sözleşme kalitesiyle ilgili olduğunu gösterir ve MCP ekosistemi için otomasyonun mümkün olduğunu kanıtlar.

7) **MCPToolBench++: A Large Scale AI Agent Model Context Protocol MCP Tool Use Benchmark** (2025, arXiv:2508.07575) – Fan, S.; Ding, X.; Zhang, L.; Mo, L.  
   - Abstract (EN): 4k+ MCP sunucusuna dayalı geniş ölçekli araç-kullanım benchmark’ı oluşturur; tek ve çok adımlı çağrılarla LLM ajanlarının MCP performansını ölçer.  
   - Özet (TR): Gerçek MCP araçlarıyla büyük ölçekli test seti sunar; ajanların çok adımlı araç çağrılarındaki başarı ve bağlam sınırı sorunlarını ortaya koyar.

8) **MCP-Guard: A Defense Framework for Model Context Protocol Integrity in Large Language Model Applications** (2025, arXiv:2508.10991) – Xing, W.; Qi, Z.; Qin, Y.; Li, Y.; Chang, C. ve ark.  
   - Abstract (EN): MCP-Guard çok katmanlı tespit (statik tarama, derin model, hafif hakem LLM) ve 70k örnekli MCP-AttackBench’i tanıtır; saldırı promptlarını %96 doğrulukla yakalar.  
   - Özet (TR): MCP araç etkileşimlerini prompt enjeksiyonu/zehirlemeye karşı savunan üç aşamalı mimari ve geniş saldırı benchmark’ı sunar; yüksek doğrulukta tespit raporlar.

9) **Help or Hurdle? Rethinking Model Context Protocol-Augmented Large Language Models** (2025, arXiv:2508.12566) – Song, W.; Zhong, H.; Ding, Z.; Xue, J.; Li, Y.  
   - Abstract (EN): MCPGAUGE ile LLM–MCP etkileşimini proaktivite, uyum, etkinlik ve maliyet boyutlarında 20k+ API çağrısıyla değerlendirir; MCP entegrasyonunun sınırlamalarını ortaya koyar.  
   - Özet (TR): MCP entegrasyonunun her zaman performans kazandırmadığını, proaktif kullanım ve maliyet-aşımı sorunlarını gösteren kapsamlı bir benchmark sunar.

10) **MCP-Universe: Benchmarking Large Language Models with Real-World Model Context Protocol Servers** (2025, arXiv:2508.14704) – Luo, Z. ve ark.  
   - Abstract (EN): 11 gerçek MCP sunucusunu içeren 6 alanlık benchmark tasarlar; yürütme tabanlı değerlendiricilerle SOTA modellerin düşük başarılarını raporlar; uzun bağlam ve “bilinmeyen araç” zorluklarını vurgular.  
   - Özet (TR): Gerçek MCP sunucularıyla LLM ajanlarının zorlandığını, uzun bağlam ve araç tanımsızlığı nedeniyle başarı oranlarının düşük kaldığını gösterir.

11) **LiveMCP-101: Stress Testing and Diagnosing MCP-enabled Agents on Challenging Queries** (2025, arXiv:2508.15760) – Yin, M. ve ark.  
   - Abstract (EN): 101 gerçek dünya sorgusuyla çok araçlı, çok adımlı stres testi benchmark’ı sunar; plan tabanlı değerlendirme kullanır; frontier modellerde bile <60% başarı gösterir.  
   - Özet (TR): Gerçekçi görevlerle MCP ajanlarını zorlayarak planlama/koordinasyon hatalarını ve token verimsizliğini ortaya koyar; hata modlarını sınıflandırır.

12) **Model Context Protocols in Adaptive Transport Systems: A Survey** (2025, arXiv:2508.19239) – Chhetri, G. ve ark.  
   - Abstract (EN): Ulaşımda parçalı protokolleri MCP benzeri mimariyle birleştiren beşli taksonomi sunar; MCP’nin anlamsal birlikte çalışabilirlik ve bağlam paylaşımında uygunluğunu savunur.  
   - Özet (TR): Adaptif ulaşım sistemlerinde MCP’nin bağlam-farkındalığı ve standart entegrasyonla parçalanmayı azaltabileceğini, araştırma yol haritasıyla birlikte tartışır.

13) **AgentX: Towards Orchestrating Robust Agentic Workflow Patterns with FaaS-hosted MCP Services** (2025, arXiv:2509.07595) – Tokal, S. S. K. A.; Jha, V.; Eswaran, A.; Jayachandran, P.; Simmhan, Y.  
   - Abstract (EN): AgentX iş akışı (tasarımcı–planlayıcı–yürütücü ajanlar) tanıtılır; MCP sunucularının FaaS dağıtımıyla ReAct ve Magentic One’a karşı latency/maliyet/başarı kıyası yapılır.  
   - Özet (TR): MCP araçlarını FaaS’ta barındırarak çok aşamalı ajan iş akışını iyileştirir; başarı, gecikme ve maliyet analizleriyle fırsat ve zorlukları gösterir.

14) **Automatic Red Teaming LLM-based Agents with Model Context Protocol Tools** (2025, arXiv:2509.21011) – He, P.; Li, C.; Zhao, B.; Du, T.; Ji, S.  
   - Abstract (EN): AutoMalTool ile kötü niyetli MCP araçları üretip ajanları zehirleme saldırılarına karşı otomatik red teaming yapar; tespit mekanizmalarını aşabildiğini deneysel olarak gösterir.  
   - Özet (TR): MCP araç zehirlemesine karşı otomatik kırmızı takım çerçevesi sunar; yaygın ajanların manipüle edilebildiğini ve mevcut savunmaların yetersizliğini ortaya koyar.

15) **Asset Discovery in Critical Infrastructures: An LLM-Based Approach** (2025, Electronics 14(32):3267) – Coppolino, L.; Iannaccone, A.; Nardone, R.; Petruolo, A.  
   - Abstract (EN): *PDF’de özet bölümü otomatik çıkarılamadı; makale kritik altyapılarda varlık keşfi için LLM tabanlı yöntem ve güvenlik etkilerini inceliyor.*  
   - Özet (TR): Kritik altyapılarda varlık keşfini LLM destekli otomasyonla ele alır; güvenlik ve keşif doğruluğu için yöntemler sunar (ayrıntılı özet PDF’den manuel çıkarılmalı).

16) **Integrating Generative AI and Model Context Protocol (MCP) with Applied Machine Learning for Advanced Agentic AI Systems** (2025, Int. J. of Computer Trends and Technology) – Nilesh Bhandarwar  
   - Abstract (EN): *PDF ilk sayfada özet alınamadı; çalışma üretken AI’yı MCP ve uygulamalı ML ile birleştirerek ileri seviye ajan sistemlerine odaklanıyor.*  
   - Özet (TR): MCP + üretken AI + uygulamalı ML bileşimini ajan sistemleri için tartışır; özet metni PDF’den manuel çıkarılmalıdır.

17) **A Survey of the Model Context Protocol (MCP): Standardizing Context to Enhance Large Language Models (LLMs)** (2025, Preprints 202504.0245) – Singh, A.; Ehtesham, A.; Kumar, S.; Talaei Khoei, T.  
   - Abstract (EN): MCP’nin istemci–sunucu mimarisi, dinamik araç keşfi ve güvenlik mekanizmalarını mevcut parçalı API çözümlerine karşı inceler; uygulama alanları ve sınırlamaları tartışır.  
   - Özet (TR): MCP’yi standart bağlam katmanı olarak değerlendirir; birlikte çalışabilirlik kazanımlarını ve uzun vadeli performans belirsizliklerini vurgular; farklı sektörler için fırsat ve riskleri listeler.

18) **AI Agents for Economic Research** (2025, NBER Working Paper 34202) – Korinek, A.  
   - Abstract (EN): *PDF’den özet otomatik çıkarılamadı; çalışma ekonomi araştırmalarında AI ajanlarının kullanımını, metodolojik katkıları ve risklerini tartışıyor.*  
   - Özet (TR): Ekonomi araştırmasında AI ajanlarının rolü ve olası etkilerini ele alır; özet metni PDF’den manuel çıkarılmalıdır.
