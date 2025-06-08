## Tréithe Ardleibhéil

Phléamar tréithe ar dtús sa chuid [“Tréithe: Sainmhíniú Iompair
Chomhroinnte”][traits-defining-shared-behavior]<!-- ignore --> de Chaibidil
10, ach níor phléamar na sonraí níos airde. Anois go bhfuil tuilleadh eolais agat
faoi Rust, is féidir linn dul isteach sa mhionsonraí.

### Cineálacha Áitshealbhóirí a Shonrú i Sainmhínithe Tréithe le Cineálacha Gaolmhara

Ceanglaíonn _cineálacha gaolmhara_ áitshealbhóir cineáil le tréith sa chaoi is gur féidir leis na sainmhínithe
modhanna na dtréithe na cineálacha áitshealbhóirí seo a úsáid ina sínithe. Sonróidh
cur i bhfeidhm tréithe an cineál coincréite atá le húsáid in ionad an
chineáil
áitshealbhóra don chur i bhfeidhm ar leith. Ar an mbealach sin, is féidir linn
tréith a shainiú a úsáideann cineálacha áirithe gan a bheith ar an eolas go díreach cad iad na cineálacha sin
go dtí go gcuirtear an tréith i bhfeidhm.

Tá cur síos déanta againn ar an gcuid is mó de na gnéithe ardleibhéil sa chaibidil seo mar rud nach bhfuil
gá leo go minic. Tá cineálacha gaolmhara áit éigin sa lár: úsáidtear iad níos annamh ná gnéithe a mhínítear sa chuid eile den leabhar ach níos coitianta ná go leor de na gnéithe eile a phléitear sa chaibidil seo.

Sampla amháin de thréith le cineál gaolmhar ná an tréith `Iterator` a sholáthraíonn an
leabharlann chaighdeánach. Tugtar `Item` ar an gcineál gaolmhar agus seasann sé
do chineál na luachanna a bhfuil an cineál a chuireann an tréith `Iterator` i bhfeidhm ag
athrá orthu. Tá sainmhíniú an tréithe `Iterator` mar a thaispeántar i Liosta
20-13.

<Listing number="20-13" caption="The definition of the `Iterator` trait that has an associated type `Item`">

```rust,noplayground
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-13/src/lib.rs}}
```

</Listing>

Is áitchoinneálaí é an cineál `Item`, agus léiríonn sainmhíniú an mhodha `next` go dtabharfaidh sé luachanna den chineál `Option<Self::Item>` ar ais. Sonróidh feidhmitheoirí an tréith `Iterator` an cineál coincréite do `Item`, agus tabharfaidh an modh `next` `Option` ar ais ina bhfuil luach den chineál coincréite sin.

D’fhéadfadh sé go mbeadh cuma choincheap cosúil le cineálacha comhlachaithe le cineálacha, sa mhéid is go gceadaíonn an dara ceann dúinn feidhm a shainiú gan a shonrú cé na cineálacha is féidir léi a láimhseáil. Chun an difríocht idir an dá choincheap a scrúdú, féachfaimid ar
chur i bhfeidhm an tréith `Iterator` ar chineál darb ainm `Counter` a shonraíonn
gurb é an cineál `Item` ná `u32`:

<Listing file-name="src/lib.rs">

```rust,ignore
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-22-iterator-on-counter/src/lib.rs:ch19}}
```

</Listing>

Is cosúil go bhfuil an comhréir seo inchomparáide le comhréir na gcineál. Mar sin, cén fáth nach sainmhínítear an tréith `Iterator` le cinn ghinearálta, mar a thaispeántar i Liosta 20-14?

<Listing number="20-14" caption="A hypothetical definition of the `Iterator` trait using generics">

```rust,noplayground
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-14/src/lib.rs}}
```

</Listing>

