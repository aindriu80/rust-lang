## Tréithe: Ag Sainmhíniú Iompar Comhroinnte

Sainmhíníonn _trait_ an fheidhmiúlacht atá ag cineál ar leith agus ar féidir leis a roinnt
cineálacha eile. Is féidir linn tréithe a úsáid chun iompar roinnte a shainiú ar bhealach teibí. muid
is féidir _trait bounds_ a úsáid chun a shonrú gur féidir le cineál cineálach a bheith ina chineál ar bith a bhfuil
iompar áirithe.

> Nóta: Tá tréithe cosúil le gné ar a dtugtar go minic _interfaces_ i gceann eile
> teangacha, cé go bhfuil roinnt difríochtaí ann.

### Tréith á Sainmhíniú

Is éard atá in iompar cineáil na modhanna ar féidir linn glaoch orthu ar an gcineál sin. Difriúil
roinneann cineálacha an t-iompar céanna más féidir linn na modhanna céanna a ghlaoch orthu sin go léir
cineálacha. Is bealach iad sainmhínithe tréithe chun sínithe modhanna a ghrúpáil le chéile chun
sraith iompraíochtaí a shainiú atá riachtanach chun cuspóir éigin a bhaint amach.

Mar shampla, lig dúinn a rá go bhfuil struchtúir iolracha againn a bhfuil cineálacha éagsúla agus
méideanna téacs: struchtúr `NewsArticle` a choinníonn scéal nuachta comhdaithe in a
suíomh ar leith agus `Tweet` ar féidir, ar a mhéad, 280 carachtar a bheith ann
le meiteashonraí a thugann le fios cé acu tweet nua, retweet nó freagra a bhí ann
chuig tweet eile.

Ba mhaith linn cliathbhosca leabharlainne comhbhailitheoir meán a dhéanamh darb ainm `aggregator` is féidir
taispeáin achoimrí ar shonraí a d'fhéadfaí a stóráil in `NewsArticle` nó `Tweet`
shampla. Chun seo a dhéanamh, tá achoimre de dhíth orainn ó gach cineál, agus iarrfaimid é sin
achoimre trí mhodh `summarize` a ghlaoch ar shampla. Léiríonn liostú 10-12 an
sainmhíniú ar thréith `Summary` phoiblí a chuireann an t-iompar seo in iúl.

<Listing number="10-12" file-name="src/lib.rs" caption="A `Summary` trait that consists of the behavior provided by a `summarize` method">

```rust,noplayground
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-12/src/lib.rs}}
```

</Listing>

Anseo, dearbhaímid tréith ag baint úsáide as an eochairfhocal `trait` agus ansin ainm an trait,
atá `Summary` sa chás seo. Dearbhaímid freisin gur `Summary` an trait ionas go
is féidir le cliathbhoscaí ag brath ar an gcliathbhosca seo úsáid a bhaint as an tréith seo freisin, mar a fheicfimid ann
cúpla sampla. Taobh istigh de na lúibíní curly, dearbhaímid na sínithe modh
a chuireann síos ar iompraíocht na gcineálacha a chuireann an trait seo i bhfeidhm, atá i
is é an cás seo ná `fn summarize(&self) -> String`.

Tar éis an síniú modh, in ionad cur i bhfeidhm a sholáthar laistigh de chatach
lúibíní, úsáidimid leathstad. Ní mór do gach cineál a chuireann an tréith seo chun feidhme a sholáthar
a iompar saincheaptha féin le haghaidh an comhlacht ar an modh. Cuirfidh an tiomsaitheoir i bhfeidhm
go mbeidh an modh `summarize` ag aon chineál a bhfuil an trait `Summary` aige
sainmhínithe go díreach leis an síniú seo.

Is féidir le tréith modhanna iolracha a bheith ina chorp: tá na sínithe modh liostaithe
ceann in aghaidh an líne, agus críochnaíonn gach líne i leathstad.

### Tréith ar Chineál a Chur i bhFeidhm

