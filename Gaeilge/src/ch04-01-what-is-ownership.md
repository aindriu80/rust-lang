## Cad is Úinéireacht ann?

Is sraith rialacha é _Úinéireacht_ a rialaíonn conas a bhainistíonn clár Rust cuimhne.
Caithfidh gach clár an bealach a úsáideann siad cuimhne ríomhaire a bhainistiú agus iad ag rith.
Tá bailiúchán truflais ag teangacha áirithe nach n-úsáidtear a thuilleadh go minic
cuimhne de réir mar a ritheann an clár; i dteangacha eile, ní mór don ríomhchláraitheoir go sainráite
an chuimhne a leithdháileadh agus a shaoradh. Úsáideann Rust an tríú cur chuige: déantar cuimhne a bhainistiú
trí chóras úinéireachta le sraith rialacha a sheiceálann an tiomsaitheoir. Más rud é
sáraítear aon cheann de na rialacha, ní thiomsóidh an clár. Níl aon cheann de na gnéithe
Cuirfidh úinéireachta moill ar do chlár agus é ar siúl.

Toisc gur coincheap nua í úinéireacht do go leor ríomhchláraitheoirí, tógann sé roinnt ama
dul i dtaithí ar. Is é an dea-scéal ná dá mhéad taithí a éiríonn tú le Rust
agus rialacha an chórais úinéireachta, is amhlaidh is fusa duit go nádúrtha é
cód a fhorbairt atá sábháilte agus éifeachtach. Coinnigh ort!

Nuair a thuigeann tú úinéireacht, beidh bunús láidir tuisceana agat
na gnéithe a dhéanann Rust uathúil. Sa chaibidil seo, foghlaimeoidh tú úinéireacht trí
ag obair trí roinnt samplaí a dhíríonn ar struchtúr sonraí an-choitianta:
teaghráin.

