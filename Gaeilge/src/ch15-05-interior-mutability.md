## `RefCell<T>` agus an Patrún um Shócmhainneacht Intí

Is patrún deartha é _Interior mutability_ i Rust a ligeann duit sóchán a dhéanamh
sonraí fiú nuair a bhíonn tagairtí do-chomhtháthaithe ann do na sonraí sin; de ghnáth, seo
dícheadaítear gníomhaíocht leis na rialacha iasachtaithe. Chun sonraí a mutate, úsáideann an patrún
cód `unsafe` taobh istigh de struchtúr sonraí chun gnáthrialacha Rust a rialaíonn a lúbadh
sóchán agus iasacht. Cuireann cód neamhshábháilte in iúl don tiomsaitheoir go bhfuilimid
na rialacha a sheiceáil de láimh seachas a bheith ag brath ar an tiomsaitheoir chun iad a sheiceáil
dúinne; déanfaimid tuilleadh plé ar chód neamhshábháilte i gCaibidil 20.

Ní féidir linn cineálacha a úsáid a úsáideann an patrún sócmhainneachta taobh istigh ach amháin nuair is féidir linn
a áirithiú go leanfar na rialacha iasachtaíochta ag am rite, cé go bhfuil an
ní féidir leis an tiomsaitheoir é sin a ráthú. Tá an cód `unsafe` atá i gceist fillte ansin i a
API sábháilte, agus tá an cineál seachtrach fós immutable.

Déanaimis an coincheap seo a iniúchadh trí bhreathnú ar an gcineál `RefCell<T>` a leanann an
patrún muability istigh.

### Rialacha Iasachta a Fhorfheidhmiú ag Am Rite le `RefCell<T>`

Murab ionann agus `Rc<T>`, is ionann an cineál `RefCell<T>` agus úinéireacht aonair ar na sonraí
coinníonn sé. Mar sin, cad a dhéanann difríocht idir `RefCell<T>` agus cineál mar `Box<T>`?
Tabhair chun cuimhne na rialacha iasachtaithe a d’fhoghlaim tú i gCaibidil 4:

- Ag aon am ar leith, féadfaidh tú _either_ (ach ní an dá cheann) tagairt sho-shóite amháin a bheith agat 
nó líon ar bith tagairtí do-inaistrithe.
- Caithfidh teistiméireachtaí a bheith bailí i gcónaí.

Le tagairtí agus `Box<T>`, cuirtear malairtí na rialacha iasachtaíochta i bhfeidhm ag
am tiomsaithe. Le `RefCell<T>`, cuirtear na hathróga seo i bhfeidhm _ag am rite_.
Le tagairtí, má sháraíonn tú na rialacha seo, gheobhaidh tú earráid tiomsaithe. Le
`RefCell<T>`, má sháraíonn tú na rialacha seo, beidh do chlár i scaoll agus scoirfidh tú.

Is iad na buntáistí a bhaineann le seiceáil na rialacha iasachtaithe ag am tiomsaithe ná earráidí
a ghabháil níos luaithe sa phróiseas forbartha, agus níl aon tionchar ar
feidhmíocht runtime toisc go bhfuil an anailís ar fad críochnaithe roimh ré. Dóibh siúd
cúiseanna, is é seiceáil na rialacha iasachtaithe ag am tiomsaithe an rogha is fearr sa
formhór na gcásanna, agus sin an fáth gurb é seo réamhshocrú Rust.

Is é an buntáiste a bhaineann leis na rialacha iasachtaithe a sheiceáil ag am rite ina ionad sin
ceadaítear cásanna áirithe cuimhne-sábháilte ansin, áit a mbeidís
dícheadaithe ag na seiceálacha ama tiomsaithe. Anailís statach, cosúil leis an tiomsaitheoir Rust,
coimeádach ó dhúchas é. Tá roinnt airíonna de chód dodhéanta a bhrath trí
ag déanamh anailís ar an gcód: is é an sampla is cáiliúla ná an Fadhb Stad, mar atá
thar raon feidhme an leabhair seo ach is ábhar spéisiúil é le taighde a dhéanamh air.

