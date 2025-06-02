## Meirg Neamhshábháilte

Tá ráthaíochtaí sábháilteachta cuimhne Rust curtha i bhfeidhm ag am an tiomsaithe i ngach cód a phléamar go dtí seo. Mar sin féin, tá teanga eile i bhfolach i Rust
nach gcuireann na ráthaíochtaí sábháilteachta cuimhne seo i bhfeidhm: tugtar _unsafe Rust_ air
agus oibríonn sé díreach cosúil le Rust rialta, ach tugann sé sárchumhachtaí breise dúinn.

Tá Meirg Neamhshábháilte ann toisc, de réir nádúir, go bhfuil anailís statach coimeádach. Nuair
a dhéanann an tiomsaitheoir iarracht a chinneadh an gcomhlíonann an cód na ráthaíochtaí nó nach gcomhlíonann,
is fearr dó roinnt clár bailí a dhiúltú ná roinnt clár neamhbhailí a ghlacadh.

Cé go bhféadfadh an cód a bheith ceart go leor, mura bhfuil
dóthain faisnéise ag tiomsaitheoir Rust le bheith muiníneach, diúltóidh sé don chód. Sna cásanna seo,
is féidir leat cód neamhshábháilte a úsáid chun a rá leis an tiomsaitheoir, "Creid dom, tá a fhios agam cad atá á dhéanamh agam." Bí cúramach, áfach, go n-úsáideann tú Rust neamhshábháilte ar do phriacal féin: má
úsáideann tú cód neamhshábháilte go mícheart, is féidir fadhbanna a bheith ann mar gheall ar neamhshábháilteacht cuimhne, amhail
dí-thagairt pointeora nialasach.

Cúis eile a bhfuil alter ego neamhshábháilte ag Rust ná go bhfuil an crua-earraí ríomhaireachta bunúsach neamhshábháilte ó dhúchas. Mura lig Rust duit oibríochtaí neamhshábháilte a dhéanamh, ní fhéadfá tascanna áirithe a dhéanamh. Caithfidh Rust ligean duit cláir chórais ísealleibhéil a dhéanamh, amhail idirghníomhú go díreach leis an gcóras oibriúcháin nó fiú do chóras oibriúcháin féin a scríobh. Tá obair le cláir chórais ísealleibhéil ar cheann de spriocanna na teanga. Déanaimis iniúchadh ar a bhféadfaimid a dhéanamh le Rust neamhshábháilte agus conas é a dhéanamh.

### Sárchumhachtaí Neamhshábháilte

Chun aistriú go Rust neamhshábháilte, bain úsáid as an eochairfhocal `unsafe` agus ansin tosaigh bloc nua ina bhfuil an cód neamhshábháilte. Is féidir leat cúig ghníomh a dhéanamh i Rust neamhshábháilte nach féidir leat a dhéanamh i Rust sábháilte, ar a dtugaimid _sárchumhachtaí neamhshábháilte_. I measc na sárchumhachtaí sin
tá an cumas chun:

- Díthagairt a dhéanamh ar phointeoir amh
- Feidhm nó modh neamhshábháilte a ghlaoch
- Athróg statach inathraithe a rochtain nó a mhodhnú
- Tréith neamhshábháilte a chur i bhfeidhm
- Rochtain a fháil ar réimsí `union`

Tá sé tábhachtach a thuiscint nach múchann `unsafe` an seiceálaí iasachta
ná nach ndíchumasaíonn sé aon cheann eile de sheiceálacha sábháilteachta Rust: má úsáideann tú tagairt i gcód neamhshábháilte,
déanfar seiceáil air fós. Ní thugann an eochairfhocal `unsafe` ach rochtain duit ar
na cúig ghné seo nach ndéanann an tiomsaitheoir seiceáil orthu ansin le haghaidh sábháilteachta
cuimhne. Gheobhaidh tú leibhéal áirithe sábháilteachta fós taobh istigh de bhloc neamhshábháilte.

Ina theannta sin, ní chiallaíonn `unsafe` go bhfuil an cód taobh istigh den bhloc contúirteach go riachtanach
nó go mbeidh fadhbanna sábháilteachta cuimhne aige cinnte: is é an cuspóir
go gcinnteoidh tú, mar chláraitheoir, go ndéanfaidh an cód taobh istigh de bhloc `unsafe`
rochtain ar chuimhne ar bhealach bailí.

Bíonn daoine earráideach, agus tarlóidh botúin, ach trí cheangal a chur ar na cúig oibríocht neamhshábháilte seo a bheith laistigh de bhloic a bhfuil nótaí orthu le `unsafe` beidh a fhios agat go gcaithfidh aon earráidí a bhaineann le sábháilteacht cuimhne a bheith laistigh de bhloc `unsafe`. Coinnigh
bloic `unsafe` beag; beidh tú buíoch níos déanaí nuair a dhéanfaidh tú imscrúdú ar fhabhtanna cuimhne.