> ### An Cruach agus an Charn
>
> Ní éilíonn go leor teangacha ríomhchláraithe duit smaoineamh ar an gcruach agus ar an
> carn go minic. Ach i dteanga ríomhchlárúcháin córais mar Rust, cibé acu a
> tá luach ar an gcruach nó bíonn tionchar ag an gcarn ar iompar na teanga agus cén fáth
> caithfidh tú cinntí áirithe a dhéanamh. Déanfar cur síos ar chodanna úinéireachta i
> maidir leis an chruach agus leis an gcarn níos déanaí sa chaibidil seo, mar sin seo achoimre
> míniú á ullmhú.
>
> Is codanna cuimhne iad an cruach agus an chairn araon atá ar fáil do do chód a úsáid
> ag am rite, ach tá siad struchtúrtha ar bhealaí éagsúla. Stórálann an cruach luachanna 
> san ord a fhaigheann sé iad agus baintear na luachanna san ord eile. Tagraítear dó seo 
> mar _an ceann deireanach isteach, an chéad cheann amach_. Smaoinigh ar cruach de
> plátaí: nuair a chuireann tú níos mó plátaí isteach, cuireann tú iad ar bharr an chairn, agus cathain
> teastaíonn pláta uait, tógann tú ceann den bharr. Ní oibreodh sé chomh maith plátaí
> a chur leis nó a bhaint den lár nó ón mbun! Tugtar _pushing ar shonraí a chur leis
> isteach ar an cruach, agus tugtar _popping as an cruach_ ar na sonraí a bhaint. Gach
> ní mór méid seasta aitheanta a bheith ag sonraí atá stóráilte ar an chruach. Sonraí le anaithnid
> ní mór méid ag am tiomsaithe nó méid a d'fhéadfadh athrú a stóráil ar an gcarn
> ina ionad.
>
> Níl an carn chomh eagraithe: nuair a chuireann tú sonraí ar an gcarn, iarrann tú a
> méid áirithe spáis. Aimsíonn an leithdháileadh cuimhne spota folamh sa charn
> atá mór go leor, marcálann sé go bhfuil sé in úsáid, agus cuireann sé _pointer_ ar ais, a bhfuil
> is é seoladh an tsuímh sin. Tugtar _leithdháileadh ar an bpróiseas seo
> heap_ agus déantar é a ghiorrú uaireanta mar _leithroinnt_ (luachanna a bhrú ar
> ní mheastar go leithdháileann an chruach). Toisc gurb é an pointeoir chuig an gcarn a
> ar a dtugtar, méid seasta, is féidir leat an pointeoir a stóráil ar an gcruach, ach nuair is mian leat
> na sonraí iarbhír, ní mór duit an pointeoir a leanúint. Smaoinigh ar a bheith ina suí ag a
> bialann. Nuair a théann tú isteach, luann tú líon na ndaoine i do ghrúpa, agus
> aimsíonn an t-óstach tábla folamh a oireann do gach duine agus a threoraíonn tú ann. Más rud é
> tagann duine éigin i do ghrúpa déanach, féadfaidh siad fiafraí de cá bhfuil tú i do shuí
> fhaigheann tú.
>
> Tá brú ar an chairn níos tapúla ná mar a leithdháileadh ar an gcarn mar gheall ar an
> ní gá don leithdháileoir áit a chuardach le sonraí nua a stóráil; go bhfuil an suíomh sin
> i gcónaí ag barr an chruach. I gcomparáid, spás a leithdháileadh ar an gcarn
> teastaíonn tuilleadh oibre mar ní mór don leithroinnt spás mór go leor a aimsiú ar dtús
> na sonraí a choinneáil agus ansin leabharchoimeád a dhéanamh chun ullmhú don chéad cheann eile
> leithdháileadh.
>
> Tá rochtain ar shonraí sa charn níos moille ná rochtain a fháil ar shonraí ar an gcruach toisc
> caithfidh tú pointeoir a leanúint le dul ann. Tá próiseálaithe comhaimseartha níos tapúla
> má léimeann siad timpeall níos lú sa chuimhne. Ag leanúint leis an analaí, a mheas ar fhreastalaí
> ag bialann ag glacadh orduithe ó go leor táblaí. Tá sé is éifeachtaí a fháil
> na horduithe go léir ag bord amháin sula dtéann tú ar aghaidh go dtí an chéad tábla eile. Ag tabhairt an
> ordú ó thábla A, ansin ordú ó thábla B, ansin ceann ó A arís, agus
> ansin bheadh próiseas ceann as B arís i bhfad níos moille. Ar an gcaoi chéanna, a
> is féidir le próiseálaí a chuid oibre a dhéanamh níos fearr má oibríonn sé ar shonraí atá gar do shonraí eile
> sonraí (mar atá sé ar an chruach) seachas níos faide ar shiúl (mar is féidir é a bheith ar an
> gcarn).
>
> Nuair a ghlaonn do chód feidhm, aistrítear na luachanna isteach san fheidhm
> (lena n-áirítear, féideartha, leideanna do shonraí ar an gcarn) agus na feidhmeanna
> brúitear athróga áitiúla isteach sa chruach. Nuair a bhíonn an fheidhm thart, iad siúd
> laghdaítear luachanna as an gcruach.
>
> Súil a choinneáil ar cad iad na codanna den chód a úsáideann na sonraí ar an gcarn,
> an méid sonraí dúblacha ar an gcarn a íoslaghdú, agus glanadh suas nach bhfuil in úsáid
> is fadhbanna leis an úinéireacht iad sonraí ar an gcarn ionas nach n-imíonn tú as spás
> seoltaí. Nuair a thuigeann tú úinéireacht, ní bheidh ort smaoineamh ar an
> Stack agus an gcarn go minic, ach a fhios agam go bhfuil an príomhchuspóir úinéireachta
> Is féidir le sonraí carn a bhainistiú cuidiú a mhíniú cén fáth a n-oibríonn sé mar a oibríonn sé.

### Rialacha Úinéireachta

Ar dtús, déanaimis féachaint ar na rialacha úinéireachta. Coinnigh na rialacha seo i gcuimhne agus muid
obair trí na samplaí a léiríonn iad:

- Tá _úinéir_ ag gach luach i Rust.
- Ní féidir ach úinéir amháin a bheith ann ag an am.
- Nuair a théann an t-úinéir as raon feidhme, beidh an luach a thit.

### Scóip Athróg

Anois agus muid imithe thart ar chomhréir bhunúsach Rust, ní chuirfimid gach `fn main() {` san áireamh
cód i samplaí, mar sin má tá tú ag leanúint chomh maith, déan cinnte a chur ar an méid seo a leanas
samplaí taobh istigh d'fheidhm `main` de láimh. Mar thoradh air sin, beidh ár samplaí a
beagán níos gonta, ag ligean dúinn díriú ar na sonraí iarbhír seachas
cód pláta coire.

Mar chéad shampla d’úinéireacht, féachfaimid ar _scóip_ roinnt athróg. A
raon feidhme is ea an raon laistigh de chlár a bhfuil mír bailí dó. Tóg an
athróg seo a leanas:

```rust
let s = "hello";
```