Toisc go bhfuil roinnt anailíse dodhéanta, más rud é nach féidir leis an tiomsaitheoir Rust a bheith cinnte an
Comhlíonann cód na rialacha úinéireachta, d'fhéadfadh sé diúltú do chlár ceart; isteach
ar an mbealach seo, tá sé coimeádach. Má ghlac Rust le clár mícheart, úsáideoirí
ní bheadh ​​muinín agat as na ráthaíochtaí a thugann Rust. Mar sin féin, má Rust
ndiúltóidh clár ceart, beidh an ríomhchláraitheoir míchaoithiúlacht, ach rud ar bith
is féidir tubaisteach tarlú. Tá an cineál `RefCell<T>` úsáideach nuair atá tú cinnte go bhfuil do
Leanann an cód na rialacha iasachtaithe ach níl an tiomsaitheoir in ann a thuiscint agus
ráthaíocht go.

Cosúil le `Rc<T>`, tá `RefCell<T>` le húsáid i gcásanna aon-snáithe amháin
agus tabharfaidh sé earráid ama tiomsaithe duit má dhéanann tú iarracht é a úsáid i snáithe ilshnáithe
comhthéacs. Labhróimid faoi conas feidhmiúlacht `RefCell<T>` a fháil in a
clár ilshnáithe i gCaibidil 16.

Seo achoimre ar na fáthanna le `Box<T>`, `Rc<T>`, nó `RefCell<T>` a roghnú:

- Cuireann `Rc<T>` ar chumas úinéirí iolracha na sonraí céanna; `Box<T>` agus `RefCell<T>` 
úinéirí aonair a bheith acu.
- Ceadaíonn `Box<T>` iasachtaí domhalartaithe nó só-aistrithe a sheiceáil ag am tiomsaithe; `Rc<T>` 
ní cheadaíonn sé ach iasachtaí domhalartaithe a sheiceáil ag am tiomsaithe; Ceadaíonn `RefCell<T>` 
iasachtaí domhalartaithe nó só-aistrithe arna seiceáil ag am rite.
- Toisc go gceadaíonn `RefCell<T>` iasachtaí só-aistrithe a sheiceáil ag am rite, is féidir leat 
mutnaigh an luach taobh istigh den `RefCell<T>` fiú nuair atá an `RefCell<T>` 
dochorraithe.

Ag sóchán an luach taobh istigh de luach neamh-inmhalartaithe tá an _só-shócmhainneacht_
patrún. Breathnaímid ar chás ina bhfuil sócmhainneacht istigh úsáideach agus
scrúdú conas is féidir.

### Insó-shócmhainneacht: Iasacht In-chomhshóite go Luach Neamh-Chomhargadh