Is é an difríocht ná nuair a úsáidtear cineálacha, mar atá i Liostáil 20-14, ní mór dúinn na cineálacha i ngach cur i bhfeidhm a anótáil; toisc gur féidir linn `Iterator<String> for Counter` nó aon chineál eile a chur i bhfeidhm freisin, d'fhéadfaimis il-chur i bhfeidhm de `Iterator` a bheith againn le haghaidh `Counter`. I bhfocail eile, nuair a bhíonn paraiméadar cineálach ag tréith, is féidir é a chur i bhfeidhm do chineál arís agus arís eile, ag athrú
na gcineálacha coincréiteacha de na paraiméadair chineálacha cineálacha gach uair. Nuair a úsáidimid an modh
`next` ar `Counter`, bheadh ​​orainn anótálacha cineáil a sholáthar chun
a léiriú cén cur i bhfeidhm de `Iterator` is mian linn a úsáid.

Le cineálacha gaolmhara, ní gá dúinn cineálacha a anótáil toisc nach féidir linn
tréith a chur i bhfeidhm ar chineál arís agus arís eile. I Liostáil 20-13 leis an
sainmhíniú a úsáideann cineálacha gaolmhara, ní féidir linn a roghnú ach uair amháin cén cineál
`Item` a bheidh ann, toisc nach féidir ach `impl Iterator for Counter` amháin a bheith ann. Ní gá dúinn a shonrú go dteastaíonn athrá de luachanna `u32` uainn i ngach áit
a dtugaimid `next` air ar `Counter`.

Bíonn cineálacha gaolmhara mar chuid de chonradh an tréithe freisin: ní mór do chur i bhfeidhm an
tréithe cineál a sholáthar chun seasamh in ionad an áitchoinneálaí cineál gaolmhar.
Is minic a bhíonn ainm ag cineálacha gaolmhara a chuireann síos ar an gcaoi a n-úsáidfear an cineál,
agus is dea-chleachtas é an cineál gaolmhar a dhoiciméadú sa doiciméadú API.

### Paraiméadair Réamhshocraithe Cineál Ginéireach agus Ró-Ualach Oibreora

Nuair a úsáidimid paraiméadair chineál ginéireacha, is féidir linn cineál coincréite réamhshocraithe a shonrú don
chineál ginéireach. Cuireann sé seo deireadh leis an ngá atá ag cur i bhfeidhm an tréithe
cineál coincréite a shonrú má oibríonn an cineál réamhshocraithe. Sonraíonn tú cineál réamhshocraithe
nuair a bhíonn cineál ginéireach á dhearbhú leis an gcomhréir `<PlaceholderType=ConcreteType>`.

Sampla iontach de chás ina bhfuil an teicníc seo úsáideach ná le _operator
overloading_, ina ndéanann tú iompar oibreora (mar shampla `+`) a shaincheapadh
i gcásanna áirithe.

Ní cheadaíonn Rust duit d’oibreoirí féin a chruthú ná ró-ualach a chur ar oibreoirí treallacha. Ach is féidir leat ró-ualach a chur ar na hoibríochtaí agus na tréithe comhfhreagracha atá liostaithe i `std::ops` trí na tréithe a bhaineann leis an oibreoir a chur i bhfeidhm. Mar shampla, i Liosta 20-15 ró-ualach a chur ar an oibreoir `+` chun dhá chás `Point` a chur le chéile. Déanaimid é seo tríd an tréith `Add` a chur i bhfeidhm ar struchtúr `Point`:

<Listing number="20-15" file-name="src/main.rs" caption="Implementing the `Add` trait to overload the `+` operator for `Point` instances">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-15/src/main.rs}}
```

</Listing>

Cuireann an modh `add` luachanna `x` dhá chás `Point` agus luachanna `y` dhá chás `Point` le chéile chun `Point` nua a chruthú. Tá cineál gaolmhar leis an tréith `Add` darb ainm `Output` a chinneann an cineál a fhilleann an modh `add`.

Tá an cineál cineálach réamhshocraithe sa chód seo laistigh den tréith `Add`. Seo a shainmhíniú:

```rust
trait Add<Rhs=Self> {
    type Output;