Anois go bhfuil sínithe inmhianaithe na modhanna `Summary` sainithe againn,
is féidir linn é a chur i bhfeidhm ar na cineálacha inár gcomhbhailitheoir meáin. Liostáil 10-13 seónna
cur i bhfeidhm na tréithe `Summary` ar an struchtúr `NewsArticle` a úsáideann
an ceannlíne, an t-údar, agus an suíomh chun luach aischuir a chruthú
`summarize`. Maidir leis an struchtúr `Tweet`, sainmhínímid `summarize` mar an t-ainm úsáideora
ina dhiaidh sin téacs iomlán an tweet, ag glacadh leis go bhfuil an t-ábhar tweet
teoranta do 280 carachtar cheana féin.

<Listing number="10-13" file-name="src/lib.rs" caption="Implementing the `Summary` trait on the `NewsArticle` and `Tweet` types">

```rust,noplayground
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-13/src/lib.rs:here}}
```

</Listing>

Tá cur i bhfeidhm tréith ar chineál cosúil le modhanna rialta a chur i bhfeidhm. Tá an
difríocht is ea gur tar éis `impl`, cuirimid an t-ainm trait ba mhaith linn a chur i bhfeidhm,
ansin bain úsáid as an eochairfhocal `for`, agus ansin sonraigh ainm an chineáil a theastaíonn uainn
an trait a chur i bhfeidhm le haghaidh. Laistigh den bhloc `impl`, chuireamar na sínithe modha
atá sainmhínithe ag an sainiú trait. In ionad leathstad a chur leis i ndiaidh gach ceann acu
síniú, úsáidimid lúibíní curly agus líon isteach an comhlacht modh leis an sainiúil
iompar a theastaíonn uainn go mbeadh modhanna an trait don chineál áirithe.

Anois go bhfuil an trait `Summary` ar `NewsArticle` agus
`Tweet`, is féidir le húsáideoirí an chliabháin na modhanna trait a ghlaoch ar chásanna de
`NewsArticle` agus `Tweet` ar an mbealach céanna a dtugaimid modhanna rialta orthu. An t-aon
difríocht ná go gcaithfidh an t-úsáideoir an tréith a thabhairt isteach sa raon feidhme chomh maith leis an
cineálacha. Seo sampla den chaoi a bhféadfadh cliathbhosca dénártha ár `aggregator` a úsáid
cliathbhosca leabharlainne:

```rust,ignore
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-01-calling-trait-method/src/main.rs}}
```

Priontálann an cód seo `1 new tweet: horse_ebooks: of course, as you probably already
know, people`.

Is féidir le cliathbhoscaí eile a bhraitheann ar an gcliathbhosca `aggregator` an `Summary` a thabhairt freisin
tréith isteach sa scóip chun `Summary` a chur i bhfeidhm ar a gcineálacha féin. Srian amháin le
Tabhair faoi deara nach féidir linn tréith a chur i bhfeidhm ar chineál ach amháin má tá an trait nó an
cineál, nó iad araon, áitiúil dár gcliathbhosca. Mar shampla, is féidir linn caighdeán a chur i bhfeidhm
tréithe leabharlainne cosúil le `Display` ar chineál saincheaptha mar `Tweet` mar chuid dár
feidhmiúlacht cliathbhosca `aggregator` toisc go bhfuil an cineál `Tweet` áitiúil dár gcuid
cliathbhosca `aggregator`. Is féidir linn freisin `Summary` ar `Vec<T>` a chur i bhfeidhm inár
cliathbhosca `aggregator` toisc go bhfuil an trait `Summary` áitiúil dár `aggregator`
cliathbhosca.

Ach ní féidir linn tréithe seachtracha a chur i bhfeidhm ar chineálacha seachtracha. Mar shampla, ní féidir linn
cuir an trait `Display` ar `Vec<T>` i bhfeidhm laistigh dár gcliathbhosca `aggregator` toisc
Sainmhínítear `Display` agus `Vec<T>` araon sa ghnáthleabharlann agus níl siad
áitiúil dár gcliathbhosca `aggregator`. Is cuid de mhaoin ar a dtugtar an srian seo
_coherence_, agus go sonrach an riail _orphan_, ainmnithe amhlaidh mar gheall ar an
níl cineál tuismitheora i láthair. Cinntíonn an riail seo nach féidir cód daoine eile
briseadh do chód agus vice versa. Gan an riail, d'fhéadfadh dhá chliabhán a chur i bhfeidhm
an tréith chéanna don chineál céanna, agus ní bheadh ​​a fhios ag Rust cén cur i bhfeidhm
a úsáid.