Iarmhairt ar na rialacha iasachtaíochta is ea nuair a bhíonn luach neamh-inmharthana agat, i.e.
ní féidir leat é a fháil ar iasacht go frithpháirteach. Mar shampla, ní thiomsóidh an cód seo:

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch15-smart-pointers/no-listing-01-cant-borrow-immutable-as-mutable/src/main.rs}}
```

Dá ndéanfadh tú iarracht an cód seo a thiomsú, gheobhfá an earráid seo a leanas:

```console
{{#include ../../listings/ch15-smart-pointers/no-listing-01-cant-borrow-immutable-as-mutable/output.txt}}
```

Mar sin féin, tá cásanna ann ina mbeadh sé úsáideach luach a athrú
é féin ina mhodhanna ach is cosúil go bhfuil sé neamh-inchurtha le cód eile. Cód lasmuigh den
ní bheadh ​​modhanna luacha in ann an luach a athrú. Ag baint úsáide as `RefCell<T>` is
bealach amháin chun an cumas sócmhainneachta taobh istigh a fháil, ach `RefCell<T>`
ní théann sé thart ar na rialacha iasachtaithe go hiomlán: an seiceálaí iasachtaí sa
Ceadaíonn tiomsaitheoir seo sócmhainneacht istigh, agus na rialacha iasacht a sheiceáil
ag am rite ina ionad. Má sháraíonn tú na rialacha, gheobhaidh tú `panic!` ina ionad
earráid tiomsaitheora.

Oibrímid trí shampla praiticiúil inar féidir linn `RefCell<T>` a úsáid chun mutate
luach domhalartaithe agus féach cén fáth a bhfuil sé sin úsáideach.

#### Cás Úsáide le haghaidh Inmheánach Mutability: Réada Bréige

Uaireanta le linn tástála úsáidfidh ríomhchláraitheoir cineál in ionad cineál eile,
chun iompar ar leith a urramú agus a dhearbhú go bhfuil sé curtha i bhfeidhm i gceart.
Tugtar _tástáil dúbailte_ ar an gcineál seo coinneálaí. Smaoinigh air sa chiall a
“stunt dúbailte” i ndéanamh scannán, nuair a chéimíonn duine isteach agus ina ionadaí
aisteoir radharc tricky ar leith a dhéanamh. Seasann dúbailteanna tástála do chineálacha eile
nuair atá tástálacha á rith againn. Is cineálacha sainiúla dúbailte tástála iad _Mock objects_
a thaifeadann cad a tharlaíonn le linn tástála ionas gur féidir leat a dhearbhú go bhfuil an ceart
gníomhartha ar siúl.

Níl réada ag meirge sa chiall chéanna is atá réada ag teangacha eile,
agus níl feidhmiúlacht réad bréige ag Rust ionsuite sa ghnáthleabharlann
mar a dhéanann roinnt teangacha eile. Mar sin féin, is féidir leat a chruthú cinnte struchtúr sin
fónfaidh na críocha céanna le réad bréige.

Seo an cás a dhéanfaimid tástáil: cruthóimid leabharlann a rianóidh luach
in aghaidh uasluacha agus seolann sé teachtaireachtaí bunaithe ar cé chomh gar don uasluach
luach atá ar an luach reatha. D’fhéadfaí an leabharlann seo a úsáid chun súil a choinneáil ar a
cuóta úsáideora don líon glaonna API a bhfuil cead acu a dhéanamh, mar shampla.

Ní chuirfidh ár leabharlann ar fáil ach an fheidhmiúlacht chun rianú a dhéanamh ar cé chomh gar do na
is é luach uasta agus cad ba cheart do na teachtaireachtaí a bheith ag na hamanna. Feidhmchláir
beifear ag súil go soláthróidh úsáid ár leabharlann an mheicníocht chun an
teachtaireachtaí: d'fhéadfadh an t-iarratas teachtaireacht a chur san iarratas, seol
ríomhphost, seol teachtaireacht téacs, nó rud éigin eile. Ní gá go mbeadh a fhios ag an leabharlann
go mion. Níl ag teastáil uaidh ach rud a chuireann tréith a chuirfimid ar fáil i bhfeidhm
ar a dtugtar `Messenger`. Léiríonn liostú 15-20 an cód leabharlainne:

<Listing number="15-20" file-name="src/lib.rs" caption="A library to keep track of how close a value is to a maximum value and warn when the value is at certain levels">

```rust,noplayground
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-20/src/lib.rs}}
```

</Listing>

Cuid thábhachtach amháin den chód seo ná go bhfuil modh amháin ag an trait `Messenger`
ar a dtugtar `send` a thógann tagairt do- immutable do `self` agus téacs an
teachtaireacht. Is é an tréith seo an comhéadan a chaithfidh ár réad bréige a chur i bhfeidhm ionas go mbeidh
is féidir an bhréag a úsáid ar an mbealach céanna le réad réadúil. An chuid thábhachtach eile
is é sin go dteastaíonn uainn iompar an mhodha `set_value` a thástáil ar an
`LimitTracker`. Is féidir linn an méid a thugaimid isteach don pharaiméadar `value` a athrú, ach
ní thugann `set_value` tada ar ais dúinn chun dearbhuithe a dhéanamh air. Ba mhaith linn a bheith
in ann a rá má chruthaímid `LimitTracker` le rud éigin a chuireann i bhfeidhm
an tréithe `Messenger` agus luach ar leith do `max`, nuair a théimid ar aghaidh difriúil
uimhreacha le haghaidh `value`, deirtear leis an teachtaire na teachtaireachtaí cuí a sheoladh.

Ní mór dúinn réad bréige a, in ionad a sheoladh r-phost nó teachtaireacht téacs nuair a againn
glaoigh ar `send`, ní choinneoidh sé ach súil ar na teachtaireachtaí a iarrtar air a sheoladh. Is féidir linn
cruthaigh sampla nua den réad bréige, cruthaigh `LimitTracker` a úsáideann an
réad bréige, cuir glaoch ar an modh `set_value` ar `LimitTracker`, agus ansin seiceáil é sin
tá na teachtaireachtaí a mbeimid ag súil leo ag an réad bréige. Léiríonn liostú 15-21 iarracht chun
cuir réad bréige i bhfeidhm chun é sin a dhéanamh, ach ní cheadóidh an seiceálaí iasachtaí é:

<Listing number="15-21" file-name="src/lib.rs" caption="An attempt to implement a `MockMessenger` that isn’t allowed by the borrow checker">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-21/src/lib.rs:here}}
```