Tagraíonn an athróg `s` do teaghrán litriúil, áit a bhfuil luach na sreinge
hardcoded isteach i dtéacs ár gclár. Tá an athróg bailí ón bpointe ag
atá dearbhaithe go dtí deireadh an _scóip_ reatha. Léiríonn liostú 4-1 a
clár le nótaí tráchta ag cur in iúl cá háit a mbeadh an athróg `s` bailí.

<Listing number="4-1" caption="A variable and the scope in which it is valid">

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/listing-04-01/src/main.rs:here}}
```

</Listing>

I bhfocail eile, tá dhá phointe tábhachtacha ama anseo:

- Nuair a thagann `s` _isteach_ sa raon feidhme, bíonn sé bailí.
- Fanann sé bailí go dtí go dtéann sé _as_ scóip.

Ag an bpointe seo, tá an gaol idir scopes agus nuair a athróga bailí
cosúil leis sin i dteangacha ríomhchlárúcháin eile. Anois cuirfimid leis seo
a thuiscint tríd an gcineál `String` a thabhairt isteach.

### An Cineál `String`

Chun na rialacha úinéireachta a léiriú, ní mór dúinn cineál sonraí atá níos casta
ná iad siúd atá clúdaithe againn sa [“Cineálacha Sonraí”][data-types]<!-- neamhaird a dhéanamh ar --> alt
de Chaibidil 3. Tá na cineálacha a clúdaíodh roimhe seo de mhéid aitheanta, is féidir iad a stóráil
ar an chruach agus popped as an chairn nuair a bhíonn a raon feidhme thart, agus is féidir a bheith
a chóipeáil go tapa agus go fánach chun cás nua neamhspleách a dhéanamh
caithfidh cuid de chód an luach céanna a úsáid i raon feidhme difriúil. Ach ba mhaith linn
féach ar na sonraí atá stóráilte ar an gcarn agus fiosraigh conas a bhíonn a fhios ag Rust cathain
glan suas na sonraí sin, agus is sampla iontach é an cineál `String`.

Díreoimid ar na codanna de `String` a bhaineann le húinéireacht. iad seo
baineann gnéithe freisin le cineálacha sonraí casta eile, cibé acu a sholáthraíonn
an leabharlann chaighdeánach nó cruthaithe agat. Déanfaimid plé níos doimhne ar `String`
[Caibidil 8][ch8]<!-- neamhaird a dhéanamh -->.

Tá teaghlitreacha feicthe againn cheana féin, áit a bhfuil luach teaghrán códaithe go crua isteach inár
clár. Tá litreacha teaghráin áisiúil, ach níl siad oiriúnach do gach ceann acu
staid ina mb'fhéidir gur mhaith linn téacs a úsáid. Cúis amháin ná go bhfuil siad
dochorraithe. Rud eile ná nach féidir gach luach teaghrán a bheith ar eolas agus muid ag scríobh
ár gcód: mar shampla, cad má theastaíonn uainn ionchur úsáideora a ghlacadh agus é a stóráil? Le haghaidh
sna cásanna seo, tá an dara cineál teaghrán ag Rust, `String`. Bainistíonn an cineál seo
sonraí a leithdháiltear ar an gcarn agus mar sin tá sé in ann méid téacs a stóráil a
is eol dúinn ag am tiomsaithe. Is féidir leat `String` a chruthú as teaghrán
litriúil ag baint úsáide as an bhfeidhm `ó`, mar sin:

```rust
let s = String::from("hello");
```

Ceadaíonn an t-oibreoir idirstad dúbailte `::` dúinn an `ó` áirithe seo a spásáil
feidhmiú faoin gcineál `String` seachas úsáid a bhaint as ainm de shaghas éigin mar
`string_from`. Déanfaimid an chomhréir seo a phlé níos mó sa [“Modh
Comhréir”][method-syntax]<!-- ignore --> alt de Chaibidil 5, agus nuair a labhair muid
faoi ​​spásáil ainmneacha le modúil i [“Cosáin chun tagairt a dhéanamh do mhír sa
Crann an Mhodúil”][paths-module-tree]<!-- ignore --> i gCaibidil 7.

Is féidir an cineál seo téad _is féidir_ a mutadh:

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/no-listing-01-can-mutate-string/src/main.rs:here}}
```

Mar sin, cad é an difríocht anseo? Cén fáth gur féidir `String` a shaobhadh ach go litriúil
ní féidir? Is é an difríocht sa chaoi a ndéileálann an dá chineál seo le cuimhne.

### Cuimhne agus Leithdháileadh

