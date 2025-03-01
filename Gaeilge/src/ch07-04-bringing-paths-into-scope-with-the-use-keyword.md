## Cosáin a Thabhairt isteach sa Scóip leis an Eochairfhocal `use`

Má bhíonn ort na cosáin chun feidhmeanna a ghlaoch a scríobh, d'fhéadfadh sé a bheith deacair agus
athchleachtach. I Liosta 7-7, cibé acu a roghnaigh muid an cosán iomlán nó an cosán coibhneasta dó
an fheidhm `add_to_waitlist`, gach uair a theastaigh uainn `add_to_waitlist` a ghlaoch
bhí orainn `front_of_house` agus `hosting` a shonrú freisin. Ar ámharaí an tsaoil, tá a
bealach leis an bpróiseas seo a shimpliú: is féidir linn aicearra chuig cosán a chruthú leis an `use`
eochairfhocal uair amháin, agus ansin bain úsáid as an t-ainm níos giorra i ngach áit eile sa raon feidhme.

I Liostú 7-11, tugaimid an modúl `crate::front_of_house::hosting` isteach sa
scóip na feidhme `eat_at_restaurant` mar sin níl le déanamh againn ach a shonrú
`hosting::add_to_waitlist` chun an fheidhm `add_to_waitlist` a ghlaoch isteach i
`eat_at_restaurant`.

<Listing number="7-11" file-name="src/lib.rs" caption="Bringing a module into scope with `use`">

```rust,noplayground,test_harness
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-11/src/lib.rs}}
```

</Listing>

Nuair a chuirtear `use` agus cosán isteach i scóip tá sé cosúil le nasc siombalach a chruthú i
an córas comhaid. Trí `use crate::front_of_house::hosting` a chur leis an gcliathbhosca
root, is ainm bailí é `hosting` anois sa raon feidhme sin, díreach mar a bheadh ​​an `hosting`
Bhí modúl sainithe sa fhréamh gcliathbhosca. Cosáin tugtha isteach sa scóip le `use`
seiceáil freisin príobháideacht, mar aon cosáin eile.

Tabhair faoi deara nach gcruthaíonn `use` ach an aicearra don raon feidhme ar leith ina bhfuil an
tarlaíonn `use`. Má dhéantar liostú 7-12, bogtar an fheidhm `eat_at_restaurant` isteach i gceann nua
modúl leanbh darb ainm `customer`, a bhfuil raon feidhme difriúil aige ansin ná an `use`
ráiteas, mar sin ní thiomsóidh an comhlacht feidhme.

<Listing number="7-12" file-name="src/lib.rs" caption="A `use` statement only applies in the scope it’s in">

```rust,noplayground,test_harness,does_not_compile,ignore
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-12/src/lib.rs}}
```

</Listing>

Léiríonn earráid an tiomsaitheora nach bhfuil feidhm ag an aicearra a thuilleadh laistigh de na
modúl `customer`:

```console
{{#include ../../listings/ch07-managing-growing-projects/listing-07-12/output.txt}}
```

Tabhair faoi deara freisin go bhfuil rabhadh ann nach n-úsáidtear an `use` ina raon feidhme a thuilleadh! Chuig
deisigh an fhadhb seo, bog an `use` laistigh den mhodúl `customer` freisin, nó sa tagairt
an t-aicearra sa mhodúl tuismitheora le `super::hosting` laistigh den leanbh
modúl `customer`.

### Cosáin `Úsáide' Idéanacha á gcruthú