</Listing>

Sainmhíníonn an cód tástála seo struchtúr `MockMessenger` a bhfuil `sent_messages` aige
réimse le `Vec` de luachanna `String` chun súil a choinneáil ar na teachtaireachtaí a insítear dó
a sheoladh. Sainmhínímid freisin feidhm ghaolmhar `new` le go mbeidh sé áisiúil di
cruthaigh luachanna `MockMessenger` nua a thosaíonn le liosta folamh teachtaireachtaí. muid
ansin cuir an trait `Messenger` i bhfeidhm do `MockMessenger` ionas gur féidir linn a
`MockMessenger` go `LimitTracker`. Sa sainmhíniú ar an modh `send`, táimid
tóg an teachtaireacht a tugadh isteach mar pharaiméadar agus stóráil sa `MockMessenger` í
liosta de na `sent_messages`.

Sa tástáil, táimid ag tástáil cad a tharlaíonn nuair a iarrtar ar an `LimitTracker` a shocrú
`value` go dtí rud atá níos mó ná 75 faoin gcéad den luach `max`. Gcéad dul síos, muid
cruthaigh `MockMessenger` nua, a thosóidh le liosta folamh teachtaireachtaí.
Ansin cruthaímid `LimitTracker` nua agus déanaimid tagairt don nua
`MockMessenger` agus luach `max` de 100. Glaoimid ar an modh `set_value` ar an
`LimitTracker` le luach 80, atá níos mó ná 75 faoin gcéad de 100. Ansin
dearbhaímid go bhfuil liosta na dteachtaireachtaí atá á gcoimeád ag an `MockMessenger`
de anois teachtaireacht amháin a bheith ann.

Mar sin féin, tá fadhb amháin leis an tástáil seo, mar a thaispeántar anseo:

```consól
{{#include ../../listings/ch15-smart-pointers/listing-15-21/output.txt}}
```

Ní féidir linn an `MockMessenger` a mhodhnú chun súil a choinneáil ar na teachtaireachtaí, toisc go bhfuil an
tagraíonn modh `send` do `self`. Ní féidir linn a ghlacadh freisin
moladh ón téacs earráide `&mut self` a úsáid sa mhodh `impl` agus
an sainmhíniú `trait`. Nílimid ag iarraidh an trait `Messenger` a athrú amháin
ar mhaithe le tástáil. Ina áit sin, ní mór dúinn bealach a aimsiú chun ár gcód tástála a dhéanamh
oibriú i gceart lenár ndearadh reatha.

Is é seo an cás inar féidir le sócmhainneacht taobh istigh cabhrú! Stórálfaimid an
`sent_messages` laistigh de `RefCell<T>`, agus ansin beidh an modh `send`
in ann `sent_messages` a mhodhnú chun na teachtaireachtaí atá feicthe againn a stóráil. Liostáil 15-22
léiríonn an chuma atá air sin:

<Listing number="15-22" file-name="src/lib.rs" caption="Using `RefCell<T>` to mutate an inner value while the outer value is considered immutable">

```rust,noplayground
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-22/src/lib.rs:here}}
```

</Listing>

Tá an réimse `sent_messages` den chineál `RefCell<Vec<String>>` anois in ionad
`Vec<String>`. San fheidhm `new`, cruthaímid `RefCell<Vec<String>>` nua
shampla thart ar an veicteoir folamh.

Chun an modh `send` a chur i bhfeidhm, tá an chéad pharaiméadar fós ina
iasacht domhalartaithe den `self`, a thagann leis an sainmhíniú trait. Glaoimid
`borrow_mut` ar an `RefCell<Vec<String>>` i `self.sent_messages` chun a fháil
tagairt shochorraithe don luach taobh istigh den `RefCell<Vec<String>>`, is é sin an
veicteoir. Ansin is féidir linn `brú` a ghlaoch ar an tagairt mutable don veicteoir a choinneáil
rian de na teachtaireachtaí a seoladh le linn na tástála.

Is é an t-athrú deireanach atá le déanamh againn ná sa dearbhú: féachaint cé mhéad earra atá ann
sa veicteoir istigh, tugaimid `borrow` ar an `RefCell<Vec<String>>` chun
tagairt domhalartaithe don veicteoir.

Anois go bhfuil tú feicthe agat conas `RefCell<T>` a úsáid, déanaimis iniúchadh ar conas a oibríonn sé!