Chun cód neamhshábháilte a leithlisiú a oiread agus is féidir, is fearr cód neamhshábháilte a iamh
laistigh d'eastarraingt shábháilte agus API sábháilte a sholáthar, a phléifimid níos déanaí sa
chaibidil nuair a scrúdóimid feidhmeanna agus modhanna neamhshábháilte. Cuirtear codanna den
leabharlann chaighdeánach i bhfeidhm mar eastarraingtí sábháilte thar chód neamhshábháilte atá
iniúchta. Cuireann timfhilleadh cód neamhshábháilte in eastarraingt shábháilte cosc ​​ar úsáidí `unsafe`
ó sceitheadh ​​​​​​amach sna háiteanna go léir a bhféadfadh tú féin nó d'úsáideoirí a bheith ag iarraidh an fheidhmiúlacht a cuireadh i bhfeidhm le cód `unsafe` a úsáid, toisc go bhfuil úsáid eastarraingthe sábháilte sábháilte.

Féachfaimid ar gach ceann de na cúig chumhacht mhór neamhshábháilte ina dhiaidh sin. Féachfaimid freisin ar
roinnt teibí a sholáthraíonn comhéadan sábháilte do chód neamhshábháilte.

### Díthagairt Pointeoir Amh

I gCaibidil 4, sa chuid [“Crochta agus Tagairtí”][dangling-references]<!-- ignore
-->, luaigh muid go gcinntíonn an tiomsaitheoir go bhfuil tagairtí i gcónaí
bailí. Tá dhá chineál nua ag Unsafe Rust ar a dtugtar _pointéirí_ atá cosúil le
tagairtí. Mar atá le tagairtí, is féidir le pointeoirí amha a bheith dochloíte nó inathraithe agus
scríobhtar iad mar `*const T` agus `*mut T`, faoi seach. Ní hé an réalta an
oibreoir díthagairt; is cuid den ainm cineáil é. I gcomhthéacs pointeoirí
amha, ciallaíonn _immutable_ nach féidir an pointeoir a shannadh go díreach
tar éis é a dhíthagairt.

Difriúil ó thagairtí agus pointeoirí cliste, pointeoirí amha:

- Ceadaítear dóibh neamhaird a dhéanamh de na rialacha iasachta trí phointeoirí dochloíte agus inathraithe araon a bheith acu
nó ilphointeoirí inathraithe chuig an suíomh céanna
- Ní ráthaítear go bpointeoidh siad chuig cuimhne bhailí
- Ceadaítear dóibh a bheith nialasach
- Ní chuireann siad aon ghlanadh uathoibríoch i bhfeidhm

Trí rogha a dhéanamh gan na ráthaíochtaí seo a fhorfheidhmiú ag Rust, is féidir leat sábháilteacht ráthaithe a thabhairt suas ar mhaithe le feidhmíocht níos fearr nó an cumas
comhéadan a dhéanamh le teanga nó crua-earraí eile nach bhfuil feidhm ag ráthaíochtaí Rust.

Léiríonn Liostáil 20-1 conas pointeoir amh dochloíte agus inathraithe a chruthú.

<Listing number="20-1" caption="Creating raw pointers with the raw borrow operators">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-01/src/main.rs:here}}
```

</Listing>

Tabhair faoi deara nach gcuirimid an eochairfhocal `unsafe` san áireamh sa chód seo. Is féidir linn pointeoirí amha a chruthú i gcód sábháilte; ní féidir linn pointeoirí amha a dhíthagairt lasmuigh de bhloc
unsafe, mar a fheicfidh tú i gceann tamaill.

Chruthaíomar pointeoirí amha trí úsáid a bhaint as na hoibreoirí iasachta amha: cruthaíonn `&raw const num` pointeoir amh dochloíte `*const i32`, agus cruthaíonn `&raw mut num` pointeoir amh inathraithe `*mut
i32`. Toisc gur chruthaíomar iad go díreach ó athróg
áitiúil, tá a fhios againn go bhfuil na pointeoirí amha seo bailí, ach ní féidir linn an toimhde sin a dhéanamh faoi aon phointeoir amh.

Chun seo a léiriú, ansin cruthóimid pointeoir amh nach féidir linn a bheith
cinnte faoi a bhailíocht, ag baint úsáide as `as` chun luach a chaitheamh in ionad na n-oibreoirí
tagartha amha a úsáid. Taispeánann Liostáil 20-2 conas pointeoir amh a chruthú chuig suíomh treallach
sa chuimhne. Níl aon sainmhíniú ar úsáid chuimhne treallach: d'fhéadfadh sonraí a bheith ag an seoladh sin nó nach mbeadh, d'fhéadfadh an tiomsaitheoir an cód a bharrfheabhsú ionas nach mbeadh rochtain chuimhne ann, nó d'fhéadfadh earráid deighilte a bheith sa chlár.
De ghnáth, ní bhíonn aon chúis mhaith ann cód mar seo a scríobh, go háirithe i gcásanna
inar féidir leat oibreoir iasachta amh a úsáid ina ionad, ach is féidir é.

<Listing number="20-2" caption="Creating a raw pointer to an arbitrary memory address">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-02/src/main.rs:here}}
```

</Listing>

Cuimhnigh gur féidir linn pointeoirí amha a chruthú i gcód sábháilte, ach ní féidir linn pointeoirí amha a _díthreorú_ agus na sonraí atá á dtagairt a léamh. I Liosta 20-3, úsáidimid an t-oibreoir
díthreorú `*` ar phointeoir amh a éilíonn bloc `unsafe`.