    fn add(self, rhs: Rhs) -> Self::Output;
}
```

Ba chóir go mbeadh an cód seo cosúil le rud éigin eolach: tréith le modh amháin agus
cineál gaolmhar. Is é `Rhs=Self` an chuid nua: tugtar _paraiméadair
cineáil_ réamhshocraithe_ ar an gcomhréir seo. Sainmhíníonn an paraiméadar cineáil cineálach `Rhs` (gearr do “taobh na láimhe deise”) cineál an pharaiméadair `rhs` sa mhodh `add`. Mura
shonraímid
cineál coincréite do `Rhs` nuair a chuirfimid an tréith `Add` i bhfeidhm, beidh cineál
`Rhs` réamhshocraithe go `Self`, arb é an cineál a bheidh á chur i bhfeidhm againn
`Add` air.

Nuair a chuireamar `Add` i bhfeidhm do `Point`, d'úsáideamar an réamhshocrú do `Rhs` mar gur
theastaigh uainn dhá chás `Point` a chur leis. Féachfaimid ar shampla de chur i bhfeidhm
na tréithe `Add` áit ar mian linn an cineál `Rhs` a shaincheapadh seachas an
réamhshocrú a úsáid.

Tá dhá struchtúr againn, `Millimeters` agus `Meters`, a bhfuil luachanna acu in aonaid
difriúla. Tugtar an patrún _newtype_ ar an bhfillteán tanaí seo de chineál atá ann cheana féin i struchtúr eile, a dhéanaimid cur síos níos mine air sa chuid [“Ag Úsáid an Phatrúin Newtype
chun Tréithe Seachtracha a Chur i bhFeidhm ar Chineálacha Seachtracha”][newtype]<!-- ignore
-->. Ba mhaith linn luachanna i milliméadair a chur le luachanna i méadair agus go
ndéanfadh cur i bhfeidhm `Add` an tiontú i gceart. Is féidir linn `Add` a chur i bhfeidhm
le haghaidh `Millimeters` le `Meters` mar an `Rhs`, mar a thaispeántar i Liostáil 20-16.

<Listing number="20-16" file-name="src/lib.rs" caption="Implementing the `Add` trait on `Millimeters` to add `Millimeters` to `Meters`">

```rust,noplayground
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-16/src/lib.rs}}
```

</Listing>

Chun `Millimeters` agus `Meters` a chur leis, sonraímid `impl Add<Meters>` chun luach an pharaiméadair chineáil `Rhs` a shocrú in ionad an réamhshocraithe `Self` a úsáid.

Úsáidfidh tú paraiméadair chineáil réamhshocraithe ar dhá phríomhbhealach:

- Chun cineál a leathnú gan an cód atá ann cheana a bhriseadh
- Chun saincheapadh a cheadú i gcásanna sonracha nach mbeidh gá ag formhór na n-úsáideoirí leis

Is sampla den dara cuspóir é tréith `Add` na leabharlainne caighdeánaí:
de ghnáth, cuirfidh tú dhá chineál cosúil leis, ach soláthraíonn an tréith `Add` an cumas
saincheapadh níos faide ná sin. Má úsáidtear paraiméadar cineáil réamhshocraithe sa sainmhíniú tréithe `Add`, ciallaíonn sé nach gá duit an paraiméadar breise a shonrú an chuid is mó den
am. I bhfocail eile, níl gá le beagán cur i bhfeidhm, rud a fhágann
go bhfuil sé níos éasca an tréith a úsáid.

Tá an chéad chuspóir cosúil leis an dara ceann ach ar a mhalairt: más mian leat
paraiméadar cineáil a chur le tréith atá ann cheana féin, is féidir leat réamhshocrú a thabhairt dó chun
síneadh feidhmiúlacht na tréithe a cheadú gan an
cód cur chun feidhme atá ann cheana a bhriseadh.

### Comhréir Láncháilithe le haghaidh Dí-athbhrí: Glaoch ar Mhodhanna leis an Ainm Céanna

Níl aon rud i Rust a chuireann cosc ​​ar thréith modh a bheith aici leis an ainm céanna
le
modh tréithe eile, agus ní chuireann Rust cosc ​​ort an dá thréith a chur i bhfeidhm
ar chineál amháin. Is féidir freisin modh a chur i bhfeidhm go díreach ar an gcineál leis
an t-ainm céanna le modhanna ó thréithe.

Nuair a bhíonn tú ag glaoch ar mhodhanna leis an ainm céanna, beidh ort a insint do Rust cé acu ceann is mian leat a úsáid. Smaoinigh ar an gcód i Liostáil 20-17 áit a bhfuil dhá thréith sainmhínithe againn,
`Pilot` agus `Wizard`, a bhfuil modh ar a dtugtar `fly` acu araon. Ansin cuirimid an dá thréith i bhfeidhm ar chineál `Human` a bhfuil modh ar a dtugtar `fly` curtha i bhfeidhm air cheana féin. Déanann gach modh `fly` rud éigin difriúil.

<Listing number="20-17" file-name="src/main.rs" caption="Two traits are defined to have a ` method and are implemented on the `Human` type, and a `fly` method is implemented on `Human` directly">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-17/src/main.rs:here}}
```

</Listing>

Nuair a ghlaonn muid `fly` ar shampla de `Human`, glaonn an tiomsaitheoir ar an modh atá curtha i bhfeidhm go díreach ar an gcineál de réir réamhshocraithe, mar a thaispeántar i Liostáil 20-18.

<Listing number="20-18" file-name="src/main.rs" caption="Calling `fly` on an instance of `Human`">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-18/src/main.rs:here}}
```

