## Cineálacha Ginearálta Sonraí

Bainimid úsáid as generics chun sainmhínithe a chruthú le haghaidh míreanna cosúil le sínithe feidhm nó
structs, ar féidir linn a úsáid ansin le go leor cineálacha sonraí nithiúla éagsúla. Déanaimis
breathnú ar dtús ar conas feidhmeanna, struchtúir, enums, agus modhanna a shainiú ag baint úsáide as
cineálach. Ansin pléifimid conas a théann cineálacha cineálacha i bhfeidhm ar fheidhmíocht cód.

### I Sainmhínithe Feidhme

Nuair a shainítear feidhm a úsáideann generics, cuirimid na cineálacha cineálacha sa
síniú na feidhme ina mbeadh muid a shonrú de ghnáth ar na cineálacha sonraí an
paraiméadair agus luach tuairisceáin. Déanann sé sin ár gcód níos solúbtha agus cuireann sé ar fáil
níos mó feidhmiúlachta do ghlaoiteoirí ar ár bhfeidhm agus dúbailt cóid a chosc.

Ag leanúint lenár bhfeidhm `largest`, léiríonn Liostú 10-4 dhá fheidhm a
Faigheann an dá cheann an luach is mó i slice. Déanfaimid iad seo a chomhcheangal ina n-aonar ansin
feidhm a úsáideann generics.