<Listing number="20-3" caption="Dereferencing raw pointers within an `unsafe` block">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-03/src/main.rs:here}}
```

</Listing>

Ní dhéanann cruthú pointeora aon dochar; ní féidir linn déileáil le luach neamhbhailí ach amháin nuair a dhéanaimid iarracht rochtain a fháil ar an luach a bhfuil sé ag pointeáil air.

Tabhair faoi deara freisin gur chruthaíomar i Liosta 20-1 agus 20-3 pointeoirí amha `*const i32` agus `*mut i32` a bhí ag pointeáil chuig an suíomh cuimhne céanna, áit a bhfuil `num`
stóráilte. Dá ndéanfaimis iarracht tagairt neamh-inathraithe agus tagairt inathraithe a chruthú chuig
`num`, ní bheadh ​​an cód tiomsaithe mar ní cheadaíonn rialacha úinéireachta Rust
tagairt inathraithe ag an am céanna le haon tagairtí neamh-inathraithe. Le
pointeoirí amha, is féidir linn pointeoir inathraithe agus pointeoir neamh-inathraithe a chruthú chuig an
suíomh céanna agus sonraí a athrú tríd an bpointeoir inathraithe, rud a d'fhéadfadh
rás sonraí a chruthú. Bí cúramach!

Leis na contúirtí seo go léir, cén fáth a n-úsáidfeá pointeoirí amha riamh? Cás úsáide mór amháin is ea nuair a bhíonn comhéadan á dhéanamh le cód C, mar a fheicfidh tú sa chéad chuid eile,
[“Glaoch ar Fheidhm nó
Modh Neamhshábháilte.”](#glaoch-ar-fheidhm-nó-modh-neamhshábháilte)<!-- neamhaird a dhéanamh --> Cás eile is ea
nuair a bhíonn teibí sábháilte á dtógáil nach dtuigeann an seiceálaí iasachta.

Tabharfaimid isteach feidhmeanna neamhshábháilte agus ansin féachfaimid ar shampla d’eibí sábháilte a úsáideann cód neamhshábháilte.

### Glaoch ar Fheidhm nó Modh Neamhshábháilte

Is é an dara cineál oibríochta is féidir leat a dhéanamh i mbloc neamhshábháilte ná glaoch ar
fheidhmeanna neamhshábháilte. Breathnaíonn feidhmeanna agus modhanna neamhshábháilte díreach cosúil le feidhmeanna agus modhanna rialta,
ach tá `unsafe` breise acu roimh an gcuid eile den
sainmhíniú. Léiríonn an eochairfhocal `unsafe` sa chomhthéacs seo go bhfuil
riachtanais ag an bhfeidhm a chaithfimid a chomhlíonadh nuair a ghlaoimid ar an bhfeidhm seo, mar ní féidir le Rust
a ráthú go bhfuil na ceanglais seo comhlíonta againn. Trí fheidhm neamhshábháilte a ghlaoch laistigh de bhloc `unsafe`, táimid ag rá gur léigh muid doiciméadacht na feidhme seo agus go nglacaimid freagracht as conarthaí na feidhme a choinneáil.

Seo feidhm neamhshábháilte darb ainm `dangerous` nach ndéanann aon rud ina corp:

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-01-unsafe-fn/src/main.rs:here}}
```

Ní mór dúinn glaoch ar an bhfeidhm `dangerous` laistigh de bhloc `unsafe` ar leithligh. Má dhéanaimid iarracht glaoch ar `dangerous` gan an bloc `unsafe`, gheobhaidh muid earráid:

```console
{{#include ../../listings/ch20-advanced-features/output-only-01-missing-unsafe/output.txt}}
```

Leis an mbloc `unsafe`, táimid ag dearbhú do Rust gur léigh muid doiciméadacht na feidhme, go dtuigeann muid conas í a úsáid i gceart, agus gur fhíoraigh muid go bhfuilimid ag comhlíonadh chonradh na feidhme.

Chun oibríochtaí neamhshábháilte a dhéanamh i gcorp feidhme neamhshábháilte, ní mór duit fós
bloc `unsafe` a úsáid díreach mar atá laistigh de ghnáthfheidhm, agus tabharfaidh an tiomsaitheoir
rabhadh duit má dhéanann tú dearmad. Cuidíonn sé seo le bloic `unsafe` a choinneáil chomh beag agus
is féidir, toisc nach mbeadh gá le hoibríochtaí neamhshábháilte ar fud
chorp iomlán na feidhme.

#### Aistarraingt Shábháilte a Chruthú thar Chód Neamhshábháilte