### Feidhmithe Réamhshocraithe

Uaireanta bíonn sé úsáideach iompar réamhshocraithe a bheith agat le haghaidh cuid de na modhanna nó gach ceann díobh
i tréith in ionad feidhmiúcháin a éileamh do gach modh ar gach cineál.
Ansin, de réir mar a chuirimid an trait i bhfeidhm ar chineál áirithe, is féidir linn a choinneáil nó a shárú
iompraíocht réamhshocraithe gach modha.

I Liostú 10-14, sonraímid teaghrán réamhshocraithe don mhodh `summarize` den
Tréith `Summary` in ionad an síniú modha amháin a shainiú, mar a rinneamar i
Liostáil 10-12.

<Listing number="10-14" file-name="src/lib.rs" caption="Defining a `Summary` trait with a default implementation of the `summarize` method">

```rust,noplayground
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-14/src/lib.rs:here}}
```

</Listing>

Chun feidhmchlár réamhshocraithe a úsáid chun achoimre a dhéanamh ar chásanna de `NewsArticle`, déanaimid
sonraigh bloc `impl` folamh le `impl Summary for NewsArticle {}`.

Cé nach bhfuilimid ag sainiú an mhodha `summarize` ar `NewsArticle` a thuilleadh
go díreach, chuireamar cur i bhfeidhm réamhshocraithe ar fáil agus shonraigh muid é sin
Cuireann `NewsArticle` an trait `Summary` i bhfeidhm. Mar thoradh air sin, is féidir linn glaoch fós
an modh `summarize` ar shampla de `NewsArticle`, mar seo:

```rust,ignore
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-02-calling-default-impl/src/main.rs:here}}
```

Priontálann an cód seo `New article available! (Read more...)`.

Ní gá dúinn aon rud a athrú chun forfheidhmiú réamhshocraithe a chruthú
cur i bhfeidhm `Summary` ar `Tweet` i Liosta 10-13. Is é an chúis atá leis sin
is ionann an chomhréir chun cur i bhfeidhm réamhshocraithe a shárú agus an chomhréir
chun modh trait a chur i bhfeidhm nach bhfuil cur i bhfeidhm réamhshocraithe aige.

Is féidir le cur i bhfeidhm réamhshocraithe modhanna eile sa tréith chéanna a ghlaoch, fiú amháin más iad sin
níl cur i bhfeidhm réamhshocraithe ag modhanna eile. Ar an mbealach seo, is féidir le trait
go leor feidhmiúlacht úsáideach a sholáthar agus ní gá ach na hoibreoirí a shonrú
cuid bheag de. Mar shampla, d'fhéadfaimis an tréithe `Summary` a shainiú chun a
modh `summarize_author` a bhfuil a chur i bhfeidhm ag teastáil, agus ansin sainigh a
modh `summarize` a bhfuil cur i bhfeidhm réamhshocraithe aige a ghlaonn an
modh `summarize_author`:

```rust,noplayground
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-03-default-impl-calls-other-methods/src/lib.rs:here}}
```

Chun an leagan seo de `Summary` a úsáid, ní gá dúinn ach `summarize_author` a shainiú
nuair a chuirimid an trait i bhfeidhm ar chineál:

```rust,ignore
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-03-default-impl-calls-other-methods/src/lib.rs:impl}}
```

Tar éis dúinn `summarize_author` a shainiú, is féidir linn `summarize` a ghlaoch ar chásanna an
Beidh `Tweet` struct, agus cur i bhfeidhm réamhshocraithe `summarize` glaoch ar an
sainmhíniú ar `summarize_author` atá curtha ar fáil againn. Toisc go bhfuil muid curtha i bhfeidhm
`summarize_author`, thug an trait `Summary` iompar an
modh `summarize` gan a cheangal orainn a thuilleadh cód a scríobh. Seo a bhfuil
is cosúil:

```rust,ignore
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-03-default-impl-calls-other-methods/src/main.rs:here}}
```

Priontálann an cód seo `1 new tweet: (Read more from @horse_ebooks...)`.

Tabhair faoi deara nach féidir an forfheidhmiú réamhshocraithe a ghlaoch ó
cur i bhfeidhm an mhodha chéanna sin a shárú.

