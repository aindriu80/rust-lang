## Cineálacha Ardleibhéil

Tá roinnt gnéithe ag córas cineáil Rust atá luaite againn go dtí seo ach nár phléamar fós. Tosaímid trí phlé a dhéanamh ar newtypes i gcoitinne agus muid ag scrúdú cén fáth
a bhfuil newtypes úsáideach mar chineálacha. Ansin bogfaimid ar aghaidh chuig leasainmneacha cineáil, gné
atá cosúil le newtypes ach le séimeantaic beagán difriúil. Pléifimid freisin
an cineál `!` agus cineálacha méide dinimiciúla.

### Ag Úsáid an Phatrúin Newtype le haghaidh Sábháilteachta agus Astarraingt Cineáil

> Nóta: Glacann an chuid seo leis gur léigh tú an chuid roimhe seo [“Ag Úsáid an
> Phatrúin Newtype chun Tréithe Seachtracha a Chur i bhFeidhm ar Chineálacha
> Seachtracha.”][using-the-newtype-pattern]<!-- neamhaird -->

Tá an patrún newtype úsáideach freisin le haghaidh tascanna thar na cinn atá pléite againn go dtí seo, lena n-áirítear a fhorfheidhmiú go statach nach mbíonn luachanna mearbhall riamh agus
aonaid luacha a léiriú. Chonaic tú sampla d'úsáid cineálacha nua chun
aonaid a léiriú i Liosta 20-16: cuimhnigh gur fhill na struchtúir `Millimeters` agus `Meters` luachanna `u32` i gcineál nua. Dá scríobhfaimis feidhm le
paraiméadar de chineál `Millimeters`, ní fhéadfaimis clár a thiomsú a
dhéanadh iarracht trí thimpiste an fheidhm sin a ghlaoch le luach de chineál `Meters` nó
`u32` simplí.

Is féidir linn an patrún cineál nua a úsáid freisin chun roinnt sonraí cur i bhfeidhm de chineál a bhaint amach: is féidir leis an gcineál nua API poiblí a nochtadh atá difriúil ó
API an chineáil inmheánaigh phríobháidigh.

Is féidir le cineálacha nua cur i bhfeidhm inmheánach a cheilt freisin. Mar shampla, d'fhéadfaimis cineál
`People` a sholáthar chun `HashMap<i32, String>` a fhilleadh a stórálann aitheantas duine
a bhaineann lena ainm. Ní idirghníomhódh cód a úsáideann `People` ach leis an
API poiblí a sholáthraímid, amhail modh chun teaghrán ainm a chur leis an mbailiúchán `People`; Ní bheadh ​​ar an gcód sin a fhios a bheith aige go sanntaímid ID `i32` d'ainmneacha
go hinmheánach. Is bealach éadrom é an patrún newtype chun ionchapslú a bhaint amach
chun sonraí cur i bhfeidhm a cheilt, rud a phléamar sa chuid [“Encapsulation that
Hides Implementation
Details”][encapsulation-that-hides-implementation-details]<!-- ignore -->
de Chaibidil 18.

### Comhchiallaigh Chineáil a Chruthú le hAiliasanna Chineáil

Soláthraíonn Rust an cumas chun _alias_ cineál a dhearbhú chun ainm eile a thabhairt do chineál atá ann cheana
. Chuige seo úsáidimid an eochairfhocal `type`. Mar shampla, is féidir linn
an t-ailias `Kilometers` a chruthú go `i32` mar seo:

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-04-kilometers-alias/src/main.rs:here}}
```

Anois, is _comhchiallach_ é an leasainm `Kilometers` le haghaidh `i32`; murab ionann agus na cineálacha `Millimeters` agus `Meters` a chruthaíomar i Liosta 20-16, ní cineál nua ar leithligh é `Kilometers`. Déileálfar le luachanna den chineál `Kilometers` ar an mbealach céanna le luachanna den chineál `i32`:

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-04-kilometers-alias/src/main.rs:there}}
```

Ós rud é gur den chineál céanna iad `Kilometers` agus `i32`, is féidir linn luachanna den dá chineál a chur leis agus is féidir linn luachanna `Kilometers` a chur ar aghaidh chuig feidhmeanna a ghlacann paraiméadair `i32`. Mar sin féin, ag baint úsáide as an modh seo, ní fhaighimid na buntáistí seiceála cineáil a fhaighimid ón patrún nuachineáil a pléadh níos luaithe. I bhfocail eile, má mheascann muid luachanna `Kilometers` agus `i32` áit éigin, ní thabharfaidh an tiomsaitheoir earráid dúinn.

Is é an príomhchás úsáide le haghaidh comhchiallaigh cineáil ná athrá a laghdú. Mar shampla, d'fhéadfadh cineál fada a bheith againn mar seo:

```rust,ignore
Box<dyn Fn() + Send + 'static>
```

Is féidir go mbeadh sé tuirsiúil agus seans maith go dtarlóidh earráidí an cineál fada seo a scríobh i sínithe feidhme agus mar anótálacha cineáil ar fud an chóid. Samhlaigh tionscadal lán de chód mar atá i Liosta 20-25.

<Listing number="20-25" caption="Using a long type in many places">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-25/src/main.rs:here}}
```

</Listing>

Déanann leasainm cineáil an cód seo níos inbhainistithe tríd an athrá a laghdú. I Liostálacha 20-26, thugamar isteach leasainm darb ainm `Thunk` don chineál focal agus is féidir leis gach úsáid den chineál a athsholáthar leis an leasainm níos giorra `Thunk`.

<Listing number="20-26" caption="Introducing a type alias `Thunk` to reduce repetition">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-26/src/main.rs:here}}
```

</Listing>

Tá an cód seo i bhfad níos éasca le léamh agus le scríobh! Is féidir le hainm bríoch a roghnú do
bhréagán cineáil cabhrú le do rún a chur in iúl freisin (is focal é _thunk_ do chód
atá le meastóireacht ag tráth níos déanaí, mar sin is ainm oiriúnach é do dhúnadh a
stóráiltear).

Úsáidtear bréagáin cineáil go coitianta leis an gcineál `Result<T, E>` chun athrá a laghdú. Smaoinigh ar an modúl `std::io` sa leabharlann chaighdeánach. Is minic a thugann oibríochtaí ionchuir/aschur `Result<T, E>` ar ais chun déileáil le cásanna nuair a
theipeann ar oibríochtaí oibriú. Tá struchtúr `std::io::Error` ag an leabharlann seo a léiríonn gach
earráid ionchuir/aschur féideartha. Beidh go leor de na feidhmeanna i `std::io` ag filleadh
`Result<T, E>` áit a bhfuil an `E` ina `std::io::Error`, amhail na feidhmeanna seo sa
tréith `Write`:

```rust,noplayground
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-05-write-trait/src/lib.rs}}
```

Déantar an `Result<..., Error>` a athdhéanamh go minic. Dá bhrí sin, tá an cineál dearbhaithe ailias seo ag `std::io`:

```rust,noplayground
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-06-result-alias/src/lib.rs:here}}
```

Ós rud é go bhfuil an dearbhú seo sa mhodúl `std::io`, is féidir linn an leasainm láncháilithe `std::io::Result<T>` a úsáid; is é sin, `Result<T, E>` leis an `E` líonta isteach mar `std::io::Error`. Seo mar a chríochnaíonn sínithe na feidhme tréithe `Write`:

```rust,noplayground
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-06-result-alias/src/lib.rs:there}}

```

Cuidíonn an cineál leasainm ar dhá bhealach: déanann sé níos éasca cód a scríobh _agus_ tugann sé
comhéadan comhsheasmhach dúinn ar fud `std::io` ar fad. Toisc gur leasainm é, níl ann
ach `Result<T, E>` eile, rud a chiallaíonn gur féidir linn aon mhodhanna a oibríonn ar
`Result<T, E>` a úsáid leis, chomh maith le comhréir speisialta cosúil leis an oibreoir `?`.

### An Cineál Nár Fhill Nár Fhill Nár Fhill

Tá cineál speisialta ag Rust darb ainm `!` ar a dtugtar i dteanga teoiric an chineáil mar an
_cineál folamh_ toisc nach bhfuil aon luachanna aige. Is fearr linn an cineál _náimh_ a thabhairt air
toisc go seasann sé in áit an chineáil fillte nuair nach bhfillfidh feidhm
nár fhill. Seo sampla:


```rust,noplayground
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-07-never-type/src/lib.rs:here}}
```

Léitear an cód seo mar “ní thugann an fheidhm `bar` riamh ar ais.” Tugtar _feidhmeanna divergacha_ ar fheidhmeanna a thugann
riamh ar ais. Ní féidir linn luachanna den chineál `!` a chruthú
mar sin ní féidir le `bar` riamh ar ais.

Ach cén úsáid atá i gcineál nach féidir leat luachanna a chruthú dó riamh? Cuimhnigh ar an gcód ó
Liostú 2-5, cuid den chluiche tomhaise uimhreacha; tá cuid de atáirgthe againn
anseo i Liostú 20-27.

<Listing number="20-27" caption="A `match` with an arm that ends in `continue`">

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-05/src/main.rs:ch19}}
```

</Listing>

Ag an am, scipeáileamar thar roinnt sonraí sa chód seo. I gCaibidil 6 sa rannóg [“An
`match` Control Flow Operator”][the-match-control-flow-operator]<!-- ignore -->
phléamar go gcaithfidh gach arm `match` an cineál céanna a thabhairt ar ais. Mar sin, mar shampla, ní oibríonn an cód seo a leanas:

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-08-match-arms-different-types/src/main.rs:here}}
```