#### Iasachtaí a Choimeád ag Am Rite le `RefCell<T>`

Nuair a chruthaítear tagairtí domhalartaithe agus mutable, úsáidimid na `&` agus `&mut`
comhréir, faoi seach. Le `RefCell<T>`, úsáidimid an `borrow` agus `borrow_mut`
modhanna, atá mar chuid den API sábháilte a bhaineann le `RefCell<T>`. Tá an
Filleann modh `borrow` an cineál pointeoir cliste `Ref<T>`, agus `borrow_mut`
ar ais an cineál pointeoir cliste `RefMut<T>`. Cuireann an dá chineál `Deref` i bhfeidhm, mar sin táimid
is féidir leo déileáil leo mar thagairtí rialta.

Coinnítear sa `RefCell<T>` cé mhéad `Ref<T>` agus `RefMut<T>` cliste
tá leideanna gníomhach faoi láthair. Gach uair a dtugaimid `borrow`, an `RefCell<T>`
méadaíonn sé a chomhaireamh maidir le cé mhéad iasacht neamh-inmhalartaithe atá gníomhach. Nuair a `Tag<T>`
téann luach amach as an raon feidhme, laghdaítear líon na n-iasachtaí do-inaistrithe faoi cheann amháin. Díreach
cosúil leis na rialacha iasachtaithe maidir le ham tiomsaithe, ligeann `RefCell<T>` go leor do-athlasaithe a bheith againn
iasachtaí nó iasacht sho-shóite amháin ag aon am.

Má dhéanaimid iarracht na rialacha seo a shárú, seachas earráid tiomsaitheora a fháil agus muid
le tagairtí, beidh scaoll faoi chur i bhfeidhm `RefCell<T>`
am rite. Léiríonn liosta 15-23 modhnú ar chur i bhfeidhm `send` isteach
Liostáil 15-22. Táimid ag iarraidh dhá iasacht shochorraithe a chruthú d’aon ghnó
chun an scóip chéanna a léiriú go gcuireann `RefCell<T>` cosc ​​orainn é seo a dhéanamh
ag am rite.

<Listing number="15-23" file-name="src/lib.rs" caption="Creating two mutable references in the same scope to see that `RefCell<T>` will panic">

```rust,ignore,panics
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-23/src/lib.rs:here}}
```

</Listing>

Cruthaímid athróg `one_borrow` don phointeoir cliste `RefMut<T>` a cuireadh ar ais
ó `borrow_mut`. Ansin cruthaímid iasacht mutable eile ar an mbealach céanna sa
athróg `two_borrow`. Déanann sé seo dhá thagairt chomhshóite sa raon feidhme céanna,
nach bhfuil ceadaithe. Nuair a ritheann muid na tástálacha le haghaidh ár leabharlann, an cód i Liostú
Tiomsóidh 15-23 gan aon earráidí, ach ní theipeann ar an tástáil:

```consól
{{#include ../../listings/ch15-smart-pointers/listing-15-23/output.txt}}
```

Tabhair faoi deara go raibh scaoll ar an gcód leis an teachtaireacht `already borrowed:
BorrowMutError`. Seo mar a láimhseálann `RefCell<T>` sáruithe ar an iasacht
rialacha ag am rite.

Roghnú a dhéanamh ar earráidí iasachtaithe ag am rite seachas am a thiomsú, mar
atá déanta againn anseo, ciallaíonn sé seo go bhféadfadh sé go mbeadh botúin i do chód á aimsiú agat níos déanaí
sa phróiseas forbartha: b'fhéidir nach raibh go dtí gur úsáideadh do chód chuig
táirgeadh. Chomh maith leis sin, thabhódh do chód pionós beag feidhmíochta rite mar
mar thoradh ar na hiasachtaí a choinneáil ag am rite seachas am tiomsaithe.
Mar sin féin, trí úsáid a bhaint as `RefCell<T>` is féidir réad bréige a scríobh is féidir
modhnaigh é féin chun súil a choinneáil ar na teachtaireachtaí atá feicthe aige agus tú á úsáid
i gcomhthéacs nach gceadaítear ach luachanna neamh-inmhalartaithe. Is féidir leat `RefCell<T>` a úsáid
in ainneoin a chomhbhabhtálacha chun níos mó feidhmiúlachta a fháil ná tagairtí rialta
sholáthar.