</Listing>

Trí an cód seo a rith, priontálfar `*waving arms furiously*`, rud a thaispeánann gur ghlaoigh Rust ar an modh `fly` a cuireadh i bhfeidhm ar `Human` go díreach.

Chun na modhanna `fly` a ghlaoch ón tréith `Pilot` nó ón tréith `Wizard`,
ní mór dúinn comhréir níos soiléire a úsáid chun a shonrú cén modh `fly` atá i gceist againn.
Léiríonn liostú 20-19 an comhréir seo.

<Listing number="20-19" file-name="src/main.rs" caption="Specifying which trait’s `fly` method we want to call">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-19/src/main.rs:here}}
```

</Listing>

Trí ainm na tréithe a shonrú roimh ainm na modha, soiléirítear do Rust cén cur i bhfeidhm de `fly` ar mhaith linn glaoch air. D’fhéadfaimis `Human::fly(&person)` a scríobh freisin, atá coibhéiseach leis an `person.fly()` a d’úsáideamar i Liosta 20-19, ach tá sé seo beagán níos faide le scríobh mura gá dúinn
díbhriú.

Nuair a ritheann tú an cód seo, priontáiltear an méid seo a leanas:

```console
{{#include ../../listings/ch20-advanced-features/listing-20-19/output.txt}}
```

Ós rud é go nglacann an modh `fly` paraiméadar `self`, dá mbeadh dhá _chineál_ againn a
chuireann _trait_ amháin i bhfeidhm, d'fhéadfadh Rust a dhéanamh amach cén cur i bhfeidhm de
thréith le húsáid bunaithe ar an gcineál `self`.

Mar sin féin, ní bhíonn paraiméadar `self` ag feidhmeanna gaolmhara nach modhanna iad. Nuair a bhíonn cineálacha nó tréithe iolracha ann a shainíonn feidhmeanna neamh-mhodhacha
leis an ainm feidhme céanna, ní bhíonn a fhios ag Rust i gcónaí cén cineál atá i gceist agat
mura n-úsáideann tú _syntax láncháilithe_. Mar shampla, i Liosta 20-20
cruthaímid tréith do dhídean ainmhithe ar mian leis _Spot_ a thabhairt ar gach madra óg.
Déanaimid tréith `Animal` le feidhm neamh-mhodhach ghaolmhar `baby_name`.
Cuirtear an tréith `Animal` i bhfeidhm don struchtúr `Dog`, ar a soláthraímid
feidhm neamh-mhodhach ghaolmhar `baby_name` go díreach freisin.

<Listing number="20-20" file-name="src/main.rs" caption="A trait with an associated function and a type with an associated function of the same name that also implements the trait">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-20/src/main.rs}}
```

</Listing>

Cuirimid an cód chun ainm a thabhairt do na coileáiníní go léir Spot i bhfeidhm sa fheidhm `baby_name` a bhaineann le `Dog`. Cuireann an cineál `Dog` an tréith `Animal` i bhfeidhm freisin, a chuireann síos ar thréithe atá ag gach ainmhí. Tugtar coileáiníní ar mhadraí óga, agus léirítear é sin i gcur i bhfeidhm na tréithe `Animal` ar `Dog` sa fheidhm `baby_name` a bhaineann leis an tréith `Animal`.

I `main`, glaoimid ar an bhfeidhm `Dog::baby_name`, a ghlaonn ar an bhfeidhm
ghaolmhar a shainmhínítear ar `Dog` go díreach. Priontálann an cód seo an méid seo a leanas:

```console
{{#include ../../listings/ch20-advanced-features/listing-20-20/output.txt}}
```

Ní hé seo an t-aschur a theastaigh uainn. Ba mhaith linn glaoch ar an bhfeidhm `baby_name` atá mar chuid den tréith `Animal` a chuireamar i bhfeidhm ar `Dog` ionas go bpriontálann an cód `A baby dog is called a puppy`. Ní chabhraíonn an teicníc chun ainm na tréithe a shonrú a
úsáideamar i Liostáil 20-19 anseo; má athraímid `main` go dtí an cód i
Liostáil 20-21, gheobhaimid earráid tiomsaithe.

<Listing number="20-21" file-name="src/main.rs" caption="Attempting to call the `baby_name` function from the `Animal` trait, but Rust doesn’t know which implementation to use">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-21/src/main.rs:here}}
```

</Listing>

Ós rud é nach bhfuil paraiméadar `self` ag `Animal::baby_name`, agus go bhféadfadh cineálacha eile a bheith ann a chuireann an tréith `Animal` i bhfeidhm, ní féidir le Rust a dhéanamh amach cén
cur i bhfeidhm de `Animal::baby_name` atá uainn. Gheobhaimid an earráid tiomsaitheora seo:

<Listing number="20-22" file-name="src/main.rs" caption="Using fully qualified syntax to specify that we want to call the `baby_name` function from the `Animal` trait as implemented on `Dog`">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-22/src/main.rs:here}}
```

