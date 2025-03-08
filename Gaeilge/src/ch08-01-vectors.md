## Liostaí Luachanna a Stóráil le Veicteoirí

Is é an chéad chineál bailiúcháin a bhreathnóimid air ná `Vec<T>`, ar a dtugtar _veicteoir_ freisin.
Ceadaíonn veicteoirí duit níos mó ná luach amháin a stóráil i struchtúr sonraí amháin a
cuireann sé na luachanna go léir in aice lena chéile i gcuimhne. Ní féidir le veicteoirí ach luachanna a stóráil
den chineál céanna. Tá siad úsáideach nuair a bhíonn liosta míreanna agat, mar shampla an
línte téacs i gcomhad nó praghsanna na n-earraí i tralaí siopadóireachta.

### Veicteoir Nua á Chruthú

Chun veicteoir folamh nua a chruthú, tugaimid an fheidhm `Vec::new`, mar a thaispeántar i
Liostáil 8-1.

<Listing number="8-1" caption="Ag cruthú veicteoir nua, folamh chun luachanna den chineál `i32`"> a choinneáil

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-01/src/main.rs:here}}
```

</Listing>

Tabhair faoi deara gur chuireamar nóta cineáil leis anseo. Toisc nach bhfuil muid ag cur isteach ar bith
luachanna isteach sa veicteoir seo, níl a fhios ag Rust cén cineál eilimintí atá beartaithe againn
stór. Is pointe tábhachtach é seo. Cuirtear veicteoirí i bhfeidhm ag baint úsáide as generics;
clúdóimid conas generics a úsáid le do chineálacha féin i gCaibidil 10. Go dtí seo,
Bíodh a fhios agat gur féidir cineál ar bith a choinneáil sa chineál `Vec<T>` a sholáthraíonn an ghnáthleabharlann.
Nuair a chruthaímid veicteoir chun cineál sonrach a shealbhú, is féidir linn an cineál laistigh a shonrú
lúibíní uillinn. I Liostú 8-1, tá sé ráite againn le Rust go bhfuil an `Vec<T>` in `v`
coinnigh gnéithe den chineál `i32`.

Níos minice, cruthóidh tú `Vec<T>` le luachanna tosaigh agus déanfaidh Rust tátal
an cineál luach is mian leat a stóráil, mar sin is annamh a theastaíonn uait an cineál seo a dhéanamh
nóta. Soláthraíonn Rust an macra `vec!` go caothúil, a chruthóidh a
veicteoir nua a shealbhaíonn na luachanna a thugann tú dó. Cruthaíonn liostú 8-2 ceann nua
`Vec<i32>` a shealbhaíonn na luachanna `1`, `2`, agus `3`. Is é an cineál slánuimhir `i32`
mar sin é an cineál slánuimhir réamhshocraithe, mar a phléamar sa [“Sonraí
Cineálacha”][data-types]<!-- neamhaird a dhéanamh ar --> alt de Chaibidil 3.

<Listing number="8-2" caption="Ag cruthú veicteoir nua ina bhfuil luachanna">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-02/src/main.rs:here}}
```

</Listing>

Toisc go bhfuil luachanna tosaigh `i32` tugtha againn, is féidir le Rust tátal a bhaint as an gcineál `v`
is `Vec<i32>`, agus ní gá an nóta cineáil. Ansin, féachfaimid conas
chun veicteoir a mhodhnú.

### Veicteoir á nuashonrú

Chun veicteoir a chruthú agus ansin eilimintí a chur leis, is féidir linn an modh `push` a úsáid,
mar a thaispeántar i Liosta 8-3.

