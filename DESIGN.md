# Тайный сад / Secret Garden — фактическая дизайн-система

Оглавление: 1. Scope; 2. Типографика и цвет; 3. Главы и сетка; 4. Сцена; 5. Интерфейсы; 6. Публичные тексты/SEO; 7. Проверки; 8. Токены.

## 1. Scope

Дневник обжитого дома. Статичные HTML/CSS/vanilla JS; actual active source документирован 12 октября 2026. Сохранены принятые композиции hero, нижние системы, H1/H2, изображения, шрифты, геометрия и пространственный GSAP driver. Корневые snapshots синхронизирует диспетчер; этот документ относится к `projects/interiors/interior-atelier-v2/`.

Новый прямой запрос владельца разрешил убрать публичные AI/DEMO-подписи и технические заглушки. Это scoped override старой обязанности видимой маркировки только для трёх active v2 и comparison. Внутренние provenance/исторические отчёты сохранены; концепции не представлены завершёнными заказами реальных клиентов. Даты/контакты/отзывы/награды/юридические утверждения не придуманы.

Текущий public-runtime inventory SHA256 `50944ab6d412b615a2aac647b6d872424ca0773bd0d2d5c50198d52c297de810`; метод и source/build inventories — в SOURCE-CHECKPOINT.json. Исторический175-input hash `7a619e74dbb829cb788c252ca954495ff9fcc97126aa7fac7cf89b230bf26a72` относится к прежнему fullSEO/QA и не описывает новую HTML/form/SVG редактуру. DESIGN/design.json — non-runtime документы, исключённые из public dist.

Сохранённая QA-коррекция11октября: BUG-QA-02: H1::before rgba(10,18,23,.6), inset−.15em −.3em/shadow0 0 .65em .25em; H1position:relative/isolation:isolate. Header scrimrgba(10,18,23,.7)/shadow0 0 .6rem .25rem: brand и navigation. Padding/геометрия/таймлайн не изменены; pixels изменены намеренно. Новая редактура не меняет её pixels/таймлайн. Старые first-generation варианты и архивы не правились.

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

Это семь содержательных глав, два развёрнутых интерьерных концепта, FAQ4 и форма. Mobilechapter padding32px20px/gap20; tablet≥76840px32px/gap24; desktop≥120056px `max(64px,calc((100vw - 1312px)/2))`/gap32. Нижний gutter самостоятелен от глобального 80rem. Scroll-margin-top7rem; mobile одно/локальныепарные grid, tablet две и desktop асимметричныеполосы.

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

Фото в `.r3-media` defaultaspect3/2/object-fit:cover; отдельные портреты/детали имеют собственные proportions/object-position/static-scale. SVG схемы contain4/3, bench-node2/3. Полный master открывается по обычной gallerylink; crop не scroll-анимация. Lazy/async decode, srcset и width/height сохранены; caption/alt теперь содержат обычные описания без публичных AI/DEMO-пометок. Внутренний provenance-ledger не удалять.

## 4. Tunnel / Zoom-through

Local GSAP/ScrollTrigger3.13.0 в `assets/js/vendor/`; `main.js` владеет scene/menu. Native scroll, один обратимый driverp0…1, pin `.scene-stage`/scrub:true/starttop top/invalidateOnRefresh/anticipatePin1. Backdrop/farplane3 имеют world scale; отдельно вырезанные plane1/2 ускоряются после выхода архитектурных силуэтов, затем открывается destination комната. Нет wheelhijack.

Ось: x=0.7057416267942583, y=0.41445270988310307. World scale `1+(18-1)*clamp(p/.94)^2`; near1 start0.34/multiplier`1+2*clamp((p-start)/(1-start))`; near2 start0.68/`1+1.4*…`. Camera travel к p.64; endX=−(axisX−.5)*canvasWidth/endY=−(axisY−.5)*canvasHeight. Mobile≤600startX=endX+stageWidth*.025, desktop0. Destination1…1.12 к p.94; hero UI fade.05….21, hero.inertp>.22. Scroll range 2.2viewportdesktop/1.4mobile≤600.