</Listing>

Táimid ag soláthar nóta cineáil do Rust laistigh de na lúibíní uillinne, rud a léiríonn gur mian linn glaoch ar an modh `baby_name` ón tréith `Animal` mar atá curtha i bhfeidhm ar `Dog` trína rá gur mian linn an cineál `Dog` a chóireáil mar `Animal` don ghlao feidhme seo. Priontálfaidh an cód seo anois an rud atá uainn:

```console
{{#include ../../listings/ch20-advanced-features/listing-20-22/output.txt}}
```

Go ginearálta, sainmhínítear comhréir láncháilithe mar seo a leanas:

```rust,ignore
<Type as Trait>::function(receiver_if_method, next_arg, ...);
```

I gcás feidhmeanna gaolmhara nach modhanna iad, ní bheadh ​​​​`glacadóir` ann:
ní bheadh ​​​​ann ach liosta d'argóintí eile. D'fhéadfá comhréir láncháilithe a úsáid i ngach áit a nglaonn tú ar fheidhmeanna nó ar mhodhanna. Mar sin féin, ceadaítear duit
aon chuid den chomhréir seo a fhágáil ar lár is féidir le Rust a dhéanamh amach ó fhaisnéis eile
sa chlár. Ní gá duit an comhréir níos foclach seo a úsáid ach amháin i gcásanna ina
bhfuil il-chur i bhfeidhm ann a úsáideann an t-ainm céanna agus go dteastaíonn cabhair ó Rust
chun a aithint cén cur i bhfeidhm ar mhaith leat glaoch air.

### Úsáid a bhaint as Supertréithe chun Feidhmiúlacht Tréithe amháin a Éileamh laistigh de Thréith Eile

Uaireanta, d'fhéadfá sainmhíniú tréithe a scríobh a bhraitheann ar thréith eile:
chun go gcuirfidh cineál an chéad tréith i bhfeidhm, ba mhaith leat a cheangal ar an gcineál sin
an dara tréith a chur i bhfeidhm freisin. Dhéanfá é seo ionas gur féidir le do shainmhíniú tréithe
úsáid a bhaint as míreanna gaolmhara an dara tréith. Tugtar _supertréith_ de do thréith ar an tréith a bhfuil do shainmhíniú tréithe ag brath uirthi.