<Listing number="8-3" caption="Ag baint úsáide as an modh `push` chun luachanna a chur le veicteoir">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-03/src/main.rs:here}}
```

</Listing>

Mar aon le haon athróg, más mian linn a bheith in ann a luach a athrú, ní mór dúinn
é a dhéanamh mutable ag baint úsáide as an eochairfhocal `mut`, mar a pléadh i gCaibidil 3. Na huimhreacha
a chuirimid taobh istigh go bhfuil gach cineál `i32`, agus Rust tátal a bhaint as seo ó na sonraí, mar sin
níl an nóta `Vec<i32>` ag teastáil uainn.

### Léamh Eilimintí Veicteoirí

Tá dhá bhealach ann chun tagairt a dhéanamh do luach atá stóráilte i veicteoir: trí innéacsú nó trí
ag baint úsáide as an modh `get`. Sna samplaí seo a leanas, táimid tar éis anótáil a dhéanamh ar na cineálacha
na luachanna a thugtar ar ais ó na feidhmeanna seo ar mhaithe le soiléireacht bhreise.

Taispeánann liosta 8-4 an dá mhodh chun luach a rochtain i veicteoir, le hinnéacsú
comhréir agus an modh `get`.

<Listing number="8-4" caption="Ag úsáid comhréir innéacsaithe agus ag baint úsáide as an modh `get` chun rochtain a fháil ar mhír i veicteoir">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-04/src/main.rs:here}}
```

</Listing>

Tabhair faoi deara roinnt sonraí anseo. Bainimid úsáid as an luach innéacs de `2` chun an tríú eilimint a fháil
toisc go bhfuil veicteoirí innéacsaithe de réir uimhreacha, ag tosú ag nialas. Ag baint úsáide as `&` agus `[]`
tugann sé tagairt dúinn don eilimint ag an luach innéacs. Nuair a úsáidimid an `get`
modh agus an t-innéacs a rith mar argóint, a fháil againn `Option<&T>` gur féidir linn
úsáid le `match`.

Soláthraíonn Rust an dá bhealach seo chun tagairt a dhéanamh d'eilimint ionas gur féidir leat a roghnú conas a dhéantar an
iompraíonn an clár nuair a dhéanann tú iarracht luach innéacs a úsáid lasmuigh de raon na
eilimintí atá ann cheana féin. Mar shampla, feicimis cad a tharlaíonn nuair a bhíonn veicteoir againn
cúig eilimint agus ansin déanaimid iarracht teacht ar eilimint ag innéacs 100 le gach ceann díobh
teicníc, mar a thaispeántar i Liosta 8-5.

<Listing number="8-5" caption="Ag iarraidh an eilimint ag innéacs 100 a rochtain i veicteoir ina bhfuil cúig eilimint">

```rust,should_panic,panics
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-05/src/main.rs:here}}
```

</Listing>

Nuair a rithfimid an cód seo, beidh an clár i scaoll mar gheall ar an gcéad mhodh `[]`
toisc go ndéanann sé tagairt d'eilimint nach bhfuil ann. Tá an modh seo a úsáidtear is fearr nuair a
ag iarraidh do ríomhchlár tuairteála má tá iarracht rochtain a fháil ar eilimint thar an
deireadh an veicteora.

Nuair a théann an modh `get` thar innéacs atá lasmuigh den veicteoir, filleann sé
`None` gan scaoll. D’úsáidfeá an modh seo má tá rochtain agat ar eilimint
thar raon an veicteora d'fhéadfadh tarlú uaireanta faoin ngnáth
imthosca. Beidh loighic ag do chód ansin chun ceachtar acu a láimhseáil
`Some(&element)` nó `None`, mar a pléadh i gCaibidil 6. Mar shampla, an t-innéacs
d'fhéadfadh a bheith ag teacht ó dhuine ag dul isteach uimhir. Má tá siad isteach de thaisme a
uimhir atá ró-mhór agus faigheann an clár luach `None`, d'fhéadfá a rá leis an
úsáideoir cé mhéad míreanna atá sa veicteoir reatha agus tabhair seans eile dóibh
cuir isteach luach bailí. Bheadh ​​sé sin níos éasca le húsáid ná an clár a thuar
mar gheall ar typo!

Nuair a bhíonn tagairt bhailí ag an gclár, forfheidhmíonn an seiceálaí iasachtaí an
rialacha úinéireachta agus iasachtaíochta (clúdaithe i gCaibidil 4) chun an tagairt seo a áirithiú
agus aon tagairtí eile d'inneachar an veicteora fós bailí. Athghairm an
riail a shonraíonn nach féidir leat tagairtí in-shó-shó-aistrithe a bheith agat sa chéanna
scóip. Tá feidhm ag an riail sin i Liostú 8-6, áit a bhfuil tagairt do-luaineach againn
leis an gcéad eilimint i veicteoir agus déan iarracht eilimint a chur leis an deireadh. seo
Ní oibreoidh an clár má dhéanaimid iarracht tagairt a dhéanamh don eilimint sin níos déanaí sa
feidhm.

