# MCP-Agentic-Security-Review

[Canlı landing page](https://yusufarbc.github.io/MCP-Agentic-Security-Review/) • IEEE makalesi, medya kit’i ve 18 dosyalık referans kütüphanesi

![MCP mimarisi ve performans özetleri](media/MCP.png)

Repo, Model Context Protocol (MCP) ekosisteminin mimari, tehdit ve savunma boyutlarını inceleyen akademik çalışmayı içerir.
`index.html` depo içeriğini tek ekranda anlatırken `paper/`, `media/` ve `reference/` klasörleri ayrıntılı materyal sağlar.

## MCP neden kritik?

- **Evrensel adaptör:** LLM tabanlı ajanların araç, API, veri kaynağı ve cihazlarla konuşmasını JSON-RPC tabanlı ortak dilde yönetir.
- **Risk panoraması:** 4 aktör (kötü niyetli geliştirici/kullanıcı, dış saldırgan, yazılım hatası) ve 16 senaryo; 1.899 sunucu taramasında %7.2 genel açık, %5.5 araç zehirlenmesi ve %66 kod kokusu görüldü.
- **Benchmark bulguları:** MCPGAUGE her zaman fayda sağlamıyor; MCP-Universe/LiveMCP-101 < %60 başarı raporluyor; MCPToolBench++ format çeşitliliğini darboğaz olarak gösterirken AutoMalTool savunmaları aşabiliyor (MCP-Guard %96 doğrulukla yakalayabiliyor).
- **Savunma stratejileri:** IFC + taint tracking, sandbox profilleri, OAuth/mTLS + scoped token, plan tabanlı test + logging + red team, imzalı paket/SBOM ve OpenAPI→AutoMCP otomasyonu.

## Repo haritası

| Yol           | İçerik                                                                                                   |
| ------------- | --------------------------------------------------------------------------------------------------------- |
| `index.html`  | Landing page: depo yapısı, medya galerisi, referans tablosu, güvenlik özet ve YouTube demosu.             |
| `paper/`      | IEEEtran LaTeX kaynakları (`paper.tex`, `paper.pdf`, `protocol.png`, log/aux dosyaları).                  |
| `media/`      | Infografikler, NotebookLM posterleri, MCP host diyagramları, protokol şeması ve `Yapay_Zeka_Ajanlari.mp4`.|
| `reference/`  | 01–18 PDF; MCP-Guard, AutoMalTool, MCPGAUGE, MCPmed, AgentX, A2AS, ekonomik ajanlar vb. konular.          |
| kök dosyalar  | `.editorconfig`, `.gitattributes`, `.gitignore`, README ve GitHub Pages için gerekli altyapı.            |

## Media vitrininden seçmeler

| Görsel | Açıklama |
| ------ | -------- |
| `media/infografik.png` | NotebookLM üretimi agent protokolü sorun/çözüm infografiği (MCP/ACP/A2A/ANP). |
| `media/model.png` | MCP mimarisi + Python ile sunucu inşa adımlarını anlatan poster. |
| `media/post.jpeg` | MCP host, protokol katmanı ve 17 tehdit vektörünü sıralayan şema. |
| `media/diagram.png` | LLM → MCP istemcisi → çoklu sunucu bağlantısını gösteren akış. |
| `media/protocol.png` | MCP’nin IDE’ler, chat arayüzleri ve veri/araç katmanları arasında standart köprü oluşunu özetler. |
| `media/Yapay_Zeka_Ajanlari.mp4` | Yerel demo video (YouTube aynası `https://www.youtube.com/watch?v=MgGM5rkxL0c`). |

`media/README.md` her dosyanın yeniden kullanımı için kısa açıklamalar sunar; landing page’de kart olarak görüntülenir.

## Referans kütüphanesi (`reference/`)

- 18 PDF; MCP mimarisi, benchmark setleri (MCPGAUGE, MCPToolBench++, LiveMCP-101), AutoMalTool, MCP-Guard, MCPmed, AgentX, A2AS, AI Agents for Economic Research gibi alanları kapsar.
- `reference/Readme.md` tüm makaleler için Türkçe/İngilizce özet içerir. Yeni kaynak eklerken dosyayı numaralandırıp Readme’ye not düşmeniz yeterli.

## Makaleyi derlemek (`paper/`)

```bash
cd paper
pdflatex paper.tex
bibtex paper
pdflatex paper.tex
pdflatex paper.tex
```

`paper.log` hata analizi içindir; `protocol.png` makaledeki figürü temsil eder.

## Çalışma önerileri

1. `index.html`’i tarayıcıda açarak mevcut içerik özetini kontrol edin (GitHub Pages bağlantısı yukarıda).
2. Medya ve referanslar güncellendiğinde hem ilgili Readme dosyalarını hem de landing page bölümlerini senkron tutun.
3. MCP güvenlik bulguları (örn. LiveMCP-101 sonuçları, AutoMalTool logları) geldiğinde `paper/` veya yeni `reports/` dizinine ekleyin.
4. Gelecekte OAuth/mTLS referans konfigürasyonları, guard-model senaryoları ve SBOM üretim skriptleri için `docs/` veya `scripts/` klasörleri oluşturabilirsiniz.

README ve `index.html`, MCP-Agentic-Security-Review deposu için yüksek seviyeli rehber görevi görür; çalışma ilerledikçe güncel kalmaları gerekir.