### Úinéirí Iolracha Sonraí In-chomhshóite a bheith agat trí `Rc<T>` agus `RefCell<T>` a Chomhcheangal

Bealach coitianta `RefCell<T>` a úsáid is ea `Rc<T>`. Chun cuimhne go
Ligeann `Rc<T>` go bhfuil úinéirí iolracha agat ar roinnt sonraí, ach ní thugann sé ach do-athlasach
rochtain ar na sonraí sin. Má tá `Rc<T>` agat a bhfuil `RefCell<T>` agat, is féidir leat
faigh luach a fhéadfaidh _agus_ úinéirí iolracha a bheith agat ar féidir leat a shóchán!

Mar shampla, tabhair chun cuimhne an sampla liosta míbhuntáistí i Liostú 15-18 nuair a d’úsáideamar
`Rc<T>` chun liostaí iolracha a cheadú chun úinéireacht liosta eile a roinnt. Toisc
Ní choinníonn `Rc<T>` ach luachanna do-athchurtha, ní féidir linn aon cheann de na luachanna sa
liosta nuair a bheidh siad cruthaithe againn. Cuirimis isteach `RefCell<T>` chun an cumas a bhaint amach
athraigh na luachanna sna liostaí. Léiríonn liostú 15-24 gur trí úsáid a bhaint as a
`RefCell<T>` sa sainmhíniú `Cons`, is féidir linn an luach atá stóráilte a mhionathrú
na liostaí:

<Listing number="15-24" file-name="src/main.rs" caption="Using `Rc<RefCell<i32>>` to create a `List` that we can mutate">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-24/src/main.rs}}
```

</Listing>

Cruthaímid luach ar sampla é de `Rc<RefCell<i32>>` agus stóráilimid é i
athróg darb ainm `value` ionas gur féidir linn rochtain a fháil air níos déanaí. Ansin cruthaímid a
`List` in `a` le malairt `Cons` a choinníonn `value`. Ní mór dúinn clónáil
`value` mar sin tá úinéireacht ag `a` agus `value` araon ar an luach `5` istigh in áit
ná úinéireacht a aistriú ó `value` go `a` nó `a` a fháil ar iasacht uaidh
`value`.

Fillteaimid an liosta `a` i `Rc<T>` mar sin nuair a chruthaímid liostaí `b` agus `c`, déanann siad
in ann tagairt a dhéanamh do `a` araon, agus is é sin a rinne muid i Liostú 15-18.

Tar éis dúinn na liostaí in `a`,`b`, agus `c` a chruthú, ba mhaith linn 10 a chur leis an
luach i `value`. Déanaimid é seo trí `borrow_mut` a ghlaoch ar `value`, a úsáideann an
gné dhíreagartha uathoibríoch a phléamar i gCaibidil 5 (féach an rannán
[“Cá bhfuil an `->` Oibreoir?” [cá bhfuil an t-oibreoir---] <!-- déan neamhaird de -->) chun
déan tagairt don `Rc<T>` don luach `RefCell<T>` istigh. An `borrow_mut`
seolann an modh pointeoir cliste `RefMut<T>`, agus úsáidimid an t-oibreoir díthagartha
air agus athraigh an luach istigh.

Nuair a phriontáilimid `a`, `b`, agus `c`, feicimid go bhfuil na modhnaithe acu go léir
luach 15 seachas 5:

```consól
{{#include ../../listings/ch15-smart-pointers/listing-15-24/output.txt}}
```

Tá an teicníc seo go leor néata! Trí úsáid a bhaint as `RefCell<T>`, tá ceann amuigh againn
luach `List` do-laghdaithe. Ach is féidir linn na modhanna ar `RefCell<T>` a sholáthraíonn
rochtain ar a shoghluaisteacht istigh ionas gur féidir linn ár sonraí a mhodhnú nuair is gá dúinn.
Cosnaíonn seiceálacha ama rite na rialacha iasachtaíochta sinn ó rásaí sonraí, agus is amhlaidh atá
uaireanta is fiú beagán luas a thrádáil don tsolúbthacht seo inár sonraí
struchtúir. Tabhair faoi deara nach n-oibríonn `RefCell<T>` do chód ilshnáithe!
Is é `Mutex<T>` an ​​leagan sábháilte de `RefCell<T>` agus pléifimid
`Mutex<T>` i gCaibidil 16.

[wheres-the---operator]: ch05-03-method-syntax.html#wheres-the---operator	