<Listing number="10-4" file-name="src/main.rs" caption="Two functions that differ only in their names and in the types in their signatures">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-04/src/main.rs:here}}
```

</Listing>

Is í an fheidhm `largest_i32` an ceann a bhaineamar amach i Liostú 10-3 a aimsíonn
an `i32` is mó i slisne. Faigheann an fheidhm `largest_char` an ceann is mó
`char` i slisne. Tá an cód céanna ag na comhlachtaí feidhme, mar sin cuirimis deireadh leis
an dúbailt trí pharaiméadar cineálach a thabhairt isteach in aon fheidhm amháin.

Chun na cineálacha a pharaiméadarú i bhfeidhm aonair nua, ní mór dúinn an cineál a ainmniú
paraiméadar, díreach mar a dhéanaimid do na paraiméadair luacha go dtí feidhm. Is féidir leat úsáid a bhaint as
aon aitheantóir mar ainm paraiméadar cineáil. Ach úsáidfimid `T` mar gheall ar, le
coinbhinsiún, tá ainmneacha paraiméadar cineál i Rust gearr, go minic ach litir amháin, agus
Is é Coinbhinsiún Cineál-ainmnithe Rust UpperCamelCase. Gearr do _type_, is é `T` an
rogha réamhshocraithe an chuid is mó de ríomhchláraitheoirí Rust.

Nuair a úsáidimid paraiméadar i gcorp na feidhme, ní mór dúinn a dhearbhú an
ainm paraiméadar sa síniú ionas go mbeidh a fhios ag an tiomsaitheoir cad a chiallaíonn an t-ainm sin.
Mar an gcéanna, nuair a úsáidimid ainm paraiméadar cineál i síniú feidhm, ní mór dúinn
chun an t-ainm paraiméadar cineál a dhearbhú sula n-úsáidfimid é. Chun an cineálach a shainiú
an fheidhm `largest`, cuirimid dearbhuithe cineál-ainm taobh istigh de lúibíní uillinne,
`<>`, idir ainm na feidhme agus liosta na bparaiméadar, mar seo:

```rust,ignore
fn largest<T>(list: &[T]) -> &T {
```

Léimid an sainmhíniú seo mar seo a leanas: tá an fheidhm `largest` cineálach thar chineál éigin
`T`. Tá paraiméadar amháin ag an bhfeidhm seo darb ainm `list`, ar sliseog luachanna é
den chineál `T`. Tabharfaidh an fheidhm `largest` tagairt ar ais do luach an
cineál céanna `T`.

Léiríonn liostú 10-5 an sainmhíniú comhcheangailte ar fheidhm `largest` ag baint úsáide as an gcineál cineálach
cineál sonraí ina shíniú. Léiríonn an liostú freisin conas is féidir linn glaoch ar an bhfeidhm
le slice de luachanna `i32` nó luachanna `char`. Tabhair faoi deara nach ndéanfaidh an cód seo
le chéile go fóill, ach déanfaimid é a shocrú níos déanaí sa chaibidil seo.

<Listing number="10-5" file-name="src/main.rs" caption="The `largest` function using generic type parameters; this doesn’t compile yet">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-05/src/main.rs}}
```

</Listing>

Má thiomsaimid an cód seo faoi láthair, gheobhaidh muid an earráid seo:

```console
{{#include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-05/output.txt}}
```

Luann an téacs cabhrach `std::cmp::PartialOrd`, atá ina _trait_, agus táimid ag
ag dul chun labhairt faoi thréithe sa chéad alt eile. Chun anois, tá a fhios go bhfuil an earráid seo
Deirtear nach n-oibreoidh an corp `largest` do gach cineál `T`
d'fhéadfadh a bheith. Toisc gur mian linn luachanna de chineál `T` sa chorp a chur i gcomparáid, is féidir linn
ná húsáid ach cineálacha ar féidir a luachanna a ordú. Chun comparáidí a chumasú, an caighdeán
Tá an tréithe `std::cmp::PartialOrd` ag an leabharlann is féidir leat a chur i bhfeidhm ar chineálacha
(féach Aguisín C le haghaidh tuilleadh ar an tréith seo). Trí na téacsanna cabhrach a leanúint
Mar mholadh, cuirimid srian leis na cineálacha atá bailí do `T` amháin dóibh siúd a chuireann i bhfeidhm
Beidh `PartialOrd` agus an sampla seo le chéile, mar gheall ar an leabharlann caighdeánach
cuireann `PartialOrd` i bhfeidhm ar `i32` agus `char` araon.

### I Sainmhínithe Struchtúr

Is féidir linn struchtúir a shainiú freisin chun paraiméadar cineál cineálach a úsáid i gceann amháin nó níos mó
réimsí ag baint úsáide as an chomhréir `<>`. Sainmhíníonn liostú 10-6 struchtúr `Point<T>` le coinneáil
Comhordaíonn `x` agus `y` luachanna de chineál ar bith.

<Listing number="10-6" file-name="src/main.rs" caption="A `Point<T>` struct that holds `x` and `y` values of type `T`">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-06/src/main.rs}}
```

</Listing>

Tá an chomhréir chun cineálacha a úsáid i sainmhínithe struchtúir cosúil leis an gceann a úsáidtear i
sainmhínithe feidhm. Ar dtús dearbhaímid ainm an pharaiméadar cineál taobh istigh
lúibíní uillinn díreach tar éis ainm an struct. Ansin úsáidimid an cineálach
clóscríobh an sainmhíniú ar struct nuair a shonróimis sonraí nithiúla ar shlí eile
cineálacha.

Tabhair faoi deara toisc nár úsáideamar ach cineál cineálach amháin chun `Point <T>` a shainiú, seo
deir an sainmhíniú go bhfuil an struchtúr `Point<T>` cineálach thar cineál éigin `T`, agus
is iad na réimsí `x` agus `y` _an dá chineál_ sin, is cuma cén cineál sin. Más rud é
cruthaímid sampla de `Point<T>` a bhfuil luachanna de chineálacha éagsúla aige, mar atá i
Ag liostú 10-7, ní thiomsóidh ár gcód.

<Listing number="10-7" file-name="src/main.rs" caption="The fields `x` and `y` must be the same type because both have the same generic data type `T`.">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-07/src/main.rs}}
```

</Listing>

Sa sampla seo, nuair a shannaimid an luach slánuimhir `5` go `x`, ligimid an
tá a fhios ag tiomsaitheoir gur slánuimhir a bheidh sa chineál cineálach `T` don chás seo de
`Point<T>`. Ansin nuair a shonraimid `4.0` le haghaidh `y`, rud a shainigh muid go mbeadh an
cineál céanna le `x`, gheobhaidh muid earráid cineál neamhréire mar seo:

```console
{{#include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-07/output.txt}}
```

Struchtúr `Point` a shainiú ina bhfuil `x` agus `y` araon cineálach ach a bhféadfadh go mbeadh
cineálacha éagsúla, is féidir linn paraiméadair ilchineálacha cineálacha a úsáid. Mar shampla, i
Ag liostú 10-8, athraíonn muid an sainmhíniú ar `Point` le bheith cineálach thar chineálacha `T`
agus `U` áit a bhfuil `x` den chineál `T` agus `y` den chineál `U`.

<Listing number="10-8" file-name="src/main.rs" caption="A `Point<T, U>` generic over two types so that `x` and `y` can be values of different types">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-08/src/main.rs}}
```

</Listing>

Anois ceadaítear na cásanna go léir de `Point` a thaispeántar! Is féidir leat an oiread cineálach a úsáid
paraiméadair cineál i sainmhíniú mar is mian leat, ach ag baint úsáide as níos mó ná cúpla a dhéanann
do chód deacair a léamh. Má aimsíonn tú go bhfuil go leor cineálacha cineálacha de dhíth ort
do chód, d'fhéadfadh sé a léiriú go bhfuil gá le do chód a athstruchtúrú go dtí níos lú
píosaí.

### I Sainmhínithe Enum

Mar a rinneamar le struchtúir, is féidir linn enums a shainiú chun cineálacha sonraí cineálacha a choinneáil ina gcuid
athraithigh. Breathnaímis ar an `Option<T>` atá sa chaighdeán
soláthairtí leabharlainne, a d’úsáideamar i gCaibidil 6:

```rust
enum Option<T> {
    Some(T),
    None,
}
```

Ba cheart go ndéanfadh an sainmhíniú seo níos mó ciall duit anois. Mar a fheiceann tú, tá an
Tá `Option<T>` enum cineálach thar an gcineál `T` agus tá dhá leagan ann: `Some`, a
tá luach amháin de chineál `T` aige, agus malairt `None` nach bhfuil luach ar bith aige.
Trí úsáid a bhaint as an `Option<T>` enum, is féidir linn coincheap teibí an
luach roghnach, agus toisc go bhfuil `Option<T>` cineálach, is féidir linn an astarraingt seo a úsáid
is cuma cén cineál an luach roghnach.

Is féidir le Enums cineálacha ilchineálacha a úsáid freisin. An sainmhíniú ar an `Result`
Is sampla amháin é an enum a d’úsáideamar i gCaibidil 9:

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

Tá an enum `Result` cineálach thar dhá chineál, `T` agus `E`, agus tá dhá leagan ann:
`Ok`, a bhfuil luach de chineál `T` aige, agus `Err`, a bhfuil luach cineáil aige
`e`. Fágann an sainmhíniú seo go bhfuil sé áisiúil an enum `Result` a úsáid áit ar bith againn
bíodh oibríocht agat a d'fhéadfadh a bheith rathúil (luach de chineál éigin `T` a thabhairt ar ais) nó a theipeann
(tabhair ar ais earráid de shaghas éigin `E`). Go deimhin, is é seo an rud a d'úsáid muid a oscailt
comhad i Liostú 9-3, áit ar líonadh `T` leis an gcineál `std::fs::File` nuair
D'éirigh leis an gcomhad a oscailt agus líonadh `E` leis an gcineál
`std::io::Error` nuair a bhí fadhbanna le hoscailt an chomhaid.

Nuair a aithníonn tú cásanna i do chód le struchtúr iolrach nó enum
sainmhínithe nach bhfuil difriúil ach amháin i gcineálacha na luachanna atá acu, is féidir leat
seachain dúbailt trí úsáid a bhaint as cineálacha cineálacha ina ionad.

### I Sainmhínithe Modh

Is féidir linn modhanna a chur i bhfeidhm maidir le struchtúir agus enums (mar a rinneamar i gCaibidil 5) agus úsáid
cineálacha cineálacha ina sainmhínithe freisin. Léiríonn liostú 10-9 an `Point<T>`
struchtúr sainmhínithe againn i Liostú 10-6 le modh darb ainm `x` curtha i bhfeidhm air.

<Listing number="10-9" file-name="src/main.rs" caption="Implementing a method named `x` on the `Point<T>` struct that will return a reference to the `x` field of type `T`">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-09/src/main.rs}}
```