Bheadh ​​ar an gcineál `guess` sa chód seo a bheith ina shlánuimhir _agus_ teaghrán,
agus éilíonn Rust nach mbeadh ach cineál amháin ag `guess`. Mar sin, cad a thugann `continue`
ar ais? Conas a ceadaíodh dúinn `u32` a thabhairt ar ais ó lámh amháin agus lámh eile a bheith againn
a chríochnaíonn le `continue` i Liosta 20-27?

Mar a bheifeá ag súil leis, tá luach `!` ag `continue`. Is é sin le rá, nuair a ríomhann Rust
an cineál `guess`, féachann sé ar an dá lámh mheaitseála, an chéad cheann le
luach `u32` agus an dara ceann le luach `!`. Toisc nach féidir le `!` luach a bheith aige
choíche, socraíonn Rust gurb é `u32` an cineál `guess`.

Is é an bealach foirmiúil chun an t-iompar seo a chur síos ná gur féidir léirithe de chineál `!` a
bhrú isteach in aon chineál eile. Ceadaítear dúinn an lámh `match` seo a chríochnú le
`continue` toisc nach dtugann `continue` luach ar ais; ina ionad sin, bogann sé an rialú ar ais go barr an lúibe, mar sin i gcás `Err`, ní shanntar luach riamh do
`guess`.

Tá an cineál never úsáideach leis an macra `panic!` chomh maith. Cuimhnigh ar an bhfeidhm `unwrap`
a nglaoimid ar luachanna `Option<T>` chun luach nó panic a tháirgeadh leis an
sainmhíniú seo:

```rust,ignore
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-09-unwrap-definition/src/lib.rs:here}}
```

Sa chód seo, tarlaíonn an rud céanna agus atá sa `match` i Liosta 20-27: Feiceann Rust go bhfuil an cineál `T` ag `val` agus go bhfuil an cineál `!` ag `panic!`, mar sin is é `T` toradh an abairt `match` iomláin. Oibríonn an cód seo toisc nach dtáirgeann `panic!` luach; críochnaíonn sé an clár. Sa chás `None`, ní bheimid
ag filleadh luach ó `unwrap`, mar sin tá an cód seo bailí.

Is léiriú deiridh amháin é `loop` a bhfuil an cineál `!` aige:

```rust,ignore
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-10-loop-returns-never/src/main.rs:here}}
```

Anseo, ní chríochnaíonn an lúb choíche, mar sin is é `!` luach an abairt. Mar sin féin, ní bheadh ​​sé seo fíor dá gcuirfimis `break` san áireamh, mar go gcríochnódh an lúb
nuair a shroichfeadh sé an `break`.

### Cineálacha Méide Dinimiciúla agus an Tréith `Méide`

Caithfidh Rust sonraí áirithe a bheith ar eolas aige faoina chineálacha, amhail cé mhéad spáis atá le
leithdháileadh do luach de chineál áirithe. Fágann sé seo cúinne amháin dá chóras
cineálacha beagán mearbhall ar dtús: coincheap na _cineálacha méide dinimiciúla_.
Uaireanta tugtar _DSTanna_ nó _cineálacha neamhmhéide_ orthu, ligeann na cineálacha seo dúinn
cód a scríobh ag baint úsáide as luachanna nach féidir linn a méid a bheith ar eolas againn ach ag am rith.