I gcás teaghrán litriúil, tá a fhios againn an t-ábhar ag am tiomsaithe, mar sin an
tá an téacs códaithe go díreach isteach sa inrite deiridh. Sin é an fáth teaghrán
tá litriúil tapa agus éifeachtach. Ach ní thagann na hairíonna seo ach ón sreang
neamh-inaistritheacht litriúil. Ar an drochuair, ní féidir linn blob cuimhne a chur isteach sa
dénártha do gach píosa téacs nach bhfuil a mhéid anaithnid ag an am tiomsaithe agus cé leis
seans go n-athróidh an méid agus an clár á rith.

Leis an gcineál `String`, chun tacaíocht a thabhairt do phíosa téacs inaistrithe, infhás,
ní mór dúinn méid cuimhne a leithdháileadh ar an gcarn, anaithnid ag am tiomsaithe,
an t-ábhar a shealbhú. Ciallaíonn sé seo:

- Ní mór an chuimhne a iarraidh ar an leithdháileadh cuimhne ag am rite.
- Teastaíonn bealach uainn leis an gcuimhne seo a thabhairt ar ais don leithroinnt nuair a bheidh sé críochnaithe againn
 ár `String`.

Déanaimid an chéad chuid sin: nuair a ghlaoimid `String::from`, a chur i bhfeidhm
iarrann sé an chuimhne atá de dhíth air. Tá sé seo go leor uilíoch i gcláir
teangacha.

Mar sin féin, tá an dara cuid difriúil. I dteangacha le bailitheoir _truflais
(GC)_, coinníonn an GC súil agus glanann sé cuimhne nach bhfuil in úsáid
a thuilleadh, agus ní gá dúinn smaoineamh faoi. I bhformhór na dteangacha gan GC,
tá sé de fhreagracht orainne a aithint nuair nach bhfuil cuimhne á húsáid a thuilleadh agus chun
cód glaonna chun é a shaoradh go sainráite, díreach mar a rinneamar chun é a iarraidh. Ag déanamh seo
i gceart bhí fadhb ríomhchláraithe deacair go stairiúil. Má dhéanaimid dearmad,
caithfimid cuimhne. Má dhéanaimid é ró-luath, beidh athróg neamhbhailí againn. Más rud é
déanaimid faoi dhó é, sin fabht freisin. Caithfimid `allocate` amháin a phéireáil leis
Díreach ceann amháin `free`.

Bíonn cosán difriúil ag meirge: cuirtear an chuimhne ar ais go huathoibríoch nuair a bhíonn an
téann athróg ar leis é as raon feidhme. Seo leagan dár sampla scóip
ó Liostú 4-1 ag baint úsáide as `String` in ionad teaghrán litriúil:

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/no-listing-02-string-scope/src/main.rs:here}}
```

Tá pointe nádúrtha ann inar féidir linn an chuimhne a theastaíonn ó ár `String` a thabhairt ar ais
don leithroinnt: nuair a théann `s` as an scóip. Nuair a théann athróg amach as
raon feidhme, glaonna Rust feidhm speisialta dúinn. Tugtar an fheidhm seo
[`drop`][drop] <!-- ignore -->, agus seo an áit ar féidir le húdar `String` a chur
an cód chun an chuimhne a thabhairt ar ais. Glaonn Rust `drop` go huathoibríoch ag an dúnadh
lúibín chatach.

> Nóta: In C++, an patrún seo chun acmhainní a aimsiú ag deireadh míre
> uaireanta tugtar _Tionscnamh um Fháil Acmhainní (RAII)_ ar an saolré.
> Beidh eolas agat ar an bhfeidhm `drop` i Rust má d'úsáid tú RAII
> patrúin.

Bíonn tionchar as cuimse ag an bpatrún seo ar an mbealach a scríobhtar cód Meirge. Féadfaidh sé cosúil
simplí anois, ach is féidir iompar cód a bheith gan choinne i níos mó
cásanna casta nuair is mian linn athróga iolracha a bheith againn úsáid na sonraí
atá leithdháilte againn ar an gcarn. Déanaimis iniúchadh ar roinnt de na cásanna sin anois.

<!-- Old heading. Do not remove or links may break. -->

<a id="ways-variables-and-data-interact-move"></a>

#### Athróga agus Sonraí ag Idirghníomhú le Bog

Is féidir le hathróga iolracha idirghníomhú leis na sonraí céanna ar bhealaí éagsúla i Rust.
Breathnaímid ar shampla ag baint úsáide as slánuimhir i Liostú 4-2.

<Listing number="4-2" caption="Assigning the integer value of variable `x` to `y`">

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/listing-04-02/src/main.rs:here}}
```