</Listing>

Anseo, shainmhíomar modh darb ainm `x` ar `Point <T>` a thugann tagairt ar ais
leis na sonraí sa réimse `x`.

Tabhair faoi deara go gcaithfimid `T` a dhearbhú díreach i ndiaidh `impl` ionas gur féidir linn `T` a úsáid lena shonrú
go bhfuil modhanna ar an gcineál `Point <T>` á gcur i bhfeidhm againn. Trí `T` a dhearbhú mar a
cineál cineálach tar éis `impl`, is féidir le meirge a aithint gurb é an cineál san uillinn
Is cineál cineálach seachas cineál coincréite é lúibíní i `Point`. D'fhéadfadh muid
roghnaigh ainm eile don pharaiméadar cineálach seo ná an t-ainm cineálach
paraiméadar dearbhaithe sa sainmhíniú struct, ach ag baint úsáide as an ainm céanna é
traidisiúnta. Má scríobhann tú modh laistigh de `impl` a dhearbhaíonn cineálach
cineál, saineofar an modh sin ar aon ásc den chineál, is cuma cén
cuirtear an cineál coincréit in ionad an chineáil cineálach.

Is féidir linn srianta ar chineálacha cineálacha a shonrú freisin agus modhanna á sainiú ar an
cineál. D'fhéadfaimis, mar shampla, modhanna a chur i bhfeidhm ar chásanna `Point<f32>` amháin
seachas ar chásanna `Point<T>` le haon chineál cineálach. I Liosta 10-10 táimid
bain úsáid as an gcineál coincréite `f32`, rud a chiallaíonn nach ndearbhaímid aon chineál i ndiaidh `impl`.

<Listing number="10-10" file-name="src/main.rs" caption="An `impl` block that only applies to a struct with a particular concrete type for the generic type parameter `T`">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-10/src/main.rs:here}}
```

</Listing>

Ciallaíonn an cód seo go mbeidh `distance_from_origin` ag an gcineál `Point<f32>`
modh ; i gcásanna eile de `Point<T>` nuair nach de chineál `f32` é `T`'
an modh seo a shainiú. Tomhaiseann an modh cé chomh fada ár bpointe ó na
pointe ag comhordanáidí (0.0, 0.0) agus úsáideann oibríochtaí matamaitice atá
ar fáil do chineálacha snámhphointe amháin.

Ní bhíonn paraiméadair chineálacha i sainmhíniú struchtúir mar a chéile i gcónaí leo siúd
úsáideann tú sínithe modha an struchtúir chéanna sin. Úsáideann liostú 10-11 an cineálach
cineálacha `X1` agus `Y1` don struchtúr `Point` agus `X2` `Y2` don mhodh `mixup`
síniú chun an sampla a dhéanamh níos soiléire. Cruthaíonn an modh `Point` nua
mar shampla leis an luach `x` ón `self` `Point` (den chineál `X1`) agus an `y`
luach ón `Point` a cuireadh isteach (den chineál `Y2`).

<Listing number="10-11" file-name="src/main.rs" caption="A method that uses generic types different from its struct’s definition">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-11/src/main.rs}}
```

</Listing>