Ní chiallaíonn sé go gcaithfimid an
fheidhm iomlán a mharcáil mar neamhshábháilte díreach toisc go bhfuil cód neamhshábháilte i bhfeidhm. Déanta na fírinne, is
aistarraingt choitianta é cód neamhshábháilte a fhilleadh i bhfeidhm shábháilte. Mar shampla, déanaimis staidéar a dhéanamh ar an bhfeidhm `split_at_mut`
ón leabharlann chaighdeánach, a éilíonn roinnt cód neamhshábháilte. Déanfaimid iniúchadh ar conas
a d'fhéadfaimis í a chur i bhfeidhm. Sainmhínítear an modh sábháilte seo ar shlisní inathraithe: tógann sé slisne amháin agus déanann sé dhá cheann de tríd an slisne a scoilt ag an innéacs a thugtar mar argóint. Taispeánann liostú 20-4 conas `split_at_mut` a úsáid.

<Listing number="20-4" caption="Using the safe `split_at_mut` function">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-04/src/main.rs:here}}
```

</Listing>

Ní féidir linn an fheidhm seo a chur i bhfeidhm ag baint úsáide as Rust sábháilte amháin. D’fhéadfadh iarracht breathnú cosúil le Liosta 20-5, nach ndéanfaidh tiomsú. Ar mhaithe le simplíocht, cuirfimid `split_at_mut` i bhfeidhm mar fheidhm seachas mar mhodh agus le haghaidh slisní de luachanna `i32` seachas le haghaidh cineál cineálach `T`.

<Listing number="20-5" caption="An attempted implementation of `split_at_mut` using only safe Rust">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-05/src/main.rs:here}}
```

</Listing>

Faigheann an fheidhm seo fad iomlán an tslisne ar dtús. Ansin dearbhaíonn sí go bhfuil
an t-innéacs a thugtar mar pharaiméadar laistigh den tslisne trí sheiceáil an bhfuil sé
níos lú ná nó cothrom leis an fhad. Ciallaíonn an dearbhú má ritheann muid innéacs
atá níos mó ná an fad chun an tslisne a roinnt ag, go mbeidh scaoll ar an bhfeidhm
sula ndéanann sí iarracht an t-innéacs sin a úsáid.

Ansin, cuirimid dhá shlisne inathraithe ar ais i dtupla: ceann ó thús an
tslisne bhunaidh go dtí an t-innéacs `mid` agus ceann eile ó `mid` go dtí deireadh an
tslisne.

Nuair a dhéanaimid iarracht an cód i Liosta 20-5 a thiomsú, gheobhaidh muid earráid.

```console
{{#include ../../listings/ch20-advanced-features/listing-20-05/output.txt}}
```

Ní thuigfidh seiceálaí iasachta Rust go bhfuil codanna difriúla den slisne á n-iasacht againn; níl a fhios aige ach go bhfuilimid ag iasacht ón slisne céanna faoi dhó.
Tá sé ceart go bunúsach codanna difriúla de shlisne a fháil ar iasacht toisc nach bhfuil an dá
shlisne ag forluí, ach níl Rust cliste go leor chun é seo a fhios. Nuair a
bheimid
cinnte go bhfuil an cód ceart go leor, ach nach bhfuil Rust, tá sé in am dul i muinín cód neamhshábháilte.

Léiríonn liostú 20-6 conas bloc `unsafe`, pointeoir amh, agus roinnt glaonna
chuig feidhmeanna neamhshábháilte a úsáid chun cur i bhfeidhm `split_at_mut` a chur ag obair.


<Listing number="20-6" caption="Using unsafe code in the implementation of the `split_at_mut` function">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-06/src/main.rs:here}}
```

</Listing>

Meabhraigh ón alt [“The Slice Type”][the-slice-type]<!-- ignore --> i
Caibidil 4 go bhfuil slisní ina dtuairimeoir chuig sonraí áirithe agus fad na slisne.
Úsáidimid an modh `len` chun fad slisne a fháil agus an modh `as_mut_ptr`
chun rochtain a fháil ar an dtuairimeoir amh de shlisne. Sa chás seo, toisc go bhfuil slisne inathraithe againn go luachanna `i32`, tugann `as_mut_ptr` pointeoir amh ar ais leis an gcineál
`*mut i32`, atá stóráilte againn san athróg `ptr`.

Coinnímid an dearbhú go bhfuil an t-innéacs `mid` laistigh den slisne. Ansin tagaimid chuig
an cód neamhshábháilte: glacann an fheidhm `slice::from_raw_parts_mut` pointeoir amh
agus fad, agus cruthaíonn sí slisne. Úsáidimid an fheidhm seo chun slisne a chruthú
a thosaíonn ó `ptr` agus atá ina míreanna `mid` ar fhad. Ansin glaoimid ar an modh `add` ar `ptr` le `mid` mar argóint chun pointeoir amh a fháil a thosaíonn ag
`mid`, agus cruthaímid slisne ag baint úsáide as an pointeoir sin agus an líon atá fágtha de
mhíreanna i ndiaidh `mid` mar an fad.

Tá an fheidhm `slice::from_raw_parts_mut` neamhshábháilte mar go nglacann sí pointeoir amh agus ní mór di muinín a bheith aici go bhfuil an pointeoir seo bailí. Tá an modh `add` ar phointeoirí amha
neamhshábháilte freisin, mar ní mór di muinín a bheith aici go bhfuil an suíomh fritháireamh ina phointeoir bailí freisin. Dá bhrí sin, b'éigean dúinn bloc `unsafe` a chur timpeall ar ár nglaonna chuig
`slice::from_raw_parts_mut` agus `add` ionas go bhféadfaimis glaoch orthu. Trí fhéachaint ar
an gcód agus tríd an dearbhú a chur leis go gcaithfidh `mid` a bheith níos lú ná nó cothrom le
`len`, is féidir linn a rá go mbeidh na pointeoirí amha go léir a úsáidtear laistigh den bhloc `unsafe`
ina dtuairimí bailí chuig sonraí laistigh den slisne. Is úsáid inghlactha agus
iomchuí de `unsafe` é seo.

Tabhair faoi deara nach gá dúinn an fheidhm `split_at_mut` mar thoradh air sin a mharcáil mar
`unsafe`, agus is féidir linn an fheidhm seo a ghlaoch ó Rust sábháilte. Chruthaíomar teibí sábháilte chuig an gcód neamhshábháilte le cur i bhfeidhm den fheidhm a úsáideann
cód `unsafe` ar bhealach sábháilte, toisc nach gcruthaíonn sé ach pointeoirí bailí ó na
sonraí a bhfuil rochtain ag an bhfeidhm seo orthu.

I gcodarsnacht leis sin, is dócha go dtitfeadh úsáid `slice::from_raw_parts_mut` i Liosta 20-7 nuair a úsáidtear an slisne. Glacann an cód seo suíomh cuimhne treallach
agus cruthaíonn sé slisne 10,000 mír ar fhad.

<Listing number="20-7" caption="Creating a slice from an arbitrary memory location">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-07/src/main.rs:here}}
```