Déanaimis tochailt isteach i sonraí cineál méide dinimiciúil ar a dtugtar `str`, a
bhíomar ag úsáid ar fud an leabhair. Sin ceart, ní `&str`, ach `str` leis féin, is DST é. Ní féidir linn a fháil amach cé chomh fada is atá an teaghrán go dtí go mbeidh an t-am rite ann, rud a chiallaíonn nach féidir linn athróg de chineál `str` a chruthú, ná ní féidir linn argóint de chineál `str` a ghlacadh. Smaoinigh ar an gcód seo a leanas, nach n-oibríonn:

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-11-cant-create-str/src/main.rs:here}}
```

Caithfidh Rust a fhios a bheith aige cé mhéad cuimhne atá le leithdháileadh d'aon luach de chineál áirithe, agus ní mór do gach luach de chineál an méid céanna cuimhne a úsáid. Dá gceadódh Rust dúinn an cód seo a scríobh, bheadh ​​ar an dá luach `str` seo an méid céanna spáis a thógáil. Ach tá faid éagsúla acu: teastaíonn 12 bheart stórála ó `s1` agus teastaíonn 15 ó `s2`. Sin é an fáth nach féidir athróg a chruthú ina bhfuil cineál méide dinimiciúil.

Mar sin, cad a dhéanaimid? Sa chás seo, tá an freagra ar eolas agat cheana féin: déanaimid na cineálacha `s1` agus `s2` ina `&str` seachas ina `str`. Cuimhnigh ón rannóg [“String
Slices”][string-slices]<!-- ignore --> de Chaibidil 4 nach stórálann struchtúr sonraí an tslis ach an suíomh tosaigh agus fad an tslis. Mar sin
cé gur luach aonair é `&T` a stórálann seoladh cuimhne an áit a bhfuil an
`T` suite, is _dhá_ luach é `&str`: seoladh an `str` agus a
fhad. Dá bhrí sin, is féidir linn méid luacha `&str` a fháil amach ag am tiomsaithe: tá sé
dhá oiread fad `usize`. Is é sin le rá, bíonn a fhios againn i gcónaí méid `&str`, is cuma cé chomh fada is atá an teaghrán a dtagraíonn sé dó. Go ginearálta, seo an chaoi
a n-úsáidtear cineálacha dinimiciúla i Rust: tá píosa breise
meiteashonraí acu a stórálann méid na faisnéise dinimiciúla. Is é an riail órga maidir le
cineálacha dinimiciúla ná go gcaithfimid luachanna de chineálacha dinimiciúla a chur i gcónaí taobh thiar de phointeoir de chineál éigin.

Is féidir linn `str` a chomhcheangal le gach cineál pointeora: mar shampla, `Box<str>` nó
`Rc<str>`. Go deimhin, chonaic tú é seo cheana ach le cineál dinimiciúil difriúil: traits. Is cineál méide dinimiciúil é gach tréith ar féidir linn tagairt a dhéanamh dó trí
ainm na tréithe a úsáid. I gCaibidil 18 sa chuid [“Úsáid Réada Tréithe a
Ligeann Luachanna de
Chineálacha
Difriúla”][using-trait-objects-that-allow-for-values-of-different-types]<!--
ignore -->, luaigh muid, chun tréithe a úsáid mar réada tréithe, go gcaithfimid
iad a chur taobh thiar de phointeoir, amhail `&dyn Trait` nó `Box<dyn Trait>` (oibreodh `Rc<dyn
Trait>` freisin).

Chun oibriú le DSTanna, soláthraíonn Rust an tréith `Sized` chun a chinneadh an bhfuil méid cineáil ar eolas ag am tiomsaithe nó nach bhfuil. Cuirtear an tréith seo i bhfeidhm go huathoibríoch
do gach rud a bhfuil a mhéid ar eolas ag am tiomsaithe. Ina theannta sin, cuireann Rust
teorainn ar `Sized` go hintuigthe le gach feidhm ghinearálta. Is é sin,
sainmhíniú feidhme ghinearálta mar seo:

```rust,ignore
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-12-generic-fn-definition/src/lib.rs}}
```

déantar é a láimhseáil amhail is dá mba rud é gur scríobhamar é seo:

```rust,ignore
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-13-generic-implicit-sized-bound/src/lib.rs}}
```

De réir réamhshocraithe, ní oibreoidh feidhmeanna cineálacha ach ar chineálacha a bhfuil méid ar eolas acu tráth an tiomsaithe. Mar sin féin, is féidir leat an comhréir speisialta seo a leanas a úsáid chun an srian seo a mhaolú:

```rust,ignore
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-14-generic-maybe-sized/src/lib.rs}}
```

Ciallaíonn tréith atá ceangailte ar `?Sized` go bhféadfadh nó nach bhféadfadh `T` a bheith `Sized` agus go sáraíonn an nótaíocht seo an réamhshocrú go gcaithfidh méid aitheanta a bheith ag cineálacha cineálacha ag
am an tiomsaithe. Níl an comhréir `?Trait` leis an gciall seo ar fáil ach do
`Sized`, ní d'aon tréithe eile.

Tabhair faoi deara freisin gur athraíomar cineál an pharaiméadair `t` ó `T` go `&T`.
Toisc nach bhféadfadh an cineál a bheith `Sized`, ní mór dúinn é a úsáid taobh thiar de chineál éigin pointeora. Sa chás seo, tá tagairt roghnaithe againn.

Ansin, labhróimid faoi fheidhmeanna agus dúnta!

[encapsulation-that-hides-implementation-details]: ch18-01-what-is-oo.html#encapsulation-that-hides-implementation-details
[string-slices]: ch04-03-slices.html#string-slices
[the-match-control-flow-operator]: ch06-02-match.html#the-match-control-flow-operator
[using-trait-objects-that-allow-for-values-of-different-types]: ch18-02-trait-objects.html#using-trait-objects-that-allow-for-values-of-different-types
[using-the-newtype-pattern]: ch20-02-advanced-traits.html#using-the-newtype-pattern-to-implement-external-traits-on-external-types