Mar shampla, abair gur mian linn tréith `OutlinePrint` a chruthú le modh `outline_print` a phriontálfaidh luach ar leith atá formáidithe sa chaoi is go bhfuil sé
frámaithe i réaltaí. Is é sin le rá, i gcás struchtúr `Point` a chuireann an
tréith chaighdeánach leabharlainne `Display` i bhfeidhm chun `(x, y)` a thabhairt, nuair a ghlaonn muid `outline_print` ar shampla `Point` a bhfuil `1` aige do `x` agus `3` do `y`, ba chóir dó
an méid seo a leanas a phriontáil:

```text
**********
*        *
* (1, 3) *
*        *
**********
```

Agus an modh `outline_print` á chur i bhfeidhm, ba mhaith linn feidhmiúlacht an tréithe `Display` a úsáid. Dá bhrí sin, ní mór dúinn a shonrú nach n-oibreoidh an tréith `OutlinePrint` ach amháin do chineálacha a chuireann `Display` i bhfeidhm freisin agus a sholáthraíonn an fheidhmiúlacht a theastaíonn ó `OutlinePrint`. Is féidir linn é sin a dhéanamh sa
sainmhíniú tréithe trí `OutlinePrint: Display` a shonrú. Tá an teicníc seo
cosúil le tréith atá ceangailte leis an tréith a chur leis. Taispeánann liostú 20-23
cur i bhfeidhm an tréithe `OutlinePrint`.

<Listing number="20-23" file-name="src/main.rs" caption="Implementing the `OutlinePrint` trait that requires the functionality from `Display`">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-23/src/main.rs:here}}
```

</Listing>

Ós rud é gur shonraigh muid go n-éilíonn `OutlinePrint` an tréith `Display`, is féidir linn an fheidhm `to_string` a úsáid a chuirtear i bhfeidhm go huathoibríoch d'aon chineál
a chuireann `Display` i bhfeidhm. Dá ndéanfaimis iarracht `to_string` a úsáid gan
colon a chur leis agus an tréith `Display` a shonrú i ndiaidh ainm na tréithe, gheobhaimis
earráid ag rá nach bhfuarthas aon mhodh darb ainm `to_string` don chineál `&Self` sa
raon feidhme reatha.

Feicfimid cad a tharlaíonn nuair a dhéanaimid iarracht `OutlinePrint` a chur i bhfeidhm ar chineál
nach gcuireann `Display` i bhfeidhm, amhail an struchtúr `Point`:

<Listing file-name="src/main.rs">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-02-impl-outlineprint-for-point/src/main.rs:here}}
```

</Listing>

Faighimid earráid ag rá go bhfuil `Display` riachtanach ach nach bhfuil sé curtha i bhfeidhm:

```console
{{#include ../../listings/ch20-advanced-features/no-listing-02-impl-outlineprint-for-point/output.txt}}
```