</Listing>

Ní linn an chuimhne ag an suíomh treallach seo, agus níl aon ráthaíocht ann go bhfuil luachanna bailí `i32` sa tslis a chruthaíonn an cód seo. Má dhéantar iarracht `values` a úsáid amhail is dá mba tslis bhailí í, ní bheidh aon sainmhíniú ar iompar.


#### Feidhmeanna `extern` a Úsáid chun Cód Seachtrach a Ghlaoch

Uaireanta, b'fhéidir go mbeadh ar do chód Rust idirghníomhú le cód atá scríofa i dteanga eile. Chuige seo, tá an eochairfhocal `extern` ag Rust a éascaíonn cruthú
agus úsáid _Foreign Function Interface (FFI)_. Is bealach é FFI do
theanga ríomhchlárúcháin feidhmeanna a shainiú agus teanga ríomhchlárúcháin (eachtrannach) eile a chumasú chun na feidhmeanna sin a ghlaoch.

Léiríonn Liostáil 20-8 conas comhtháthú a bhunú leis an bhfeidhm `abs`
ón leabharlann chaighdeánach C. De ghnáth, bíonn feidhmeanna a dhearbhaítear laistigh de bhloic `extern`
neamhshábháilte le glaoch orthu ó chód Rust, mar sin ní mór iad a mharcáil mar `unsafe` freisin. Is é an chúis atá leis ná nach gcuireann teangacha eile rialacha agus ráthaíochtaí Rust i bhfeidhm, agus ní féidir le Rust iad a sheiceáil, mar sin tá an fhreagracht ar an ríomhchláraitheoir sábháilteacht a chinntiú.

<Listing number="20-8" file-name="src/main.rs" caption="Declaring and calling an `extern` function defined in another language">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-08/src/main.rs}}
```

</Listing>

Laistigh den bhloc `unsafe extern "C"`, liostaímid ainmneacha agus sínithe feidhmeanna seachtracha ó theanga eile ar mhaith linn glaoch uirthi. Sainmhíníonn an chuid `"C"` cén _comhéadan dénártha feidhmchláir (ABI)_ a úsáideann an fheidhm sheachtrach: sainmhíníonn an ABI conas glaoch ar an bhfeidhm ag leibhéal an tionóil. Is é an ABI `"C"` an ceann is coitianta agus leanann sé ABI na teanga ríomhchlárúcháin C.

Níl aon bhreithnithe sábháilteachta cuimhne ag baint leis an bhfeidhm seo, áfach.
Go deimhin, tá a fhios againn go mbeidh aon ghlao ar `abs` sábháilte i gcónaí d'aon `i32`, mar sin is féidir linn an eochairfhocal `safe` a úsáid chun a rá go bhfuil sé sábháilte glaoch ar an bhfeidhm shonrach seo cé go bhfuil sí i mbloc `unsafe extern`. Nuair a dhéanaimid an t-athrú sin, ní gá bloc `unsafe` a thuilleadh le glaoch uirthi, mar a thaispeántar i Liostáil 20-9.


<Listing number="20-9" file-name="src/main.rs" caption="Explicitly marking a function as `safe` within an `unsafe extern` block and calling it safely">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-09/src/main.rs}}
```

</Listing>

Ní chiallaíonn sé go bhfuil feidhm sábháilte má mharcálann tú í mar `safe`! Ina áit sin, is cosúil le gealltanas atá á thabhairt agat do Rust _go bhfuil sí_ sábháilte í. Is ortsa atá an fhreagracht fós a chinntiú go gcomhlíontar an gealltanas sin!


