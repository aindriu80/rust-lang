## Ár dTionscadal I/O a Fheabhsú

Leis an eolas nua seo faoi iterators, is féidir linn feabhas a chur ar an tionscadal I/O i
Caibidil 12 trí úsáid a bhaint as iterators chun áiteanna sa chód a dhéanamh níos soiléire agus níos mó
gonta. Breathnaímid ar conas is féidir le hathraitheoirí ár gcur i bhfeidhm ar an
Feidhm `Config::build` agus an fheidhm `search`.

### Ag baint `clone` ag Úsáid Iterator

I Liostú 12-6, chuireamar cód leis a ghlac slice de luachanna `String` agus a chruthaigh
sampla den struchtúr `Config` trí innéacsú isteach sa slice agus clónáil an
luachanna, ag ligean don struchtúr `Config` úinéireacht a bheith aige ar na luachanna sin. I Liostú 13-17,
táimid tar éis feidhmiú na feidhme `Config::build` a chur i bhfeidhm mar a bhí
i Liosta 12-23:

<Listing number="13-17" file-name="src/lib.rs" caption="Reproduction of the `Config::build` function from Listing 12-23">

```rust,ignore
{{#rustdoc_include ../../listings/ch13-functional-features/listing-12-23-reproduced/src/lib.rs:ch13}}
```

</Listing>

Ag an am, dúirt muid gan a bheith buartha faoi na glaonna `clone` mí-éifeachtach mar gheall ar
chuirfimis deireadh leo amach anseo. Bhuel, tá an t-am sin anois!

Bhí `clone` ag teastáil uainn anseo mar tá slisne againn le heilimintí `String` sa
paraiméadar `args`, ach ní le `args` an fheidhm `args`. Chun filleadh
úinéireacht ar shampla `Config`, bhí orainn na luachanna a chlónáil ón `query`
agus réimsí `file_path` de `Config` ionas gur féidir leis an ásc `Config` a luachanna a bheith agat.

Leis an eolas nua atá againn faoi iterators, is féidir linn an fheidhm `args` a athrú go
úinéireacht a ghlacadh ar iterator mar a argóint in ionad a fháil ar iasacht slice.
Úsáidfimid feidhmiúlacht atrialach in ionad an chóid a sheiceálann an fad
an tslis agus na hinnéacsanna go láithreacha ar leith. Beidh sé seo soiléiriú cad é an
Tá feidhm `Config::build` ag déanamh mar go mbeidh rochtain ag an atrialach ar na luachanna.

Nuair a ghlacann `Config::build`' úinéireacht ar an atriallta agus stopann sé ag úsáid innéacsú
oibríochtaí a fhaigheann iasachtaí, is féidir linn na luachanna `String` a bhogadh ón atrialltóir isteach
`Config` seachas `clone` a ghlaoch agus leithdháileadh nua a dhéanamh.

#### Ag baint úsáide as an Iterator Filleadh go Díreach

Oscail comhad _src/main.rs_ do thionscadal I/O, ba cheart go mbeadh cuma mar seo air:

<span class="filename">Filename: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch13-functional-features/listing-12-24-reproduced/src/main.rs:ch13}}
```

Athróimid ar dtús tús na `main` a bhí againn i Liostú
12-24 leis an gcód i Liostú 13-18, a úsáideann atrialltóir an uair seo. seo
ní thiomsófar go dtí go ndéanaimid `Config::build` a nuashonrú freisin.

<Listing number="13-18" file-name="src/main.rs" caption="Passing the return value of `env::args` to `Config::build`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-18/src/main.rs:here}}
```

</Listing>

Tugann an fheidhm `env::args` iterator ar ais! Seachas a bheith ag bailiú na
luachanna iterator isteach i veicteoir agus ansin sliocht a chur chuig `Config::build`, anois
táimid ag dul faoi úinéireacht an iterator a tugadh ar ais ó `env::args` go
`Config::build` go díreach.

Ansin, ní mór dúinn an sainmhíniú ar `Config::build` a nuashonrú. I do I/O
comhad _src/lib.rs_ an tionscadail, déanaimis síniú `Config::build` a athrú go
cuma Liostáil 13-19. Ní thiomsóidh sé seo go fóill toisc go gcaithfimid nuashonrú a dhéanamh ar an
comhlacht feidhm.