I Liostú 7-11, b'fhéidir gur shíl tú cén fáth ar shonraigh muid `use
crate::front_of_house::hosting` agus ansin ar a dtugtar `hosting::add_to_waitlist` isteach
`eat_at_restaurant`, seachas an cosán `use` a shonrú an bealach ar fad amach chuige
an fheidhm `add_to_waitlist` chun an toradh céanna a bhaint amach, mar atá i Liostú 7-13.

<Listing number="7-13" file-name="src/lib.rs" caption="Bringing the `add_to_waitlist` function into scope with `use`, which is unidiomatic">

```rust,noplayground,test_harness
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-13/src/lib.rs}}
```

</Listing>

Cé go ndéanann Liostú 7-11 agus Liostú 7-13 an tasc céanna, Liostáil
Is é 7-11 an gnáthbhealach chun feidhm a thabhairt isteach sa scóip le `use`. Ag tabhairt
modúl tuismitheora na feidhme isteach sa scóip le ciallaíonn `use` go gcaithfimid an
modúl tuismitheora nuair a ghlaonn tú an fheidhm. Ag sonrú an mhodúil tuismitheora cathain
Má ghlaonn tú ar an bhfeidhm, is léir nach bhfuil an fheidhm sainithe go háitiúil
agus athrá ar an gcosán iomlán á íoslaghdú fós. Is é an cód i Liosta 7-13
ní léir cá bhfuil `add_to_waitlist` sainmhínithe.

Ar an láimh eile, agus tú ag tabhairt isteach structs, enums, agus míreanna eile le `use`,
tá sé idiomatic an cosán iomlán a shonrú. Léiríonn liostú 7-14 an gnáthbhealach
chun struchtúr `HashMap` na leabharlainne caighdeánach a thabhairt isteach i scóip dhénártha
cliathbhosca.

<Listing number="7-14" file-name="src/main.rs" caption="Bringing `HashMap` into scope in an idiomatic way">

```rust
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-14/src/main.rs}}
```

</Listing>

Níl aon chúis láidir taobh thiar den idiom seo: níl ann ach an coinbhinsiún a bhfuil
tháinig sé chun cinn, agus tá taithí ag daoine ar chód Rust a léamh agus a scríobh ar an mbealach seo.

Is í an eisceacht don idiom seo ná má táimid ag tabhairt dhá mhír leis an ainm céanna
isteach sa scóip le ráitis `use`, mar ní cheadaíonn Rust é sin. Liostáil 7-15
léiríonn sé conas dhá chineál `Result` a thabhairt isteach sa scóip a bhfuil an t-ainm céanna orthu ach
modúil tuismitheoirí éagsúla, agus conas tagairt a dhéanamh dóibh.

<Listing number="7-15" file-name="src/lib.rs" caption="Bringing two types with the same name into the same scope requires using their parent modules.">

```rust,noplayground
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-15/src/lib.rs:here}}
```

</Listing>

Mar a fheiceann tú, trí na modúil tuismitheora a úsáid déantar idirdhealú idir an dá chineál `Result`.
Más rud é ina ionad sin shonraigh muid `use std::fmt::Result` agus `use std::io::Result`, dhéanfaimis
tá dhá chineál `Result` sa scóip chéanna, agus ní bheadh ​​a fhios ag Rust cén ceann atá againn
i gceist nuair a d'úsáideamar `Result`.

### Ainmneacha Nua a Sholáthar leis an Eochairfhocal `as`

Tá réiteach eile ar an bhfadhb a bhaineann le dhá chineál den ainm céanna a thabhairt
isteach sa raon feidhme céanna le `use`: tar éis an chosáin, is féidir linn a shonrú `as` agus nua
ainm áitiúil, nó _alias_, don chineál. Léiríonn liostú 7-16 bealach eile le scríobh
an cód i Liostú 7-15 trí cheann amháin den dá chineál `Result` a athainmniú ag baint úsáide as `as`.

<Listing number="7-16" file-name="src/lib.rs" caption="Renaming a type when it’s brought into scope with the `as` keyword">

```rust,noplayground
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-16/src/lib.rs:here}}
```

</Listing>

Sa dara ráiteas `use`, roghnaigh muid an t-ainm nua `IoResult` le haghaidh an
cineál `std::io::Result`, nach mbeidh ag teacht salach ar an `Result` ó `std::fmt`
a thugamar isteach sa scóip freisin. Tá Liostáil 7-15 agus Liostú 7-16
a mheastar a bheith ina ngnáthnós, mar sin tá an rogha suas duitse!

### Ainmneacha á ath-onnmhairiú le `pub use`

Nuair a thugaimid ainm isteach sa scóip leis an eochairfhocal `use`, an t-ainm atá ar fáil i
tá an raon feidhme nua príobháideach. Chun an cód a ghlaonn ár gcód a chumasú chun tagairt a dhéanamh
an t-ainm sin amhail is dá mbeadh sé sainmhínithe i raon feidhme an chóid sin, is féidir linn `pub` a chur le chéile
agus `use`. Tugtar _re-exporting_ ar an teicníocht seo toisc go bhfuil
mír isteach sa raon ach freisin an mhír sin a chur ar fáil do dhaoine eile le tabhairt isteach
a raon feidhme.

Taispeánann Liostú 7-17 an cód i Liostú 7-11 le `use` sa mhodúl fréimhe
athraigh go `pub use`.

<Listing number="7-17" file-name="src/lib.rs" caption="Making a name available for any code to use from a new scope with `pub use`">

```rust,noplayground,test_harness
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-17/src/lib.rs}}
```

</Listing>

Roimh an athrú seo, bheadh ar chód seachtrach glaoch ar an `add_to_waitlist`
feidhm ag baint úsáide as an cosán
`restaurant::front_of_house::hosting::add_to_waitlist()`, a mbeadh
D'éiligh sé go ndéanfaí an modúl `front_of_house`  a mharcáil mar `pub`. Anois go bhfuil an `pub use` 
seo tar éis an modúl `hosting` ath-onnmhairithe aón modúl fréimhe, cód seachtrach
in ann an cosán `restaurant::hosting::add_to_waitlist()` a úsáid ina ionad sin.

Tá sé úsáideach ath-onnmhairiú nuair a bhíonn struchtúr inmheánach do chód difriúil
ón gcaoi a smaoineodh ríomhchláraitheoirí a ghlaonn do chód ar an bhfearann. Le haghaidh
Mar shampla, sa mheafar bialann seo, a cheapann na daoine atá ag rith na bialainne
faoi ​​“aghaidh an tí” agus “cúl an tí.” Ach custaiméirí ag tabhairt cuairte ar bhialann
is dócha nach smaoineoidh siad ar na codanna den bhialann sna téarmaí sin. Le
`pub use`, is féidir linn ár gcód a scríobh le struchtúr amháin ach rud eile a nochtadh
struchtúr. Mar gheall air seo déanann ár leabharlann dea-eagraithe do ríomhchláraitheoirí a oibríonn uirthi
an leabharlann agus ríomhchláraitheoirí ag glaoch ar an leabharlann. Breathnóimid ar shampla eile
de `pub use` agus conas a théann sé i bhfeidhm ar dhoiciméadú do chliabhán sa [“Easpórtáil a
API Poiblí áisiúil le `pub use`”][ch14-pub-use]<!-- neamhaird a dhéanamh ar --> alt de
Caibidil 14 .

### Pacáistí Seachtracha á Úsáid

I gCaibidil 2, rinneamar tionscadal cluiche tomhais a ríomhchlárú a bhain úsáid as seachtrach
pacáiste ar a dtugtar `rand` chun uimhreacha randamacha a fháil. Chun `rand` a úsáid inár dtionscadal, déanaimid
cuireadh an líne seo le _Cargo.toml_:

!-- When updating the version of `rand` used, also update the version of
`rand` used in these files so they all match:
* ch02-00-guessing-game-tutorial.md
* ch14-03-cargo-workspaces.md
-->

<Listing file-name="Cargo.toml">

```toml
{{#include ../../listings/ch02-guessing-game-tutorial/listing-02-02/Cargo.toml:9:}}
```

</Listing>

Nuair a chuirtear `rand` isteach mar spleáchas i _Cargo.toml_ insíonn do Cargo an
pacáiste `rand` agus aon spleáchais ó [ crates.io]( https://crates.io/ ) agus
cuir `rand` ar fáil dár dtionscadal.

Ansin, chun sainmhínithe `rand` a thabhairt isteach i raon feidhme ár bpacáiste, chuireamar a
líne `use` ag tosú le hainm an chliabháin, `rand`, agus liostaigh na míreanna
bhíomar ag iarraidh a thabhairt isteach sa scóip. Thabhairt chun cuimhne go bhfuil sa [“Giniúint Randamach
Uimhir”][rand]<!-- neamhaird a dhéanamh ar --> alt i gCaibidil 2, thugamar an trait `Rng`
isteach sa raon feidhme agus tugadh an fheidhm `rand:: thread_rng` air:

``` meirge, neamhaird
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-03/src/main.rs:ch07-04}}
```

Tá go leor pacáistí curtha ar fáil ag baill de phobal Rust ag
[crates.io](https://crates.io/), agus aon cheann acu a tharraingt isteach i do phacáiste
Tá na céimeanna céanna i gceist: iad a liostú i gcomhad _Cargo.toml_ do phacáiste agus
ag baint úsáide as `use` chun míreanna óna cliathbhoscaí a thabhairt isteach sa scóip.

Tabhair faoi deara gur cliathbhosca é an leabharlann chaighdeánach `std` atá lasmuigh dár gcuid
pacáiste. Toisc go bhfuil an leabharlann caighdeánach seolta leis an teanga Rust, táimid
ní gá _Cargo.toml_ a athrú chun `std` a chur san áireamh. Ach ní mór dúinn tagairt a dhéanamh
sé le `use` chun míreanna a thabhairt as sin isteach i raon feidhme ár bpacáiste. Mar shampla,
le `HashMap` d'úsáidfimid an líne seo:

```rust
use std::collections::HashMap;
```

Is cosán iomlán é seo ag tosú le `std`, ainm na leabharlainne caighdeánach
cliathbhosca.

### Conairí Neadaithe a Úsáid chun Liostaí Móra `use` a ghlanadh

Má táimid ag baint úsáide as míreanna iolracha atá sainithe sa chliabhán céanna nó sa mhodúl céanna, liostáil
is féidir le gach mír ar a líne féin go leor spáis ingearach a ghlacadh inár gcomhaid. Le haghaidh
Mar shampla, an dá ráiteas `use` seo a bhí againn sa chluiche buille faoi thuairim i Liosta 2-4
tabhair míreanna ó `std` isteach sa scóip:

<Listing file-name="src/main.rs">

```rust,ignore
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/no-listing-01-use-std-unnested/src/main.rs:here}}
```

</Listing>

Ina áit sin, is féidir linn cosáin neadaithe a úsáid chun na míreanna céanna a thabhairt isteach i raon feidhme amháin
líne. Déanaimid é seo trí chomhchuid an chosáin a shonrú, agus dhá cheann ina dhiaidh
colons, agus ansin lúibíní chatach thart ar liosta de na codanna de na cosáin a
difriúil, mar a thaispeántar i Liosta 7-18.

<Listing number="7-18" file-name="src/main.rs" caption="Specifying a nested path to bring multiple items with the same prefix into scope">

```rust,ignore
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-18/src/main.rs:here}}
```

</Listing>

I gcláir níos mó, a thabhairt go leor míreanna i raon feidhme as an gcliathbhosca céanna nó
Is féidir le modúl ag baint úsáide as cosáin neadaithe líon na ráiteas `use` ar leith a laghdú
ag teastáil go leor!

Is féidir linn cosán neadaithe a úsáid ar aon leibhéal i gcosán, rud atá úsáideach nuair a chuirtear le chéile
dhá ráiteas `use` a roinneann fobhealach. Mar shampla, taispeánann Liostú 7-19 dhá cheann
ráitis `use`: ceann a thugann `std::io` isteach sa scóip agus ceann a thugann
`std::io::Write` isteach sa scóip.

<Listing number="7-19" file-name="src/lib.rs" caption="Two `use` statements where one is a subpath of the other">

```rust,noplayground
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-19/src/lib.rs}}
```

</Listing>

Is é an chuid choitianta den dá chonair seo ná `std::io`, agus sin an chéad cheann iomlán
cosán. Chun an dá chonair seo a chumasc i ráiteas amháin `use`, is féidir linn `self` a úsáid isteach
an cosán neadaithe, mar a thaispeántar i Liosta 7-20.

<Listing number="7-20" file-name="src/lib.rs" caption="Combining the paths in Listing 7-19 into one `use` statement">

```rust,noplayground
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-20/src/lib.rs}}
```

</Listing>

Tugann an líne seo `std::io` agus `std::io::Write` isteach sa scóip.

### An tOibreoir Glob

Más mian linn _all_ míreanna poiblí atá sainithe i gcosán isteach sa raon feidhme a thabhairt, is féidir linn
sonraigh an cosán sin a leanann an t-oibreoir `*` glob:

```rust
use std::collections::*;
```

Tugann an ráiteas `use` seo na míreanna poiblí go léir atá sainmhínithe in `std::collections` isteach
an raon feidhme reatha. Bí cúramach agus an t-oibreoir glob á úsáid agat! Is féidir le Glob é a dhéanamh
níos deacra a insint cad iad na hainmneacha atá sa raon feidhme agus cén áit a úsáidtear ainm i do chlár
shainmhíníodh.

Is minic a úsáidtear an t-oibreoir glob agus é ag tástáil chun gach rud a thabhairt faoi thástáil
isteach sa mhodúl `tests`; Labhróimid faoi sin sa [“Conas Scríobh
Tástálacha”][writing-tests]<!-- neamhaird --> alt i gCaibidil 11. An t-oibreoir glob
úsáidtear uaireanta freisin mar chuid den phatrún réamhluí: féach [na doiciméid chaighdeánacha leabharlainne](../std/prelude/index.html#other-preludes) <!-- neamhaird -->
chun tuilleadh eolais a fháil ar an bpatrún sin.

[ch14-pub-use]: ch14-02-publishing-to-crates-io.html#exporting-a-convenient-public-api-with-pub-use
[rand]: ch02-00-guessing-game-tutorial.html#generating-a-random-number
[writing-tests]: ch11-01-writing-tests.html#how-to-write-tests