> #### Ag Glaoch ar Fheidhmeanna Rust ó Theangacha Eile
>
> Is féidir linn `extern` a úsáid freisin chun comhéadan a chruthú a ligeann do theangacha eile
> glaoch ar fheidhmeanna Rust. In ionad bloc iomlán `extern` a chruthú, cuirimid an
> eochairfhocal `extern` leis agus sonraímid an ABI le húsáid díreach roimh an eochairfhocal `fn` don
> fheidhm ábhartha. Ní mór dúinn anótáil `#[unsafe(no_mangle)]` a chur leis freisin
> chun a rá leis an tiomsaitheoir Rust gan ainm na feidhme seo a mhilleadh. Is é _Mhangling_
> ná nuair a athraíonn tiomsaitheoir an t-ainm a thugamar d'fheidhm go hainm difriúil
> ina bhfuil níos mó faisnéise do chodanna eile den phróiseas tiomsaithe le
> a úsáid ach atá níos lú inléite ag daoine. Déanann gach tiomsaitheoir teanga ríomhchlárúcháin
> ainmneacha a mhilleadh beagán difriúil, mar sin chun go mbeidh feidhm Rust inainmnithe ag
> teangacha eile, ní mór dúinn mangling ainmneacha an tiomsaitheora Rust a dhíchumasú. Tá sé seo
> neamhshábháilte mar d'fhéadfadh imbhuailtí ainmneacha a bheith ann trasna leabharlanna gan an
> mangling ionsuite, mar sin is orainne atá an fhreagracht a chinntiú go bhfuil an t-ainm atá
> easpórtáilte againn sábháilte le heaspórtáil gan mangling.
>
> Sa sampla seo a leanas, déanaimid an fheidhm `call_from_c` inrochtana ó
> chód C, tar éis í a thiomsú chuig leabharlann chomhroinnte agus a nascadh ó C:
>
> ```rust
> #[unsafe(no_mangle)]
> pub extern "C" fn call_from_c() {
> println!("Glaoite ar fheidhm Rust ó C díreach!");
> }
> ```
>
> Ní gá `unsafe` a úsáid don úsáid seo de `extern`.

### Rochtain ar Athróg Statach Inathraithe nó í a Mhodhnú

Sa leabhar seo, níor phléamar _athróga domhanda_ go fóill, a dtacaíonn Rust leo
ach is féidir leo a bheith ina gcúis le rialacha úinéireachta Rust. Má tá dhá shnáithe ag
rochtain ar an athróg dhomhanda inathraithe chéanna, is féidir leis rás sonraí a chur faoi deara.

I Rust, tugtar athróga _statacha_ ar athróga domhanda. Taispeánann liostáil 20-10
sampla dearbhaithe agus úsáid athróg statach le slisne teaghráin mar
luach.

<Listing number="20-10" file-name="src/main.rs" caption="Defining and using an immutable static variable">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-10/src/main.rs}}
```

</Listing>

Tá athróga statach cosúil le tairiseacha, a phléamar sa chuid
[“Tairiseacha”][differences-between-variables-and-constants]<!-- neamhaird -->
i gCaibidil 3. Tá ainmneacha na n-athróg statach i `SCREAMING_SNAKE_CASE` de réir
choinbhinsiúin. Ní féidir le hathróga statach tagairtí a stóráil ach leis an saolré `'static`, rud a chiallaíonn gur féidir leis an tiomsaitheoir Rust an saolré a ríomh agus nach bhfuil orainn é a anótáil go sainráite. Tá sé sábháilte rochtain a fháil ar athróg statach
neamh-athraithe.

Difríocht bheag idir tairiseacha agus athróga statach neamh-athraithe ná go
bhfuil seoladh seasta sa chuimhne ag luachanna in athróg statach. Trí úsáid a bhaint as an luach
rochtaineofar ar na sonraí céanna i gcónaí. Ar an láimh eile, ceadaítear do thairiseacha
a gcuid sonraí a dhúbailt aon uair a úsáidtear iad. Difríocht eile is ea gur féidir le hathróga statach
a bheith inathraithe. Tá sé
_neamhshábháilte_ rochtain a fháil ar athróga statach inathraithe agus iad a mhodhnú. Taispeánann liostú 20-11 conas athróg statach inathraithe darb ainm `COUNTER` a dhearbhú, rochtain a fháil uirthi agus í a mhodhnú.

