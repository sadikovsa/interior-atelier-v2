# Тайный сад / Secret Garden — фактическая дизайн-система

Оглавление: 1. Scope; 2. Типографика и цвет; 3. Главы и сетка; 4. Сцена; 5. Интерфейсы; 6. DEMO/SEO; 7. Проверки; 8. Токены.

## 1. Scope

Дневник обжитого дома. Статичные HTML/CSS/vanilla JS без сборщика; фактический код документирован 11 октября 2026 после PM ACCEPTED, QA_PASS_WITH_NOTES и независимого REVIEW_SHIP. Владелец принял hero и content/additions comps исторически; это не новое утверждение финального runtime.

Hero сохраняет системные шрифты/глобальные токены. Нижняя система scoped `.content-r3--garden` и использует свои `--c-*`. Старые три папки сохранены без изменений. HTML/fonts/images/vendor/main.js/tokens в QA round1 не менялись. BUG-QA-02: H1::before rgba(10,18,23,.6), inset−.15em −.3em/shadow0 0 .65em .25em; H1position:relative/isolation:isolate. Header scrimrgba(10,18,23,.7)/shadow0 0 .6rem .25rem: brand и navigation. Padding/геометрия/таймлайн не изменены; pixels изменены намеренно.

Current 175 input SHA256 `7a619e74dbb829cb788c252ca954495ff9fcc97126aa7fac7cf89b230bf26a72`. Эти DESIGN/design.json — non-runtime дополнения, исключённые из 175 измеренных файлов и Sites/Pages artifact. JSON содержит actual значения; не является повторным измерением.

## 2. Типографика и цвет

Hero heading `Arial, system-ui, sans-serif`, body `Arial, system-ui, sans-serif`. Ниже — **Literata + Commissioner**: H2weight400/line1.08/tracking-0.025em/max-width26ch; H3body60020px/1.3, prose≤65ch. Локальные declaredfont-face ranges: {"Literata": {"weight_range": "400 600", "font_display": "swap", "subsets": ["cyrillic-ext", "cyrillic", "latin"], "css": "assets/fonts/literata.css"}, "Commissioner": {"weight_range": "400 600", "font_display": "swap", "subsets": ["cyrillic-ext", "cyrillic", "latin"], "css": "assets/fonts/commissioner.css"}}. Используются Literata 400–500 и Commissioner 400–600; variable face range не означает применение всех весов. Два семейства×три subsetWOFF2, шесть файлов/две OFL на вариант, font-display:swap, CDN нет.

Основная нижняя палитра: {"background": "#213c31", "text": "#ede6d8", "muted": "#afbca4", "accent": "#afbca4"}. Остальные светлые/indigo/warm tokens — в `.studio/design.json`, извлечены из CSS, а не заменяют hero palette.

Mobile lower body17px/1.5/caption14/H234; ≥768 body18/caption15/H244; ≥1200 body20/H264. 

## 3. Девять глав и layout

1. Один дом. Разный ритм
2. Порядок без витрины
3. Под листвой
4. Комната продолжается на террасе
5. Фактуры, с которыми живут
6. Место за общим столом
7. Решаем вместе
8. Вопросы о жизни дома
9. Опишите привычный день

Это семь содержательных глав, два развёрнутых DEMO-кейса, FAQ4 и форма. Mobilechapter padding32px20px/gap20; tablet≥76840px32px/gap24; desktop≥120056px `max(64px,calc((100vw - 1312px)/2))`/gap32. Нижний gutter самостоятелен от глобального 80rem. Scroll-margin-top7rem; mobile одно/локальныепарные grid, tablet две и desktop асимметричныеполосы.

| Desktop≥1200 блок | Колонки |
|---|---|
| `.g-day` | `32fr 68fr` |
| `.g-storage` | `32fr 68fr` |
| `.g-forest` | `58fr 42fr` |
| `.g-terrace` | `74fr 26fr` |
| `.g-textures` | `37fr 28fr 35fr` |
| `.g-dining` | `64fr 36fr` |
| `.g-together` | `38fr 30fr 32fr` |

На 768px day/storage/forest/dining1fr1fr; textures1.1fr.85fr1fr. Forestroom4/5 переходит в 4/3 на desktop, окно 2/3≤280px; threshold полоса 4/1. Hero слева/H1max-width7.4em, clamp(2.25rem,5vw,5rem), weight500; ≤6002.25rem. Арочные слои идут по собственной архитектурной оси.