<Listing number="8-6" caption="Attempting to add an element to a vector while holding a reference to an item">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-06/src/main.rs:here}}
```

</Listing>

Beidh an earráid seo mar thoradh ar an gcód seo a thiomsú:

```console
{{#include ../../listings/ch08-common-collections/listing-08-06/output.txt}}
```

Seans go n-oibreodh an cód i Liostú 8-6: cén fáth ar cheart tagairt a dhéanamh
don chéad eilimint cúram faoi athruithe ag deireadh an veicteora? Tá an earráid seo
mar gheall ar an gcaoi a n-oibríonn veicteoirí: toisc go gcuireann veicteoirí na luachanna in aice lena chéile
mar chuimhne, d'fhéadfadh go mbeadh gá le heilimint nua a chur le deireadh an veicteora
cuimhne nua a leithdháileadh agus na gnéithe d'aois a chóipeáil chuig an spás nua, más ann
níl dóthain spáis ann chun na heilimintí go léir a chur in aice lena chéile san áit a bhfuil an veicteoir
atá stóráilte faoi láthair. Sa chás sin, bheadh ​​an tagairt don chéad eilimint
ag tagairt do chuimhne dealraithe. Cuireann na rialacha iasachtaíochta cosc ​​ar chláir ó
ag críochnú sa chás sin.

> Nóta: Le haghaidh tuilleadh eolais ar shonraí cur chun feidhme an chineáil `Vec<T>`, féach [“The
> Rustonomicon”][nomicon].

### Ag Atriall Thar na Luachanna i Veicteoir

Chun rochtain a fháil ar gach eilimint i veicteoir ar a seal, dhéanfaimis athrá trí gach ceann de na
eilimintí seachas innéacsanna a úsáid chun rochtain a fháil ar cheann amháin ag an am. Léiríonn liostú 8-7 conas
lúb `for` a úsáid chun tagairtí do-athlasta a fháil do gach eilimint i veicteoir de
luachanna `i32` agus priontáil iad.

<Listing number="8-7" caption="Gach eilimint a phriontáil i veicteoir trí na heilimintí a atriall ag baint úsáide as lúb `for`">

``` meirge
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-07/src/main.rs:here}}
```

</Listing>

Is féidir linn athrá a dhéanamh freisin ar thagairtí mutable do gach eilimint i veicteoir mutable
chun athruithe a dhéanamh ar na heilimintí go léir. An lúb `for` i Liostú 8-8
cuirfidh sé `50` le gach eilimint.

<Listing number="8-8" caption="Iterating over mutable references to elements in a vector">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-08/src/main.rs:here}}
```

</Listing>

Chun an luach a thagraíonn an tagairt mutable a athrú, ní mór dúinn úsáid a bhaint as an
`*` oibreoir díreference chun an luach in `i` a bhaint amach sular féidir linn an `+=` a úsáid
oibreoir. Labhróimid níos mó faoin oibreoir díreagartha san [“Tar éis an
Pointeoir don Luach leis an Oibritheoir Dereference”][deref]<!-- neamhaird -->
alt de Chaibidil 15 .

Tá sé sábháilte atriallta thar veicteoir, bíodh sé neamh-inchurtha nó comh-athsholáthair, mar gheall ar an
rialacha seiceálaithe iasachtaí. Má rinneamar iarracht míreanna a chur isteach nó a bhaint sa `for`
comhlachtaí lúb i Liostú 8-7 agus Liostú 8-8, gheobhaimid earráid tiomsaithe
cosúil leis an gceann a fuair muid leis an gcód i Liosta 8-6. An tagairt do na
veicteoir a choinníonn an lúb `for` cosc ​​ar mhodhnú comhuaineach ar an
veicteoir iomlán.

### Enum a úsáid chun Ilchineálacha a Stóráil