### Tréithe mar Pharaiméadair

Anois go bhfuil a fhios agat conas tréithe a shainiú agus a chur i bhfeidhm, is féidir linn iniúchadh a dhéanamh ar conas iad a úsáid
tréithe a shainiú feidhmeanna a ghlacann go leor cineálacha éagsúla. Bainfimid úsáid as an
Tréith `Summary` chuireamar i bhfeidhm ar na cineálacha `NewsArticle` agus `Tweet` in
Ag liostú 10-13 chun feidhm `notify` a shainiú a dtugtar an modh `summarize` air
ar a pharaiméadar `item`, atá de shaghas éigin a chuireann an `Summary` i bhfeidhm
trait. Chun seo a dhéanamh, úsáidimid an chomhréir `impl Trait`, mar seo:

```rust,ignore
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-04-traits-as-parameters/src/lib.rs:here}}
```

In ionad cineál nithiúil don pharaiméadar `item`, sonraímid an `impl`
eochairfhocal agus an t-ainm trait. Glacann an paraiméadar seo le haon chineál a chuireann an
tréith shonraithe. I gcorp an `notify`, is féidir linn glaoch ar aon mhodhanna ar `item`
a thagann as an trait `Summary`, mar shampla `summarize`. Is féidir linn `notify` a ghlaoch
agus pas a fháil in aon chás de `NewsArticle` nó `Tweet`. Cód a ghlaonn an
feidhmiú le haon chineál eile, mar shampla `String` nó `i32`, ní thiomsóidh
toisc nach gcuireann na cineálacha sin `Summary` i bhfeidhm.

<!-- Sean-cheannteidil. Ná bain amach nó seans go mbrisfidh naisc. -->

<a id="fixing-the-more-function-with-trait-bounds"></a>

#### Comhréir Trait Bound

Feidhmíonn an chomhréir `impl Trait` do chásanna simplí ach is comhréir é i ndáiríre
siúcra le haghaidh foirm níos faide ar a dtugtar _trait bound_; Breathnaíonn sé mar seo:

```rust,ignore
pub fn notify<T: Summary>(item: &T) {
    println!("Breaking news! {}", item.summarize());
}
```

Tá an fhoirm níos faide seo comhionann leis an sampla sa roinn roimhe seo ach tá
níos briathar. Cuirimid teorainneacha tréithe leis an dearbhú den chineál cineálach
paraiméadar tar éis idirstad agus laistigh de lúibíní uillinn.

Tá an chomhréir `impl Trait` áisiúil agus cruthaíonn sé cód níos gonta go simplí
cásanna, agus is féidir leis an gcomhréir tréithe níos iomláine castacht a chur in iúl i gcásanna eile
cásanna. Mar shampla, is féidir dhá pharaiméadar a bheith againn a chuireann `Summary` i bhfeidhm. Ag déanamh
mar sin tá cuma mar seo ar chomhréir `impl Trait`:

```rust,ignore
pub fn notify(item1: &impl Summary, item2: &impl Summary) {
```

Is cuí `impl Trait` a úsáid má theastaíonn uainn go gceadódh an fheidhm seo `item1` agus
cineálacha éagsúla a bheith ag `item2` (chomh fada agus a chuireann an dá chineál `Summary` i bhfeidhm). Más rud é
ba mhaith linn iallach a chur ar an dá paraiméadair a bheith ar an gcineál céanna, áfach, ní mór dúinn a úsáid a
trait faoi cheangal, mar seo:

```rust,ignore
pub fn notify<T: Summary>(item1: &T, item2: &T) {
```

Sonraítear an cineál cineálach `T` mar an cineál `item1` agus `item2`
paraiméadair srianta ar an bhfeidhm den sórt sin go bhfuil an cineál nithiúla an luach
a rith mar argóint ar son `item1` agus caithfidh `item2` a bheith mar an gcéanna.

#### Ag sonrú na dTréithe Iolracha leis an gComhréir `+`

Is féidir linn níos mó ná tréith amháin a shonrú freisin. Abair go raibh muid ag iarraidh `notify` a úsáid
formáidiú taispeána chomh maith le `summarize` ar `item`: sonraímid sa `notify`
sainmhíniú go gcaithfidh `item` `Display` agus `Summary` araon a chur i bhfeidhm. Is féidir linn a dhéanamh
mar sin ag baint úsáide as an chomhréir `+`:

```rust,ignore
pub fn notify(item: &(impl Summary + Display)) {
```

Tá an chomhréir `+` bailí freisin le teorainneacha tréithe ar chineálacha cineálacha:

```rust,ignore
pub fn notify<T: Summary + Display>(item: &T) {
```

Leis an dá theorainn tréith sonraithe, is féidir le corp an `notify` `summarize` a ghlaoch
agus úsáid `{}` chun `item` a fhormáidiú.

#### Tréith níos Soiléire Teorainneacha le Clásail `áit`

Tá míbhuntáistí ag baint le húsáid an iomarca teorainneacha trait. Tá a thréith féin ag gach cineálach
teorainneacha, mar sin is féidir go leor feidhmeanna a bhfuil paraiméadair chineálacha iolracha acu
faisnéis faoi cheangal idir ainm na feidhme agus a liosta paraiméadar,
rud a fhágann gur deacair síniú na feidhme a léamh. Ar an gcúis seo, tá malartach ag Rust
Comhréir chun teorainneacha tréithe a shonrú taobh istigh de chlásal `where` i ndiaidh na feidhme
síniú. Mar sin, in ionad é seo a scríobh:

```rust,ignore
fn some_function<T: Display + Clone, U: Clone + Debug>(t: &T, u: &U) -> i32 {
```

we can use a `where` clause, like this:

```rust,ignore
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-07-where-clause/src/lib.rs:here}}
```

Níl an oiread sin bearrtha ar shíniú na feidhme seo: ainm na feidhme, liosta paraiméadar,
agus cineál fillte gar dá chéile, cosúil le feidhm gan go leor tréithe
teorainneacha.

### Cineálacha Filleadh a chuireann Tréithe i bhFeidhm

Is féidir linn an chomhréir `impl Trait` a úsáid freisin sa suíomh fillte chun aischur a
luach de shaghas éigin a chuireann trait i bhfeidhm, mar a thaispeántar anseo:

```rust,ignore
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-05-returning-impl-trait/src/lib.rs:here}}
```

Trí úsáid a bhaint as `impl Summary` don chineál tuairisceáin, sonraímid go bhfuil an
Filleann an fheidhm `returns_summarizable` cineál éigin a chuireann an `Summary` i bhfeidhm
trait gan an cineál coincréit a ainmniú. Sa chás seo, `returns_summarizable`
seolann sé `Tweet` ar ais, ach ní gá go mbeadh a fhios sin ag an gcód a ghlaonn an fheidhm seo.

Tá an cumas chun cineál tuairisceáin a shonrú de réir na tréithe a chuireann sé i bhfeidhm amháin
úsáideach go háirithe i gcomhthéacs dúnadh agus atrialltóirí, a chlúdaímid iontu
Caibidil 13. Cruthaíonn dúnta agus iterators cineálacha nach bhfuil a fhios ach ag an tiomsaitheoir nó
cineálacha atá an-fhada a shonrú. Ligeann an chomhréir `impl Trait` tú go gonta
sonraigh go bhfilleann feidhm cineál éigin a chuireann an trait `Iterator` i bhfeidhm
gan gá le cineál an-fhada a scríobh amach.