Фото в `.r3-media` defaultaspect3/2/object-fit:cover; отдельные портреты/детали имеют собственные proportions/object-position/static-scale. SVG схемы contain4/3, bench-node2/3. Полный master открывается по обычной gallerylink; crop не scroll-анимация. Lazyasyncdecode/srcset/widthheight и видимые AI/DEMOcaptions/alt сохранены; внутренние provenanceledger не удалять.

## 4. Tunnel / Zoom-through

Local GSAP/ScrollTrigger3.13.0 в `assets/js/vendor/`; `main.js` владеет scene/menu. Native scroll, один обратимый driverp0…1, pin `.scene-stage`/scrub:true/starttop top/invalidateOnRefresh/anticipatePin1. Backdrop/farplane3 имеют world scale; отдельно вырезанные plane1/2 ускоряются после выхода архитектурных силуэтов, затем открывается destination комната. Нет wheelhijack.

Ось: x=0.7057416267942583, y=0.41445270988310307. World scale `1+(18-1)*clamp(p/.94)^2`; near1 start0.34/multiplier`1+2*clamp((p-start)/(1-start))`; near2 start0.68/`1+1.4*…`. Camera travel к p.64; endX=−(axisX−.5)*canvasWidth/endY=−(axisY−.5)*canvasHeight. Mobile≤600startX=endX+stageWidth*.025, desktop0. Destination1…1.12 к p.94; hero UI fade.05….21, hero.inertp>.22. Scroll range 2.2viewportdesktop/1.4mobile≤600.

Canvasmax(100vw,177.683svh)×max(100svh,56.28vw), центр translate(−50%,−50%). Stage100svh/min-height36rem, ≤60033rem. Image-load/filtersrefresh триггеров. ReducedmatchMediacleanup снимает pin/transforms/opacity, inert=false; transitionsinstant. NoJS статичная architecture+destinationfallback и полныйконтент. Эти фазы относятся к фактической геометрии, не универсальный preset.

## 5. Компоненты

Menu<768 aria-expanded/Escape/focusrestore, WAAPIheight/opacity280ms, reduced0. Ссылки без подчёркивания; focusoutline3px/offset4, controls≥44px, formfields/submit≥52px.

Фильтры all, garden, forest: aria-pressed/count, два кейса; first case chapter с filters остаётся видимой при скрытом case, чтобы#projects→Все восстановил список. После изменения height ScrollTrigger.refresh; noJSfiltersdisabled/allcasesvisible.

Gallery17 ссылок, native dialog, requested отдельно от displayedactive. Next/Prev накапливаются относительно requested; после native Image.decode generation/dialog.open guard применяет image/alt/caption/counter одним выбором. Decodeerror сохраняет lastgood, resetrequestedactive/status; closeinvalidate+touchreset, delayedcloseevent не портит reopen. Arrowkeys/Tabtrap/nativeEscape/focusrestore, swipe горизонт>|48|px. Dialogwidthmin(1200px,100vw−32px), max94dvh/padding20/stickybar/overflowauto; imagecontainmax70dvh. ≤600width100vw−20px/padding12/image54dvh. NoJS прямая ссылка работает.

FAQ4 native detailsopen в HTML; JS закрывает и реверсирует от текущих height/opacity, cancel предыдущего WAAPI,280ms/cubic-bezier(.22,1,.36,1). Reducedinstant, noJSopen. Localform typebutton: trimname/message, contactemail с@/точкой или телефон 7–15 цифр допустимыхсимволов; inlineerrors/aria-invalid/firstinvalidfocus, successstatusfocus. SubmitpreventDefault, нет POST/storage/backend. NoJScheckdisabled+честноепояснение.

## 6. DEMO, SEO и доставка

Кейсы/схемы/бренды вымышлены; AI изображения подписаны. `[НУЖЕН ТЕКСТ ЮРИСТА]` сохраняется. Реальный запуск требует всех замен [PM§4](../interior-demo/.studio/v2/seo-qa-release/06-delivery.md); owner разрешил публичный DEMO, не превращение его в настоящий бизнес.

Уникальные title/description/canonical/OG/Twitter, neutralWebPageJSONLD, localicons/manifest/noSW. Canonical `https://interior-studio-v2.dilsan881.chatgpt.site/interior-atelier-v2/`. `noindex,follow` намерен, robots разрешает его получить, sitemap исключает noindexURL; нет fictitiousOrganization/LocalBusiness/reviews. Pagesdocs готов и локально проверен, APIenable403 «Resource not accessible by integration»: рассчитанный github.ioURL не live. SHA/privateSitepublicationproof фиксирует root отдельным release, не этот design документ.