Canvasmax(100vw,177.683svh)×max(100svh,56.28vw), центр translate(−50%,−50%). Stage100svh/min-height36rem, ≤60033rem. Image-load/filtersrefresh триггеров. ReducedmatchMediacleanup снимает pin/transforms/opacity, inert=false; transitionsinstant. NoJS статичная architecture+destinationfallback и полныйконтент. Эти фазы относятся к фактической геометрии, не универсальный preset.

## 5. Интерфейсы и локальное описание

Сохранённые menu/filter/gallery/FAQ handlers до form block byte-identical с исходным checkpoint. Menu<768: aria-expanded/Escape/focus restore,280msheight/opacity/reduced0. Controls≥44px, поля/основная кнопка≥52px; ссылки без подчёркивания, focusoutline3px/offset4px. Фильтры aria-pressed/count, два проекта; firstcasechapter сfilter остаётся доступной для#projects→Все; после изменения высоты ScrollTrigger.refresh. NoJSвсе проекты видны, filterdisabled.

Gallery17ссылок: native dialog; requested отдельно от displayedactive; nativeImage.decode + generation/dialog.open guard применяет image/alt/caption/counter одним завершённым выбором. Ошибка сохраняет lastgood/resetrequested/status. Closeinvalidate и guard delayedclose при reopen; Arrowkeys/Tabtrap/nativeEscape/focusrestore/swipe>|48|px. Dialogwidthmin(1200px,100vw−32px)/max94dvh; imagecontainmax70dvh; ≤600width100vw−20px/image54dvh. NoJSпрямые ссылки работают. FAQ4 native detailsopen; JSWAAPIheight/opacity280ms/cubic-bezier(.22,1,.36,1), cancel/reverse от текущего состояния; reducedinstant/noJSopen.

**Новая форма** готовит описание, не отправляет заявку. Typebutton «Подготовить описание»; прежняя trim/name/message и email/phone7–15digits validation сохранена. Inlineerrors/aria-invalid/firstinvalidfocus; submitpreventDefault. После успеха появляется editabletextarea «Подготовленное описание» и «Скопировать», «Сохранить TXT», «Выделить текст». Шаблон `Привычный день — Secret Garden` содержит имя/контакт/исходноеописание; пользователь может переписать получившийся текст.

Экспорт берёт **текущее edited textarea.value**, а не исходные поля/кеш. Clipboardуспех только после fulfilledwriteText; rejection/недоступность дают инструкцию и focus/select для ручного копирования. generation/exportRequest/visibility/currentvalue guard не применяет устаревший asyncstatus после правок/регенерации/нового экспорта. Пробельный текст не копируется/не скачивается. Изменение исходных полей скрывает и очищает draft; его правки очищают exportstatus. НетPOST/network/backend/localStorage/sessionStorage. NoJSdisabledpreparation+«Чтобы подготовить описание, включите JavaScript».

TXT: Blobtext/plain;charset=utf-8 по явному нажатию, temporaryanchor/downloadfilename `secret-garden-interior-brief.txt`, anchorremove/revokeObjectURL через1000ms. Success «TXT-файл передан браузеру для сохранения» не утверждает сохранение на устройстве. Heightchangesrefresh/restore scrollY instant; лишних refresh при повторных скрытых пустых input нет.

Добавлены только четыре scopedCSSправила: visiblebriefgrid/gap20px, briefH3margin-bottom0, flexactionswrap/gap12px, cleanfooter navgrid-column1/-1. Цвета/семейства/controlstyles наследуются от прежней темы; новый общий stylekit/таймлайн не добавлен. Footer —профиль и три работающихanchors.

## 6. Публичные тексты и SEO

Маркировки AI/DEMO/«демонстрационные данные», публичная provenance-памятка, блок подготовки к запуску и legalplaceholder удалены по явному запросу. Caption/alt/aria/embeddedJSON/meta/manifest/SVGtitle имеют обычные описания; нейроизображения не названы фотографиями выполненных заказов. Содержательные cautions о замерах, материале, устойчивости и узлах сохранены. SVGизменяют только восемь titleстрок по трём пакетам; геометрия/ledger сохранились.