</Listing>

Is dócha gur féidir linn buille faoi thuairim a dhéanamh ar a bhfuil á dhéanamh seo: “ceannaigh an luach `5` le `x`; déan ansin
cóip den luach in `x` agus ceangail le `y` é." Tá dhá athróg againn anois, `x`
agus `y`, agus an dá chomhionann `5`. Tá sé seo go deimhin cad atá ag tarlú, mar gheall ar slánuimhreacha
is luachanna simplí iad le méid seasta aitheanta, agus déantar an dá luach `5` seo a bhrú
isteach sa chruach.

Breathnaímis anois ar an leagan `String`:

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/no-listing-03-string-move/src/main.rs:here}}
```

Breathnaíonn sé seo an-chosúil, agus mar sin d'fhéadfaimis glacadh leis gurb é an bealach a oibríonn sé
céanna: is é sin, dhéanfadh an dara líne cóip den luach i `s1` agus ceangail
é go `s2`. Ach ní hé seo a tharlaíonn go hiomlán.

Breathnaigh ar Fíor 4-1 chun a fheiceáil cad atá ag tarlú do `String` faoi na
clúdaigh. Tá trí chuid i `String`, léirithe ar chlé: pointeoir chuig
an chuimhne a choinníonn inneachar na téad, fad, agus toilleadh.
Stóráiltear an grúpa sonraí seo ar an chruach. Ar dheis tá an chuimhne ar an
carn a shealbhaíonn an t-ábhar.

<img alt="Dhá tábla: sa chéad tábla tá léiriú s1 ar an
stack, arb é atá ann a fhad (5), toilleadh (5), agus pointeoir chuig an gcéad cheann
luach sa dara tábla. Sa dara tábla tá léiriú an
sonraí teaghrán ar an gcarn, beart le beart." src="img/trpl04-01.svg" class="center"
style="width: 50%;" />

<span class="caption">Fíor 4-1: Léiriú i gcuimhne ar `String`
a bhfuil an luach `"hello"` faoi cheangal go `s1`</span>

Is é an fad ná cé mhéad cuimhne, i mbearta, atá inneachar an `String`
ag baint úsáide as faoi láthair. Is é an toilleadh an méid iomlán de chuimhne, i mbeart, go bhfuil an
Tá `String` faighte ón leithdháilteoir. An difríocht idir fad agus
cúrsaí acmhainne, ach ní sa chomhthéacs seo, mar sin go fóill, tá sé ceart neamhaird a dhéanamh
acmhainn.

Nuair a shannaimid `s1` do `s2`, déantar na sonraí `String` a chóipeáil, rud a chiallaíonn go ndéanaimid cóip den
pointeoir, an fad, agus an toilleadh atá ar an gcruach. Ní chóipeáilimid an
sonraí ar an gcarn a dtagraíonn an pointeoir dó. I bhfocail eile, na sonraí
Breathnaíonn ionadaíocht sa chuimhne cosúil le Fíor 4-2.

<img alt="Trí tábla: táblaí s1 agus s2 a léiríonn na teaghráin sin ar an
stack, faoi seach, agus an dá phointe ag díriú ar na sonraí teaghrán céanna ar an gcarn."
src="img/trpl04-02.svg" class="center" style="leithead: 50%;" />

<span class="caption">Fíor 4-2: Léiriú i gcuimhne ar an athróg `s2`
ina bhfuil cóip den phointeoir, den fhad agus den toilleadh `s1`</span>

Tá cuma _not_ ar an léiriú ar Fhíor 4-3, agus is é sin an rud a dhéanfadh cuimhne
cuma an ndearna Rust na sonraí carn a chóipeáil ina ionad sin freisin. Má rinne Rust é seo, beidh an
d'fhéadfadh oibríocht `s2 = s1` a bheith an-chostasach i dtéarmaí feidhmíochta rite má
bhí na sonraí ar an gcarn mór.

<img alt="Ceithre thábla: dhá thábla a léiríonn na sonraí cruachta le haghaidh s1 agus s2,
agus díríonn gach ceann acu ar a chóip féin de shonraí teaghrán ar an gcarn."
src="img/trpl04-03.svg" class="center" style="leithead: 50%;" />

<span class="caption">Fíor 4-3: Féidearthacht eile maidir le cad a d’fhéadfadh `s2 = s1`
déan má chóipeáil Rust na sonraí carn freisin</span>

Níos luaithe, dúirt muid nuair a théann athróg as raon feidhme, Rust go huathoibríoch
glaonn sé an fheidhm `drop` agus glanann sé an chuimhne chairn don athróg sin. Ach
Léiríonn Fíor 4-2 an dá phointe sonraí ag díriú ar an suíomh céanna. Seo a
fadhb: nuair a théann `s2` agus `s1` as an raon feidhme, déanfaidh siad araon iarracht an
cuimhne chéanna. Earráid _double free_ a thugtar air seo agus tá sé ar cheann de na cuimhne
fabhtanna sábháilteachta a luaigh muid roimhe seo. Is féidir cuimhne a bheith mar thoradh ar chuimhne a shaoradh faoi dhó
éilliú, a bhféadfadh leochaileachtaí slándála a bheith mar thoradh air.

Chun sábháilteacht chuimhne a chinntiú, tar éis na líne `let s2 = s1;`, measann Rust `s1` mar
bailí a thuilleadh. Mar sin, ní gá do Rust rud ar bith a shaoradh nuair a théann `s1`
as scóip. Seiceáil cad a tharlaíonn nuair a dhéanann tú iarracht `s1` a úsáid i ndiaidh `s2`
cruthaithe ; ní oibreoidh sé:

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch04-understanding-ownership/no-listing-04-cant-use-after-move/src/main.rs:here}}
```