Mar sin féin, ní féidir leat `impl Trait` a úsáid ach amháin má tá cineál amháin á sheoladh ar ais agat. Le haghaidh
mar shampla, an cód seo a sheolann ceachtar `NewsArticle` nó `Tweet` leis an
ní n-oibreodh an cineál tuairisceáin atá sonraithe mar `impl Summary`:

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-06-impl-trait-returns-one-type/src/lib.rs:here}}
```

Ní cheadaítear 'Nuacht-Airteagal' nó 'Tweet' a thabhairt ar ais de bharr srianta
thart ar an gcaoi a gcuirtear an chomhréir `impl Trait` i bhfeidhm sa tiomsaitheoir. Clúdóidh muid
conas feidhm a scríobh leis an iompar seo sa [“Ag Úsáid Réada Tréith a Ligeann Luachanna de Chineálacha Éagsúla”][using-trait-objects-that-allow-for-values-of-different-types]<!--
neamhaird a dhéanamh ar --> alt de Chaibidil 18.

### Ag Úsáid Teorainneacha Trait chun Modhanna a Chur i bhFeidhm go Coinníollach

Trí úsáid a bhaint as tréith atá faoi cheangal le bloc `impl` a úsáideann paraiméadair chineálacha,
is féidir linn modhanna a chur i bhfeidhm go coinníollach le haghaidh cineálacha a chuireann an sonraithe i bhfeidhm
tréithe. Mar shampla, cuireann an cineál `Pair<T>` i Liosta 10-15 i bhfeidhm i gcónaí an
feidhm `new` chun sampla nua de `Pair<T>` a thabhairt ar ais (aisghlaoch ón
[“Modhanna a Shainmhíniú”][methods]<!-- neamhaird a dhéanamh ar --> roinn de Chaibidil 5 a dhéanann `Self`
is ailias cineál é don chineál bloc `impl`, atá sa chás seo
`Pair<T>`). Ach sa chéad bhloc `impl` eile, ní chuireann `Pair<T>` i bhfeidhm ach an
modh `cmp_display` má chuireann a chineál inmheánach `T` an trait `PartialOrd` i bhfeidhm
a chumasaíonn comparáid _agus_ an tréithe `Display` a chumasaíonn priontáil.

<Listing number="10-15" file-name="src/lib.rs" caption="Conditionally implementing methods on a generic type depending on trait bounds">

```rust,noplayground
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-15/src/lib.rs}}
```

</Listing>

Is féidir linn freisin tréith a chur i bhfeidhm go coinníollach d'aon chineál a chuireann i bhfeidhm
tréith eile. Cur i bhfeidhm tréith ar aon chineál a shásaíonn an tréith
tugtar _blanket implementations_ ar theorainneacha agus úsáidtear go forleathan iad sna
Leabharlann chaighdeánach meirge. Mar shampla, cuireann an leabharlann chaighdeánach an
Tréith `ToString` ar aon chineál a chuireann an trait `Display` i bhfeidhm. An `impl`
Breathnaíonn an bloc sa ghnáthleabharlann cosúil leis an gcód seo:

```rust,ignore
impl<T: Display> ToString for T {
    // --snip--
}
```

Toisc go bhfuil an cur i bhfeidhm cuimsitheach seo ag an leabharlann chaighdeánach, is féidir linn an
modh `to_string` arna shainiú ag an tréith `ToString` ar aon chineál a fheidhmíonn
an trait `Display`. Mar shampla, is féidir linn slánuimhreacha a thiontú ina gcuid comhfhreagrach
Luachanna `String` mar seo toisc go gcuireann slánuimhreacha `Display` i bhfeidhm:

```rust
let s = 3.to_string();
```

Tá cur i bhfeidhm blaincéid le feiceáil sa doiciméadú don trait sa
Alt “Feidhmitheoirí”.

Ligeann tréithe agus teorainneacha tréithe dúinn cód a scríobh a úsáideann paraiméadair chineálacha chun
dúbailt a laghdú ach sonraigh freisin don tiomsaitheoir gur mian linn an cineálach
cineál a bhfuil iompar ar leith. Is féidir leis an tiomsaitheoir an tréith faoi cheangal a úsáid ansin
faisnéis le seiceáil go soláthraíonn na cineálacha coincréite go léir a úsáidtear lenár gcód an
iompar ceart. I dteangacha atá clóscríofa go dinimiciúil, gheobhaimid earráid ag
am rite má ghlaomar modh ar chineál nár shainigh an modh. Ach
Bogann Rust na hearráidí seo chun am a thiomsú agus mar sin tá iallach orainn na fadhbanna a réiteach
sula mbeidh ár gcód fiú in ann a rith. Ina theannta sin, ní gá dúinn cód a scríobh
a sheiceálann iompar ag am rite toisc go bhfuil seiceáil déanta againn cheana féin tráth an tiomsaithe
am. Má dhéantar amhlaidh, feabhsaíonn sé an fheidhmíocht gan an tsolúbthacht a thabhairt suas
de chineálacha.

[using-trait-objects-that-allow-for-values-of-different-types]: ch18-02-trait-objects.html#using-trait-objects-that-allow-for-values-of-different-types
[methods]: ch05-03-method-syntax.html#defining-methods