Title: «Secret Garden — интерьер дома и повседневные сценарии». Canonical `https://sadikovsa.github.io/interior-atelier-v2/`. OG/Twitter/WebPageJSONLD/localicons/manifest, robots и намеренный `noindex,follow` сохранены. Отсутствие публичных пометок не означает фактологически подтверждённый коммерческий запуск; индексация/юридические данные/backend требуют отдельного scope. Не появился ложный Organization/LocalBusiness/review/реальный контакт.

Три standalonePages уже существуют. Редактура12октября republish выполняется диспетчером после checks с отдельными source/pagesSHA и actualHTTP/browserproof; прежний API403 —исторический статус одного App, не текущий globalblocker. Существующий liveURL не доказывает загрузку новой редакции. PrivateSites обновляется отдельно, его sourceSHA отличается от GitHubSHA.

## 7. Доказательства и границы

Новая редактура: [запрос](../../../work/interior-cleanup/00-request.md), [copy](../../../work/interior-cleanup/02-copy.md), [buildnotes](../../../work/interior-cleanup/03-build-notes.md), [статическиеchecks](../../../work/interior-cleanup/static-result.json). Localrefs/uniqueIDs/JSON/XML/noindex, source/dist/deterministicbuild PASS; semanticpublicmarkers0. Staticfrozen geometry/H1/H2/raster/fonts/icons/vendor/main.js, SVGgeometry и CSS/JSunaffectedprefix подтверждены. HTMLbody/SVGtitles/formruntime изменены —не body/allassets byte-identical.

[Текущий focused QA](../../../work/interior-cleanup/05-qa-report.md): **QA_PASS_WITH_NOTES**, BLOCKER0/MAJOR0/MINOR0. Chromium151/Linux:12fresh normal contexts (3×320×844/390×844/768×900/1440×900) и3noJS+3reduced390×844. Все прошли native wheel через9глав и обратноY0 без горизонтальногоoverflow/markers;6functionalflows390/1440 проверили меню/filter/gallery/FAQ и новую форму. Source/dist bytes и frozenbaseline paths проверены отдельно; новый body/SVGtitles/form не называются byte-identical.

Настоящие clipboardwrite/read и TXTdownload/saveAs/readUTF8 в6flows совпали с текущим editedtextarea.value, включая Unicode/newline/emoji. Clipboardpermissions granted тестом. ControlledNotAllowedError дал focus/select и ручную инструкцию; пробельный draft не экспортировался. Два heldpromise race на каждомflow проверили edit и originalinput→regen без stalestatus. Изменение исходного поля инвалидировало output; Enter не навигировал, nonGET0/storageunchanged. Кнопка «Выделить текст» отдельно **НЕ ПРОВЕРЕНА**; общий selectText реально выполнен clipboardfailure-веткой. Exportasync races отдельно в reducedcontext не повторялись.

Fresh48normalPNG+6fallbackPNG; QA реально открыл три кадра, независимый reviewer выполняется отдельно. [Rawresults](../../../work/interior-cleanup/qa/hosting-regression.json) и [readonlychecks](../../../work/interior-cleanup/qa/static-readonly.json). Documenter не запускал browser и не выдаёт сохранённые screenshots за собственное художественное review. Новые motionrecordings выполняет QA отдельно; dimensions/duration manifest и actualpublicationproof фиксирует root. Старый validation-only PASS не доказывал новый editable/exportworkflow.

FullSEO/QA11октября остаются историческими: targetedbugfixes/nativewheel/review и изолированныеLH относятся к предыдущему artifact, reuse только неизменённых contracts. Нового LH/fullQA/FPS/fieldINP не запускали; прежний mobileLCP4.5–5.95s остаётся историческим ограничением, не измерением этой редакции. TBTнеINP/A100неполныйWCAG. Crossbrowser/physicalphones/screenreaders/OSIME/toolbarzoom/allmotioncontrast/FPS/fieldCWV/INP НЕ ПРОВЕРЕНО этим focusedrelease.

Новая publicationverification/reviewer делается root отдельными доказательствами. Source/build/checkpoint inventories и provenance сохраняются внутри пакетов/history; publicdist исключает внутренние instructions/reports.

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