Gheobhaidh tú earráid mar seo toisc go gcuireann Rust cosc ort an
tagairt neamhbhailí:

```console
{{#include ../../listings/ch04-understanding-ownership/no-listing-04-cant-use-after-move/output.txt}}
```

Má tá na téarmaí _shallow copy_ agus _deep copy_ cloiste agat agus tú ag obair leo
teangacha eile, coincheap an phointeora, an fad agus an toilleadh a chóipeáil
gan na sonraí a chóipeáil is dócha gur cosúil le cóip éadomhain a dhéanamh. Ach
toisc go ndéanann Rust an chéad athróg neamhbhailí freisin, in ionad a bheith ar a dtugtar a
cóip éadomhain, a thugtar air mar _move_. Sa sampla seo, déarfaimis go bhfuil `s1`
a _bogadh_ go `s2`. Mar sin, taispeántar cad a tharlaíonn i ndáiríre i bhFíor 4-4.

<img alt="Trí tábla: táblaí s1 agus s2 a léiríonn na teaghráin sin ar an
stack, faoi seach, agus an dá phointe ag díriú ar na sonraí teaghrán céanna ar an gcarn.
Tá tábla s1 liathaithe toisc nach bhfuil s1 bailí a thuilleadh; ní féidir ach s2 a úsáid chun
rochtain a fháil ar na sonraí carn." src="img/trpl04-04.svg" class="center" style="width:
50%;" />

<span class="caption">Fíor 4-4: Léiriú i gcuimhne tar éis `s1` a bheith
neamhbhailí</span>

Réitíonn sé sin ár bhfadhb! Le ach `s2` bailí, nuair a théann sé as raon feidhme é
saorfaidh an chuimhne amháin, agus táimid críochnaithe.

Ina theannta sin, tá rogha dearaidh intuigthe leis seo: ní dhéanfaidh Rust choíche
cruthaigh cóipeanna “doimhne” de do shonraí go huathoibríoch. Mar sin, aon _uathoibríoch_
is féidir glacadh leis go bhfuil an chóipeáil neamhchostasach i dtéarmaí feidhmíochta am rite.

#### Scóip agus Tasc