Chun seo a shocrú, cuirimid `Display` i bhfeidhm ar `Point` agus sásaímid an srian a éilíonn `OutlinePrint`, mar seo:
<Listing file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/no-listing-03-impl-display-for-point/src/main.rs:here}}
```

</Listing>

Ansin, má chuirtear an tréith `OutlinePrint` i bhfeidhm ar `Point`, déanfar tiomsú go rathúil, agus is féidir linn glaoch ar `outline_print` ar shampla `Point` chun é a thaispeáint
laistigh d'imlíne réaltaí.

### Ag Úsáid an Phatrúin Newtype chun Tréithe Seachtracha a Chur i bhFeidhm ar Chineálacha Seachtracha

I gCaibidil 10 sa chuid [“Implementing a Trait on a
Cineál”][implementing-a-trait-on-a-type]<!-- ignore -->, luaigh muid an
riail dílleachta a deir nach gceadaítear dúinn tréith a chur i bhfeidhm ar chineál ach amháin má tá an tréith nó an cineál áitiúil dár gcliathbhosca. Is féidir an
srian seo a sheachaint trí úsáid a bhaint as an pattern _newtype_, rud a bhaineann le cineál nua a chruthú i struchtúr tuple. (Phléamar struchtúir tupla sa chuid [“Úsáid Struchtúir Tupla gan Réimsí Ag Úsáid le Réimsí Ag Cruthú Cineálacha Difriúla”][tuple-structs]<!-- ignore --> de Chaibidil 5.) Beidh réimse amháin ag an struchtúr tupla agus beidh sé ina fhillteán tanaí timpeall an chineáil ar mhaith linn tréith a chur i bhfeidhm dó. Ansin, beidh an cineál fillteáin áitiúil dár gcliathbhosca, agus is féidir linn an tréith a chur i bhfeidhm ar an bhfillteán.

Is téarma é _Newtype_ a thagann ón teanga ríomhchlárúcháin Haskell.
Níl aon phionós feidhmíochta rith-ama ann as an patrún seo a úsáid, agus baintear an
cineál fillteáin as ag am tiomsaithe.

Mar shampla, abair gur mhaith linn `Display` a chur i bhfeidhm ar `Vec<T>`, rud a choisceann an riail dílleachta orainn a dhéanamh go díreach toisc go bhfuil an tréith `Display` agus an cineál `Vec<T>` sainmhínithe lasmuigh dár gcliathbhosca. Is féidir linn struchtúr `Wrapper` a dhéanamh a bhfuil sampla de `Vec<T>` ann; ansin is féidir linn `Display` a chur i bhfeidhm ar `Wrapper` agus an luach `Vec<T>` a úsáid, mar a thaispeántar i Liosta 20-24.

<Listing number="20-24" file-name="src/main.rs" caption="Creating a `Wrapper` type around `Vec<String>` to implement `Display`">

```rust
{{#rustdoc_include ../../listings/ch20-advanced-features/listing-20-24/src/main.rs}}
```

</Listing>

Úsáideann cur i bhfeidhm `Display` `self.0` chun rochtain a fháil ar an `Vec<T>` istigh,
toisc gur struchtúr tupla é `Wrapper` agus gurb é `Vec<T>` an ​​mhír ag innéacs 0 sa
tupla. Ansin is féidir linn feidhmiúlacht an tréithe `Display` a úsáid ar `Wrapper`.

Is é an míbhuntáiste a bhaineann leis an teicníc seo a úsáid ná gur cineál nua é `Wrapper`, mar sin níl na modhanna den luach atá aige aige. Bheadh ​​orainn gach modh de `Vec<T>` a chur i bhfeidhm go díreach ar `Wrapper` sa chaoi is go dtarmligfidh na modhanna chuig `self.0`, rud a ligfeadh dúinn `Wrapper` a chóireáil díreach mar
`Vec<T>`. Dá mba mhian linn go mbeadh gach modh atá ag an gcineál istigh ag an gcineál nua,
bheadh ​​an tréith `Deref` (a phléitear i gCaibidil 15 sa rannán [“Treating Smart
Pointers Like Regular References with the `Deref`
Trait”][smart-pointer-deref]<!-- ignore -->) ar an `Wrapper` chun an cineál istigh a thabhairt ar ais ina réiteach. Mura mian linn go mbeadh gach modh den chineál istigh ag an gcineál `Wrapper`—mar shampla, chun iompar an chineáil `Wrapper` a shrianadh—bheadh ​​orainn na modhanna amháin atá uainn a chur i bhfeidhm de láimh.

Tá an patrún cineál nua seo úsáideach fiú nuair nach bhfuil tréithe i gceist. Déanaimis an fócas a athrú agus breathnú ar roinnt bealaí chun cinn chun idirghníomhú le córas cineáil Rust.

[newtype]: ch20-02-advanced-traits.html#using-the-newtype-pattern-to-implement-external-traits-on-external-types
[implementing-a-trait-on-a-type]: ch10-02-traits.html#implementing-a-trait-on-a-type
[traits-defining-shared-behavior]: ch10-02-traits.html#traits-defining-shared-behavior
[smart-pointer-deref]: ch15-02-deref.html#treating-smart-pointers-like-regular-references-with-the-deref-trait
[tuple-structs]: ch05-01-defining-structs.html#using-tuple-structs-without-named-fields-to-create-different-types