<Listing number="13-19" file-name="src/lib.rs" caption="Updating the signature of `Config::build` to expect an iterator">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-19/src/lib.rs:here}}
```

</Listing>

Léiríonn doiciméadú caighdeánach na leabharlainne don fheidhm `env::args` go bhfuil an
cineál an iterator a fhilleann sé ná `std::env::Args`, agus cuireann an cineál sin i bhfeidhm
an trait `Iterator` agus cuireann sé luachanna `String` ar ais.

Tá síniú na feidhme `Config::build` nuashonraithe againn mar sin an paraiméadar
tá cineál cineálach ag `args` agus na teorainneacha trait `impl Iterator<Item = String>`
in ionad `&[String]`. Úsáideadh an chomhréir `impl Trait` seo a phléamar
an [“Tréithe mar Pharaiméadar”][impl-trait]<!-- neamhaird --> de Chaibidil 10
ciallaíonn sé gur féidir le `args` a bheith ina chineál ar bith a chuireann an trait `Iterator` i bhfeidhm agus
seolann míreanna `String` ar ais.

Toisc go bhfuil muid ag glacadh úinéireachta ar `args` agus beidh muid ag mutating `args` faoi
ag athrá thairis air, is féidir linn an eochairfhocal `mut` a chur isteach i sonraíocht an
paraiméadar `args` chun é a dhéanamh mutable.

#### Ag Úsáid Modhanna Trait `Iterator` In ionad Innéacsú

Ansin, socróimid corp `Config::build`. Toisc go gcuireann `args` an
Tréith `Iterator`, tá a fhios againn gur féidir linn an modh `next` a ghlaoch air! Liostáil 13-20
nuashonraíonn sé an cód ó Liostú 12-23 chun an modh `next` a úsáid:

<Listing number="13-20" file-name="src/lib.rs" caption="Changing the body of `Config::build` to use iterator methods">

```rust,noplayground
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-20/src/lib.rs:here}}
```

</Listing>

Cuimhnigh gurb é an chéad luach i luach aischuir `env::args` ainm
an clár. Ba mhaith linn neamhaird a dhéanamh air sin agus an chéad luach eile a bhaint amach, mar sin glaoimid ar dtús
`next` agus ná déan faic leis an luach tuairisceáin. Sa dara háit, tugaimid `next` chun an
luach ba mhaith linn a chur sa réimse `query` de `Config`. Má fhilleann `next` a
`Some`, úsáidimid `match` chun an luach a bhaint amach. Má fhilleann sé `None`, ciallaíonn sé
níor tugadh go leor argóintí agus filleann muid go luath le luach `Err`. Déanaimid
an rud céanna don luach `file_path`.

### Cód a Dhéanamh níos soiléire le Cuibheoirí Iterator

Is féidir linn leas a bhaint as iterators san fheidhm `search` inár I/O
tionscadal, a atáirgeadh anseo i Liostú 13-21 mar a bhí i Liostú 12-19:

<Listing number="13-21" file-name="src/lib.rs" caption="The implementation of the `search` function from Listing 12-19">

```rust,ignore
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-19/src/lib.rs:ch13}}
```

</Listing>

Is féidir linn an cód seo a scríobh ar bhealach níos gonta ag baint úsáide as modhanna oiriúntóra iterator.
Má dhéantar é sin, is féidir linn veicteoir `results` idirmheánacha mutable a sheachaint. Tá an
is fearr le stíl ríomhchláraithe feidhmiúil an méid stát mutable a íoslaghdú
cód a dhéanamh níos soiléire. D'fhéadfaí feabhsú sa todhchaí a chumasú dá mbainfí an stát mutable
chun cuardach a dhéanamh ag an am céanna, mar ní bheadh ​​orainn a bhainistiú
rochtain chomhthráthach ar an veicteoir `results`. Léiríonn liostú 13-22 an t-athrú seo:

<Listing number="13-22" file-name="src/lib.rs" caption="Using iterator adapter methods in the implementation of the `search` function">

```rust,ignore
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-22/src/lib.rs:here}}
```

</Listing>

Thabhairt chun cuimhne gurb é cuspóir na feidhme `search` gach líne a chur ar ais isteach
`contents` ina bhfuil an `query`. Cosúil leis an sampla `filter` i Liostú
13-16, úsáideann an cód seo an `filter` cuibheoir a choinneáil ach amháin na línte go
`line.contains(query)` filleann `true` le haghaidh. Bailímid na línte meaitseála ansin
isteach i veicteoir eile le `collect`. I bhfad níos simplí! Thig leat a dhéanamh mar an gcéanna
athrú chun modhanna atrialach a úsáid san fheidhm `search_case_insensitive` mar
go maith.

### Ag Roghnú Idir Lúb nó Iterators

Is í an chéad cheist loighciúil eile ná cén stíl ar cheart duit a roghnú i do chód féin agus
cén fáth: an cur i bhfeidhm bunaidh i Liostú 13-21 nó an leagan a úsáideann
iterators i Liosta 13-22. Is fearr leis an gcuid is mó de ríomhchláraitheoirí Rust an t-iterator a úsáid
stíl. Tá sé beagán níos deacra a fháil ar an hang of ar dtús, ach nuair a bhraitheann tú
maidir leis na hoiriúnóirí iterator éagsúla agus cad a dhéanann siad, is féidir iterators a bheith níos éasca a
thuiscint. In ionad fiddling leis na píosaí éagsúla lúbadh agus tógáil
veicteoirí nua, díríonn an cód ar chuspóir ardleibhéil an lúb. seo
achoimríonn cuid den chód coitianta ionas gur fusa na coincheapa a fheiceáil
atá uathúil don chód seo, mar an riocht scagtha i ngach eilimint
ní mór don iterator pas a fháil.

Ach an ionann an dá fheidhmiú i ndáiríre? An toimhde iomasach
b'fhéidir go mbeidh an lúb níos ísle níos tapúla. Labhraimís faoi
feidhmíochta.

[impl-trait]: ch10-02-traits.html#traits-as-parameters