Tá a mhalairt de seo fíor maidir leis an ngaol idir scóip, úinéireacht, agus
cuimhne á scaoileadh tríd an bhfeidhm `drop` freisin. Nuair a shannadh tú go hiomlán
luach nua ar athróg atá ann cheana féin, glaofaidh Rust `drop` agus saorfaidh sé an bunleagan
cuimhne luach láithreach. Smaoinigh ar an gcód seo, mar shampla:

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/no-listing-04b-replacement-drop/src/main.rs:here}}
```

Ar dtús dearbhaímid athróg `s` agus ceanglaímid é de `String` leis an luach
`"Dia duit"`. Ansin cruthaímid láithreach `String` nua leis an luach `"ahoy"` agus
a shannadh do `s`. Ag an bpointe seo, níl aon rud ag tagairt don luach bunaidh ar
an gcarn ar chor ar bith.

<img alt="Tábla amháin s a léiríonn an luach teaghrán ar an chruach, ag díriú ar
an dara píosa sonraí téad (ahoy) ar an gcarn, leis an teaghrán bunaidh
sonraí (hello) liath amach toisc nach féidir é a rochtain a thuilleadh."
src="img/trpl04-05.svg"
rang = "ionad"
style="width: 50%;"
/>

<span class="caption">Fíor 4-5: Léiriú sa chuimhne i ndiaidh na tosaigh
cuireadh an luach ina iomláine.</span>

Mar sin téann an teaghrán bunaidh as raon feidhme láithreach. Rithfidh Rust an `drop`
feidhmiú air agus saorfar a chuimhne ar an bpointe boise. Nuair a phriontáilimid an luach
ag an deireadh, beidh sé `"ahoy, world!"`.

<!-- Sean-cheannteideal. Ná bain amach nó seans go mbrisfidh naisc. -->

<a id="ways-variables-and-data-interact-clone"></a>

#### Athróga agus Sonraí ag Idirghníomhú le Clón

Más mian linn _do_ sonraí carn an `String` a chóipeáil go domhain, ní hamháin an
sonraí cruachta, is féidir linn úsáid a bhaint as modh coitianta ar a dtugtar `clone`. Déanfaimid plé ar an modh
comhréir i gCaibidil 5, ach toisc go bhfuil modhanna mar ghné coitianta i go leor
teangacha ríomhchlárúcháin, is dócha go bhfaca tú iad roimhe seo.

Seo sampla den mhodh ‘clóin’ i ngníomh:


```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/no-listing-05-clone/src/main.rs:here}}
```

Oibríonn sé seo go breá agus cruthaíonn sé go sainráite an iompar a léirítear i bhFíor 4-3,
áit a ndéantar na sonraí carn _does_ a chóipeáil.

Nuair a fheiceann tú glao chuig `clone`, tá a fhios agat go bhfuil roinnt cód treallach á
a fhorghníomhú agus féadfaidh an cód sin a bheith costasach. Tá sé ina tháscaire amhairc go bhfuil rud éigin
difriúil ag dul ar aghaidh.

#### Sonraí Cruachta Amháin: Cóipeáil

Tá roic eile nár labhair muid faoi go fóill. An cód seo ag baint úsáide as
slánuimhreacha—ar taispeánadh cuid de i Liostú 4-2—oibreacha agus atá bailí:

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/no-listing-06-copy/src/main.rs:here}}
```

Ach is cosúil go bhfuil an cód seo ag teacht salach ar a bhfuil foghlamtha againn: níl aon ghlaoch orainn
`clone`, ach tá `x` fós bailí agus níor aistríodh go `y` é.

Is é an chúis atá leis sin ná go bhfuil cineálacha cosúil le slánuimhreacha a bhfuil méid aitheanta acu ag tiomsú
stóráiltear an t-am go hiomlán ar an gcruach, mar sin tá cóipeanna de na luachanna iarbhír tapa
a dhéanamh. Ciallaíonn sé sin nach bhfuil aon chúis ann go mbeimis ag iarraidh `x` a chosc
bailí tar éis dúinn an athróg `y` a chruthú. I bhfocail eile, níl aon difríocht ann
idir chóipeáil dhomhain agus éadomhain anseo, mar sin ní dhéanfadh glaoch `clone` tada
difriúil ón ngnáthchóipeáil éadomhain, agus is féidir linn é a fhágáil amach.

Tá nóta speisialta ag Rust ar a dtugtar an trait `Copy` is féidir linn a chur air
cineálacha atá stóráilte ar an chruach, mar atá slánuimhreacha (beidh muid ag caint níos mó faoi
tréithe i [Caibidil 10][traits]<!-- ignore -->). Má chuireann cineál an `Copy` i bhfeidhm
tréithe, ní ghluaiseann athróga a úsáideann í, ach go ndéantar iad a chóipeáil go fánach,
rud a fhágann go bhfuil siad fós bailí tar éis sannadh d'athróg eile.

Ní ligfidh Rust dúinn cineál a anótáil le `Copy` más é an cineál, nó aon chuid dá chuid,
tá an trait `Drop` curtha i bhfeidhm aige. Má theastaíonn rud éigin speisialta ón gcineál le tarlú
nuair a théann an luach as raon feidhme agus cuirimid an nóta `Copy` leis an gcineál sin,
gheobhaidh muid earráid ama tiomsaithe. Chun foghlaim faoi conas an nóta `Copy` a chur leis
le do chineál chun an tréith a chur i bhfeidhm, féach [“Derivable
Traits”][díorthaigh-traits]<!-- ignore --> in Aguisín C.