<Listing number="20-11" file-name="src/main.rs" caption="Reading from or writing to a mutable static variable is unsafe">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-11/src/main.rs}}
```

</Listing>

Mar is amhlaidh le hathróga rialta, sonraímid inathraitheacht ag baint úsáide as an eochairfhocal `mut`. Aon
chód a léann nó a scríobhann ó `COUNTER`, ní mór dó a bheith laistigh de bhloc `unsafe`. Tiomsaíonn agus priontálann an
cód i Liosta 20-11 `COUNTER: 3` mar a bheimid ag súil leis
toisc go bhfuil sé snáithithe aonair. Dá mbeadh rochtain ag il-snáitheanna ar `COUNTER`, is dócha go mbeadh rásaí sonraí mar thoradh air, mar sin is iompar neamhshainithe é. Dá bhrí sin, ní mór dúinn
an fheidhm iomlán a mharcáil mar `unsafe`, agus an teorainn sábháilteachta a dhoiciméadú, ionas
go mbeidh a fhios ag aon duine a ghlaonn ar an bhfeidhm cad atá ceadaithe agus nach bhfuil ceadaithe dóibh a dhéanamh
go sábháilte.

Aon uair a scríobhaimid feidhm neamhshábháilte, is gnách trácht a scríobh
ag tosú le `SAFETY` agus ag míniú cad is gá don ghlaoiteoir a dhéanamh chun an
fheidhm a ghlaoch go sábháilte. Mar an gcéanna, aon uair a dhéanaimid oibríocht neamhshábháilte, is gnách trácht a scríobh ag tosú le `SAFETY` chun a mhíniú conas a chothaítear na
rialacha sábháilteachta.

Ina theannta sin, ní cheadóidh an tiomsaitheoir duit tagairtí a chruthú d'athróg statach inathraithe. Ní féidir leat rochtain a fháil air ach trí phointeoir amh, a cruthaíodh le ceann de na hoibreoirí iasachta amh. Áirítear leis sin cásanna ina gcruthaítear an tagairt go dofheicthe, mar nuair a úsáidtear é sa `println!` sa liostú cód seo. Cuidíonn an
riachtanas nach féidir tagairtí d'athróga statach inathraithe a chruthú ach trí
phointeoirí amha le riachtanais sábháilteachta a dhéanamh níos soiléire maidir lena n-úsáid.

Le sonraí inathraithe atá inrochtana go domhanda, tá sé deacair a chinntiú nach bhfuil aon rásaí sonraí ann, agus is é sin an fáth a mheasann Rust go bhfuil athróga statach inathraithe neamhshábháilte. Más féidir, is fearr na teicnící comhthráthachta agus na
pointeoirí cliste snáithe-shábháilte a phléamar i gCaibidil 16 a úsáid ionas go seiceálann an tiomsaitheoir go ndéantar sonraí a rochtaintear ó shnáitheanna éagsúla go sábháilte.

### Tréith Neamhshábháilte a Chur i bhFeidhm

Is féidir linn `unsafe` a úsáid chun tréith neamhshábháilte a chur i bhfeidhm. Tá tréith neamhshábháilte nuair a bhíonn roinnt neamhathróg ag ceann amháin ar a laghad dá modhanna nach féidir leis an tiomsaitheoir a fhíorú. Dearbhaímid go bhfuil tréith `unsafe` tríd an eochairfhocal `unsafe` a chur roimh `trait` agus cur i bhfeidhm na tréithe a mharcáil mar `unsafe` freisin, mar a thaispeántar i
Liostú 20-12.

<Listing number="20-12" caption="Defining and implementing an unsafe trait">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-12/src/main.rs}}
```

</Listing>


Trí úsáid a bhaint as `unsafe impl`, táimid ag gealladh go gcoimeádfaimid na neamhathraithe nach féidir leis an tiomsaitheoir a fhíorú.

Mar shampla, cuimhnigh ar na tréithe marcóra `Sync` agus `Send` a phléamar sa chuid
[“Extensible Concurrency with the `Sync` and `Send`
Traits”][extensible-concurrency-with-the-sync-and-send-traits]<!-- ignore -->
i gCaibidil 16: cuireann an tiomsaitheoir na tréithe seo i bhfeidhm go huathoibríoch má
tá ár gcineálacha comhdhéanta go hiomlán de chineálacha `Send` agus `Sync`. Má chuireann muid cineál i bhfeidhm
ina bhfuil cineál nach `Send` nó `Sync` é, amhail pointeoirí amha,
agus más mian linn an cineál sin a mharcáil mar `Send` nó `Sync`, ní mór dúinn `unsafe` a úsáid. Ní féidir le Rust
a fhíorú go gcoimeádann ár gcineál na ráthaíochtaí gur féidir é a sheoladh go sábháilte
trasna snáitheanna nó rochtain a fháil air ó il-snáitheanna; dá bhrí sin, ní mór dúinn na seiceálacha sin a dhéanamh de láimh agus a léiriú mar sin le `unsafe`.

### Rochtain ar Réimsí Aontais

Is é an gníomh deireanach nach n-oibríonn ach le `unsafe` ná rochtain a fháil ar réimsí
_union_. Tá `union` cosúil le `struct`, ach ní úsáidtear ach réimse dearbhaithe amháin
i gcás áirithe ag an am céanna. Úsáidtear aontais go príomha chun
idirghníomhú le haontais i gcód C. Tá rochtain a fháil ar réimsí aontais neamhshábháilte toisc nach féidir le Rust
cineál na sonraí atá stóráilte faoi láthair san aontais a ráthú.
Is féidir leat tuilleadh eolais a fháil faoi aontais i [an Tagairt Rust][reference].

### Úsáid a bhaint as Miri chun cód neamhshábháilte a sheiceáil