I `main`, tá `Point` sainmhínithe againn a bhfuil `i32` ann do `x` (le luach `5`)
agus `f64` le haghaidh `y` (le luach `10.4`). Is struchtúr `Point` é an athróg `p2`
a bhfuil sreangshlis le haghaidh `x` (le luach `"Hello"`) agus `char` le haghaidh `y`
(le luach `c`). Ag glaoch `mixup` ar `p1` leis an argóint `p2` tugann `p3` dúinn,
a mbeidh `i32` le haghaidh `x` mar gur tháinig `x` ó `p1`. An athróg `p3`
will have a `char` for `y` because `y` came from `p2`. An macra `println!`
priontálfaidh glao `p3.x = 5, p3.y = c`.

Is é cuspóir an sampla seo a léiriú staid ina bhfuil roinnt cineálach
dearbhaítear paraiméadair le `impl` agus dearbhaítear cuid acu leis an modh
sainmhíniú. Anseo, dearbhaítear na paraiméadair chineálacha `X1` agus `Y1` ina dhiaidh sin
`impl` mar go dtéann siad leis an sainmhíniú struct. Na paraiméadair chineálacha `X2`
agus déantar `Y2` a dhearbhú tar éis `fn mixup` toisc nach mbaineann siad ach leis an
modh.

### Feidhmíocht an Chóid ag Úsáid Generics

B'fhéidir go bhfuil tú ag smaoineamh an bhfuil costas ama rite ag baint úsáide as cineál cineálach
paraiméadair. Is é an dea-scéal ná nach ndéanfaidh úsáid cineálacha cineálacha do chlár
reáchtáil ar bith níos moille ná mar a bheadh ​​sé le cineálacha coincréite.

Cuireann meirge é seo i gcrích trí mhonamorphization an chóid a dhéanamh ag baint úsáide as
generics ag am tiomsaithe. Is é _Monomorphization_ an próiseas a bhaineann le casadh cineálach
cód isteach i gcód sonrach trí na cineálacha nithiúla a úsáidtear nuair a
tiomsaithe. Sa phróiseas seo, déanann an tiomsaitheoir a mhalairt de na céimeanna a d'úsáideamar
chun an fheidhm chineálach a chruthú i Liostú 10-5: féachann an tiomsaitheoir ar gach ceann de na
áiteanna ina dtugtar cód cineálach agus gineann cód do na cineálacha nithiúla
tugtar an cód cineálach le.

Breathnaímid ar conas a oibríonn sé seo trí úsáid a bhaint as cineálach na leabharlainne caighdeánach
`Option<T>` enum:

```rust
let integer = Some(5);
let float = Some(5.0);
```

Nuair a thiomsaíonn Rust an cód seo, déanann sé monomorphization. Le linn sin
phróiseas, léann an tiomsaitheoir na luachanna a úsáideadh i `Option<T>`
cásanna agus aithníonn sé dhá chineál `Option<T>`: is é ceann amháin `i32` agus an ceann eile
tá `f64`. Mar sin, leathnaíonn sé an sainmhíniú cineálach ar `Option<T>` ina dhá cheann
sainmhínithe ar `i32` agus `f64`, rud a chuirtear in ionad an chineálach
sainmhíniú leis na cinn ar leith.

Breathnaíonn an leagan monomorphized den chód cosúil leis an méid seo a leanas (an
Úsáideann tiomsaitheoir ainmneacha atá difriúil ó na cinn atá in úsáid againn anseo le haghaidh léiriú):

<Listing file-name="src/main.rs">

```rust
enum Option_i32 {
    Some(i32),
    None,
}

enum Option_f64 {
    Some(f64),
    None,
}

fn main() {
    let integer = Option_i32::Some(5);
    let float = Option_f64::Some(5.0);
}
```

</Listing>

Cuirtear na sainmhínithe ar leith cruthaithe ag
an tiomsaitheoir. Toisc go dtiomsaíonn Rust cód cineálach i gcód a shonraíonn an
cineál i ngach cás, ní íocaimid aon chostas ama rite as generics a úsáid. Nuair a bheidh an cód
ritheann, feidhmíonn sé díreach mar a bheadh ​​sé dá mbeadh dúbailt againn ar gach sainmhíniú
lámh. Déanann an próiseas monamorphization generics Rust thar a bheith éifeachtach
ag am rite.