Mar sin, cad iad na cineálacha a chuireann an trait `Copy` i bhfeidhm? Is féidir leat an doiciméadú a sheiceáil le haghaidh
an cineál a thugtar a bheith cinnte, ach mar riail ghinearálta, aon ghrúpa de scálach simplí
is féidir le luachanna `Copy` a chur i bhfeidhm, agus ní gá aon rud a leithdháileadh nó a bhfuil cuid acu
foirm acmhainne is féidir `Copy` a chur i bhfeidhm. Seo cuid de na cineálacha a
cuir `Copy` i bhfeidhm:

- Gach cineál slánuimhir, mar shampla `u32`.
- An cineál Boole, `bool`, le luachanna `true` agus `false`.
- Gach cineál snámhphointe, mar shampla `f64`.
- An cineál carachtar, `char`.
- Tuples, mura bhfuil iontu ach cineálacha a chuireann `Copy` i bhfeidhm freisin. Mar shampla,
 Cuireann `(i32, i32)` `Copy` i bhfeidhm, ach ní dhéanann `(i32, Teaghrán)`.

### Úinéireacht agus Feidhmeanna

Tá na meicníochtaí a bhaineann le luach a chur ar aghaidh go dtí feidhm cosúil leo siúd nuair a
luach a shannadh d'athróg. Má chuirtear athróg ar aghaidh chuig feidhm, bogfar nó
cóip, díreach mar a dhéanann sannadh. Tá sampla i liostú 4-3 le roinnt nótaí
ag léiriú cá háit a dtéann athróga isteach agus amach as an scóip.

<Listing number="4-3" file-name="src/main.rs" caption="Feidhmeanna le húinéireacht agus raon feidhme anótáilte">

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/listing-04-03/src/main.rs}}
```

</Listing>

Dá ndéanfaimis iarracht `s` a úsáid tar éis an ghlao go `takes_ownership`, chaithfeadh Rust a
earráid ama tiomsaithe. Cosnaíonn na seiceálacha statacha seo sinn ó bhotúin. Bain triail as cur
cód go `main` a úsáideann `s` agus `x` chun a fheiceáil cén áit ar féidir leat iad a úsáid agus cén áit
cuireann na rialacha úinéireachta cosc ​​ort é sin a dhéanamh.

### Luachanna Aischuir agus Scóip

Is féidir le luachanna tuairisceáin úinéireacht a aistriú freisin. Taispeánann liosta 4-4 sampla de a
feidhm a thugann luach éigin ar ais, le nótaí cosúil leis na cinn i Liostú
4-3.

<Listing number="4-4" file-name="src/main.rs" caption="Transferring ownership of return values">

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/listing-04-04/src/main.rs}}
```

</Listing>

leanann úinéireacht athróige an patrún céanna gach uair: ag sannadh a
aistríonn luach chuig athróg eile é. Nuair a athróg a chuimsíonn sonraí ar an
gcarn imithe as raon feidhme, beidh an luach a ghlanadh suas le `drop` mura úinéireacht
de na sonraí aistríodh chuig athróg eile.

Cé go n-oibríonn sé seo, úinéireacht a ghlacadh agus ansin úinéireacht a thabhairt ar ais le gach
Tá feidhm beagán tedious. Cad a tharlaíonn má theastaíonn uainn ligean d’fheidhm luach a úsáid ach
nach bhfuil úinéireacht a ghlacadh? Tá sé an-chorraithe go bhfuil gá le haon rud a thabharfaimid isteach freisin
a thabhairt ar ais más mian linn é a úsáid arís, chomh maith le haon sonraí a thagann as
ó chorp an fheidhm a d'fhéadfadh muid a bheith ag iarraidh a thabhairt ar ais chomh maith.

Ligeann Rust dúinn luachanna iolracha a thabhairt ar ais trí úsáid a bhaint as tuple, mar a thaispeántar i Liostú 4-5.

<Listing number="4-5" file-name="src/main.rs" caption="Úinéireacht paraiméadair á filleadh">

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/listing-04-05/src/main.rs}}
```

</Listing>

Ach tá sé seo i bhfad ró-searmanas agus a lán oibre le haghaidh coincheap ba chóir a bheith
coitianta. Go fortunately dúinn, tá gné ag Rust chun luach a úsáid gan
úinéireacht a aistriú, ar a dtugtar _references_.

[data-types]: ch03-02-data-types.html#data-types
[ch8]: ch08-02-strings.html
[traits]: ch10-02-traits.html
[derivable-traits]: appendix-03-derivable-traits.html
[method-syntax]: ch05-03-method-syntax.html#method-syntax
[paths-module-tree]: ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html
[drop]: ../std/ops/trait.Drop.html#tymethod.drop