## 7. QA, review и границы

[Fix03](../interior-demo/.studio/v2/seo-qa-release/03-fix-notes.md), [QA05a](../interior-demo/.studio/v2/seo-qa-release/05a-qa-recheck.md), [review05b](../interior-demo/.studio/v2/seo-qa-release/05b-design-review.md), [SEO04§8](../interior-demo/.studio/v2/seo-qa-release/04-seo-report.md), [PM06](../interior-demo/.studio/v2/seo-qa-release/06-delivery.md), [freshinventory](../interior-demo/.studio/v2/seo-qa-release/qa-recheck-evidence-index.json). Исторические FAIL/bugproof сохранены. Current native wheel3×390/1440 через 9 глав/назад Y0; rapidgallerynative-network6/6 +metadata/error/retry/reopen; noJS/reduced passed. Freshcontrast14targets прошли; Формы 320/360/390/768overflow0. Reviewer открыл шесть corrected кадров; прочие неизменные lower/motioncontracts reuseR3review, не новыйполныйпросмотр documenter.

Final isolated LH13.5.0/Chromium151/Node24.19.0 localhostHTTP/no-store: mobilePerformance69/LCP5945.78ms; desktop94/1639.22ms; CLS0/A100/BP100/SEO66intentionalnoindex. Simulated4Gmobile412×823CPU4, desktop1440×900CPU1. Mobile LCP>4s —известный P2advisory, не good mobile CWV; hard численногобюджетав AC небыло. INP/field CWV/FPS неизмерено/TBT не INP. MP425/26.64/25.24s —исторические R3 записи, current playback проверен, correctedpixels внихнет.

НЕ ПРОВЕРЕНО: Firefox/WebKit/Safari, physical phones, screen readers/assistive tech, OSIME/softkeyboard, toolbar200%zoom, все motion/hover/gradientcontraststates, полный WCAG, субъективнаяплавность/FPS, field CWV/INP, новый publicPagesdeployment. Reflow640CSSpx/DPR2 не toolbarzoom; A100 неполнаясертификация. Это документирование доказательств, не повтор browserQA.

## 8. Глобальные tokens фактического hero

| CSStoken | Значение |
|---|---|
| `--color-bg` | `#132B2E` |
| `--color-text` | `#E7DFC9` |
| `--color-muted` | `#B4C8BF` |
| `--color-accent` | `#C4AB83` |
| `--color-surface` | `#203A3A` |
| `--color-on-accent` | `#132B2E` |
| `--color-error` | `#FFB4AC` |
| `--color-focus` | `#C4AB83` |
| `--color-hero-text` | `#FFFFFF` |
| `--color-hero-scrim` | `rgba(10,18,23,0.84)` |
| `--font-heading` | `Arial, system-ui, sans-serif` |
| `--font-body` | `Arial, system-ui, sans-serif` |
| `--font-size-caption` | `0.8125rem` |
| `--font-size-body` | `1rem` |
| `--font-size-lead` | `1.25rem` |
| `--font-size-h2` | `clamp(2rem, 4vw, 3.75rem)` |
| `--font-size-hero` | `clamp(2.25rem, 4.4vw, 4.5rem)` |
| `--font-size-object` | `clamp(5rem, 22vw, 22rem)` |
| `--line-body` | `1.6` |
| `--line-heading` | `1.08` |
| `--space-1` | `0.25rem` |
| `--space-2` | `0.5rem` |
| `--space-3` | `1rem` |
| `--space-4` | `1.5rem` |
| `--space-5` | `2rem` |
| `--space-6` | `3rem` |
| `--space-7` | `5rem` |
| `--space-section` | `clamp(4rem, 8vw, 8rem)` |
| `--page-gutter` | `clamp(1.25rem, 4vw, 4rem)` |
| `--content-width` | `80rem` |
| `--radius-control` | `0px` |
| `--radius-panel` | `2px` |
| `--shadow-panel` | `0 16px 48px rgba(0,0,0,0.18)` |
| `--duration-control` | `180ms` |
| `--duration-panel` | `280ms` |
| `--ease-control` | `cubic-bezier(0.2, 0, 0, 1)` |
| `--ease-panel` | `cubic-bezier(0.22, 1, 0.36, 1)` |
| `--tap-size` | `44px` |

Файлы реализации: tokens/base/layout/components/motion/content-fonts/content-layout/content-interface.css, main/content.js, local fonts/OFL/manifest. Для нового проекта использовать отдельный scopedbrief и доказательства; эта память versionedinstructions, не изменениевесовмодели.