Nuair atá cód neamhshábháilte á scríobh agat, b'fhéidir gur mhaith leat a sheiceáil go bhfuil an rud atá scríofa agat
sábháilte agus ceart i ndáiríre. Ceann de na bealaí is fearr chun é sin a dhéanamh ná
[Miri][miri] a úsáid, uirlis oifigiúil Rust chun iompar neamhshainithe a bhrath. Cé gur uirlis _statach_ é an seiceálaí iasachta a oibríonn ag am tiomsaithe, is uirlis
_dinimiciúil_ é Miri a oibríonn ag am rith. Seiceálann sé do chód trí do
chlár, nó a shraith tástála, a rith, agus a bhrath nuair a sháraíonn tú na rialacha a thuigeann sé faoi conas ba chóir do Rust oibriú.

Éilíonn úsáid Miri tógáil oíche de Rust (a labhraímid faoi níos mó i
[Aguisín G: Conas a dhéantar Rust agus “Rust Oíche”][nightly]). Is féidir leat
leagan oíche de Rust agus an uirlis Miri a shuiteáil trí `rustup +nightly
component add miri` a chlóscríobh. Ní athraíonn sé seo cén leagan de Rust a úsáideann do thionscadal; ní chuireann sé ach an uirlis le do chóras ionas gur féidir leat é a úsáid nuair is mian leat.
Is féidir leat Miri a rith ar thionscadal trí `cargo +nightly miri run` nó `cargo
+nightly miri test` a chlóscríobh.

Mar shampla de cé chomh cabhrach is féidir leis seo a bheith, smaoinigh ar a tharlaíonn nuair a ritheann muid é
i gcoinne Liostála 20-11:

```console
{{#include ../../listings/ch20-advanced-features/listing-20-11/output.txt}}
```

Tugann sé faoi deara go cabhrach agus go cruinn go bhfuil tagairtí comhroinnte againn do shonraí inathraithe,
agus tugann sé rabhadh faoi. Sa chás seo, ní insíonn sé dúinn conas an
fhadhb a réiteach,
ach ciallaíonn sé go bhfuil a fhios againn go bhfuil fadhb fhéideartha ann agus gur féidir linn smaoineamh ar
conas a chinntiú go bhfuil sí sábháilte. I gcásanna eile, is féidir leis a rá linn i ndáiríre go bhfuil roinnt
cód _cinnte_ a bheith mícheart agus moltaí a dhéanamh maidir le conas é a shocrú.

Ní ghabhann Miri _gach_ rud_ a d'fhéadfá a dhéanamh mícheart agus cód neamhshábháilte á scríobh agat.

Ar an gcéad dul síos, ós rud é gur seiceáil dhinimiciúil í, ní ghabhann sé ach fadhbanna le cód
a ritheann i ndáiríre. Ciallaíonn sé sin go mbeidh ort é a úsáid i gcomhar le
teicnící tástála maithe chun do mhuinín faoin gcód neamhshábháilte a
scríobh tú a mhéadú. Ar an gcéad dul síos, ní chlúdaíonn sé gach bealach is féidir a bhféadfadh do chód
a bheith lochtach. Má _ghabhann_ Miri fadhb, tá a fhios agat go bhfuil fabht ann, ach ní chiallaíonn sé nach bhfuil fadhb ann díreach toisc nach _ghabhann_ Miri fabht. Is féidir le Miri
go leor a ghabháil, áfach. Bain triail as é a rith ar na samplaí eile de chód neamhshábháilte sa
chaibidil seo agus féach cad a deir sé!

### Cathain is Ceart Cód Neamhshábháilte a Úsáid

Níl sé mícheart ná fiú neamhaird a thabhairt ar `unsafe` a úsáid chun ceann de na cúig ghníomh (sárchumhachtaí) a pléadh díreach a dhéanamh. Ach tá sé níos deacra cód `unsafe` a fháil
ceart mar ní féidir leis an tiomsaitheoir cabhrú le sábháilteacht cuimhne a choinneáil. Nuair a bhíonn
cúis agat cód `unsafe` a úsáid, is féidir leat é sin a dhéanamh, agus má tá an nóta `unsafe` soiléir agat, is fusa foinse na bhfadhbanna a rianú nuair a tharlaíonn siad.
Aon uair a scríobhann tú cód neamhshábháilte, is féidir leat Miri a úsáid chun cabhrú leat a bheith níos muiníní
go gcomhlíonann an cód atá scríofa agat rialacha Rust.

Chun iniúchadh i bhfad níos doimhne a dhéanamh ar conas oibriú go héifeachtach le Rust neamhshábháilte, léigh
treoir oifigiúil Rust don ábhar, an [Rustonomicon][nomicon].

[dangling-references]: ch04-02-references-and-borrowing.html#dangling-references
[differences-between-variables-and-constants]: ch03-01-variables-and-mutability.html#constants
[extensible-concurrency-with-the-sync-and-send-traits]: ch16-04-extensible-concurrency-sync-and-send.html#extensible-concurrency-with-the-sync-and-send-traits
[the-slice-type]: ch04-03-slices.html#the-slice-type
[reference]: ../reference/items/unions.html
[miri]: https://github.com/rust-lang/miri
[editions]: appendix-05-editions.html
[nightly]: appendix-07-nightly-rust.html
[nomicon]: https://doc.rust-lang.org/nomicon/