Ní féidir le veicteoirí ach luachanna den chineál céanna a stóráil. Is féidir é seo a
deacair ; tá cásanna úsáide cinnte le haghaidh gá a stóráil liosta de
míreanna de chineálacha éagsúla. Ar ámharaí an tsaoil, sainmhínítear na leaganacha de enum
faoin gcineál enum céanna, mar sin nuair a theastaíonn cineál amháin uainn chun gnéithe de
cineálacha éagsúla, is féidir linn enum a shainiú agus a úsáid!

Mar shampla, abair go dteastaíonn uainn luachanna a fháil as a chéile i scarbhileog ina bhfuil
tá slánuimhreacha i gcuid de na colúin sa ró, roinnt uimhreacha snámhphointe,
agus roinnt teaghráin. Is féidir linn enum a shainiú a mbeidh na leaganacha éagsúla acu
cineálacha luacha, agus measfar an cineál céanna a bheith ar na leaganacha uile enum: sin
den enum. Ansin is féidir linn veicteoir a chruthú chun an enum sin a shealbhú agus mar sin, ar deireadh thiar,
shealbhú cineálacha éagsúla. Tá sé seo léirithe againn i Liostú 8-9.

<Listing number="8-9" caption="Defining an `enum` to store values of different types in one vector">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-09/src/main.rs:here}}
```

</Listing>

Caithfidh Rust a fhios cad iad na cineálacha a bheidh sa veicteoir ag am tiomsaithe ionas go mbeidh a fhios aige
go díreach cé mhéad cuimhne ar an gcarn a bheidh ag teastáil chun gach eilimint a stóráil. muid
Ní mór a bheith soiléir freisin faoi na cineálacha a cheadaítear sa veicteoir seo. Má meirge
ceadaítear veicteoir a shealbhú de chineál ar bith, bheadh ​​seans ann go mbeadh ceann amháin nó níos mó de
dhéanfadh na cineálacha earráidí leis na hoibríochtaí a dhéantar ar ghnéithe de
an veicteoir. Ag baint úsáide as enum móide slonn `match` ciallaíonn sé sin go gcinnteoidh Rust
ag an am tiomsaithe a láimhseáiltear gach cás féideartha, mar a pléadh i gCaibidil 6.

Mura bhfuil a fhios agat an tsraith uileghabhálach cineálacha a gheobhaidh clár ag am rite
stóráil i veicteoir, ní oibreoidh an teicníc enum. Ina áit sin, is féidir leat úsáid a bhaint as trait
réad, a chlúdóimid i gCaibidil 18.

Anois go bhfuil roinnt de na bealaí is coitianta chun veicteoirí a úsáid pléite againn, bí cinnte
athbhreithniú a dhéanamh ar [an doiciméadú API][vec-api]<!-- neamhaird --> do gach ceann de na go leor
modhanna úsáideacha arna sainiú ar `Vec<T>` ag an leabharlann chaighdeánach. Mar shampla, i
Chomh maith le `push`, baintear agus cuireann modh `pop` an eilimint dheireanach ar ais.

### Má thiteann Veicteoir Titeann a Eilimintí

Cosúil le haon `struct` eile, saortar veicteoir nuair a théann sé as raon feidhme, mar
atá anótáilte i Liostú 8-10.

<Listing number="8-10" caption="Showing where the vector and its elements are dropped">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-10/src/main.rs:here}}
```

</Listing>

Nuair a thiteann an veicteoir, scaoiltear a bhfuil ann go léir freisin, rud a chiallaíonn an
déanfar slánuimhreacha atá aige a ghlanadh suas. Cinntíonn an seiceálaí iasachtaí go bhfuil aon
ní úsáidtear tagairtí d'inneachar veicteora ach amháin nuair a bhíonn an veicteoir féin
bailí.

Bogfaimid ar aghaidh go dtí an chéad chineál bailiúcháin eile: `String`!

[data-types]: ch03-02-data-types.html#data-types
[nomicon]: ../nomicon/vec/vec.html
[vec-api]: ../std/vec/struct.Vec.html
[deref]: ch15-02-deref.html#following-the-pointer-to-the-value-with-the-dereference-operator