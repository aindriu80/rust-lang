## Earráidí Inghnóthaithe le `Result`

Níl formhór na n-earráidí tromchúiseach go leor chun a cheangal ar an gclár stop iomlán.
Uaireanta nuair a theipeann ar fheidhm is ar chúis is féidir leat a léirmhíniú go héasca
agus freagra a thabhairt ar. Mar shampla, má dhéanann tú iarracht comhad a oscailt agus go mainneoidh an oibríocht sin
toisc nach bhfuil an comhad ann, b'fhéidir gur mhaith leat an comhad a chruthú ina ionad
an próiseas a fhoirceannadh.

Athghairm ó [“Láimhseáil Teip Féideartha le `Result`”][handle_failure]<!--
neamhaird a dhéanamh ar --> i gCaibidil 2 go bhfuil dhá shainmhíniú ar an enum `Result`
leaganacha, `Ok` agus `Err`, mar a leanas:

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

Is paraiméadair chineálacha iad na `T` agus `E`: pléifimid cineálacha níos mó
mionsonraí i gCaibidil 10. Ní mór duit fios a bheith agat anois go seasann `T`
an cineál luacha a thabharfar ar ais i gcás ratha laistigh den `Ok`
athraitheach, agus seasann `E` don chineál earráide a thabharfar ar ais in a
cás teipe laistigh den leagan `Err`. Toisc go bhfuil na cineálacha cineálacha seo ag `Result`
paraiméadair, is féidir linn an cineál `Result` agus na feidhmeanna a shainmhínítear air a úsáid
go leor cásanna éagsúla ina bhfuil an luach ratha agus luach earráide ba mhaith linn a
féadfaidh an t-aischur a bheith difriúil.

Glaoimis ar fheidhm a thugann luach `Torthaí' ar ais toisc go bhféadfadh an fheidhm
teip. I Liosta 9-3 déanaimid iarracht comhad a oscailt.

<Listing number="9-3" file-name="src/main.rs" caption="Opening a file">

```rust
{{#rustdoc_include  ../../listings/ch09-error-handling/listing-09-03/src/main.rs}}
```

</Listing>

Is é an cineál fillte ar `File::open` `Result<T, E>`. An paraiméadar cineálach `T`
comhlánaithe ag cur i bhfeidhm `File::open` le cineál an
luach ratha, `std::fs::File`, atá ina láimhseáil comhaid. An cineál `E` a úsáidtear i
Is é an luach earráide `std::io::Error`. Ciallaíonn an cineál fillte seo an glao chuig
Seans go n-éireodh le `File::open` agus go seolfar láimhseáil comhaid ar féidir linn a léamh uaidh nó
scríobh chuig. Seans go dteipfeadh ar an nglao feidhme freisin: mar shampla, seans nach mbeadh an comhad
ann, nó seans nach bhfuil cead againn an comhad a rochtain. An `File::open`
ní mór go mbeadh bealach ag feidhm a insint dúinn cé acu ar éirigh leis nó ar theip air agus ag
an t-am céanna a thabhairt dúinn ceachtar an láimhseáil comhad nó faisnéis earráid. seo
Is é an fhaisnéis go díreach a thugann an `Result` enum in iúl.

Sa chás go n-éiríonn le `File::open`, an luach san athróg
Beidh `greeting_file_result` ina shampla de `Ok` ina bhfuil láimhseáil comhaid.
Sa chás go dteipeann air, beidh an luach in `greeting_file_result` mar luach
instance of `Err` ina bhfuil tuilleadh eolais faoin gcineál earráide a
tharla.

Ní mór dúinn cur leis an gcód i Liostú 9-3 chun gníomhartha éagsúla a dhéanamh ag brath
ar an luach tuairisceáin `File::open`. Léiríonn liostú 9-4 bealach amháin chun an
`Result` ag baint úsáide as uirlis bhunúsach, an abairt `match` a phléamar ann
Caibidil 6 .

<Listing number="9-4" file-name="src/main.rs" caption="Using a `match` expression to handle the `Result` variants that might be returned">

```rust,should_panic
{{#rustdoc_include ../../listings/ch09-error-handling/listing-09-04/src/main.rs}}
```

</Listing>

Tabhair faoi deara, cosúil leis an enum `Option`, go raibh an `Result` enum agus a leagan
tugtha isteach sa scóip ag an réamhrá, mar sin ní gá dúinn `Result::` a shonrú
roimh na leaganacha `Ok` agus `Err` sna hairm `match`.

Nuair a bhíonn an toradh `Ok`, seolfaidh an cód seo an luach `file` istigh as
an leagan `Ok`, agus ansin sannaimid an luach láimhseála comhaid sin don athróg
`greeting_file`. Tar éis an `match`, is féidir linn an láimhseáil comhaid a úsáid le haghaidh léamh nó
ag scríobh.

Láimhseálann an lámh eile den `match` an cás óna bhfaighimid luach `Err` uaidh
`File::open`. Sa sampla seo, roghnaigh muid an macra `panic!` a ghlaoch. Más rud é
níl aon chomhad darb ainm _hello.txt_ inár n-eolaire reatha agus ritheann muid é seo
cód, feicfimid an t-aschur seo a leanas ón macra `panic!`:

```console
{{#include ../../listings/ch09-error-handling/listing-09-04/output.txt}}
```

Mar is gnách, cuireann an t-aschur seo in iúl dúinn go díreach cad a chuaigh mícheart.

### Ag Meaitseáil ar Earráidí Difriúla

Beidh `panic!` sa chód i Liostú 9-4 is cuma cén fáth ar theip ar `File::open`.
Mar sin féin, ba mhaith linn gníomhartha éagsúla a dhéanamh ar chúiseanna teipe éagsúla. Más rud é
Theip ar `Comhad::open` toisc nach bhfuil an comhad ann, ba mhaith linn an comhad a chruthú
agus cuir an láimhseáil ar ais chuig an gcomhad nua. Má theip ar `File::open` d'aon cheann eile
cúis - mar shampla, toisc nach raibh cead againn an comhad a oscailt - táimid fós
Ba mhaith liom an cód a `panic!` ar an mbealach céanna a rinne sé i Liosta 9-4. Chun seo, táimid
cuir slonn `match` istigh leis, a thaispeántar i Liostú 9-5.

<Listing number="9-5" file-name="src/main.rs" caption="Handling different kinds of errors in different ways">

<!-- ignore this test because otherwise it creates hello.txt which causes other
tests to fail lol -->

```rust,ignore
{{#rustdoc_include ../../listings/ch09-error-handling/listing-09-05/src/main.rs}}
```

</Listing>

Is é an cineál luacha a fhilleann `File::open` taobh istigh den leagan `Err`
`io::Error`, ar struchtúr é a sholáthraíonn an leabharlann chaighdeánach. An struchtúr seo
tá modh `kind` aige ar féidir linn glaoch air chun luach `io::ErrorKind` a fháil. An enum
Soláthraíonn an leabharlann chaighdeánach `io::ErrorKind` agus tá leaganacha eile ann
ag léiriú na gcineálacha éagsúla earráidí a d'fhéadfadh teacht as `io`
oibríocht. Is é an leagan is mian linn a úsáid ná `ErrorKind::NotFound`, a thugann le fios
níl an comhad atáimid ag iarraidh a oscailt ann fós. Mar sin táimid ag meaitseáil ar
`greeting_file_result`, ach tá meaitseáil istigh againn freisin ar `error.kind()`.

Is é an coinníoll ba mhaith linn a sheiceáil sa chluiche inmheánach ná an bhfuil an luach ar ais
le `error.kind()` an leagan `NotFound` den enum `ErrorKind`. Má tá,
déanaimid iarracht an comhad a chruthú le `File::create`. Mar sin féin, mar gheall ar `File::create`
d'fhéadfadh teip freisin, ní mór dúinn an dara lámh sa abairt `match` istigh. Nuair a bheidh an
ní féidir an comhad a chruthú, priontáiltear teachtaireacht earráide eile. An dara lámh de
fanann an `match` seachtrach mar an gcéanna, mar sin scaoll an chláir ar aon earráid seachas
an earráid chomhaid atá ar iarraidh.

> #### Roghanna eile seachas `match` a úsáid le `Result<T, E>`
>
> Sin go leor `match`! Tá an abairt `match` an-úsáideach ach an-úsáideach freisin
> i bhfad primitive. I gCaibidil 13, foghlaimeoidh tú faoi dhúnadh, a úsáidtear
> le go leor de na modhanna atá sainmhínithe ar `Result<T, E>`. Is féidir na modhanna seo a bheith níos mó
> gonta ná `match` a úsáid agus luachanna `Result<T, E>` i do chód á láimhseáil.
>
> Mar shampla, seo bealach eile chun an loighic chéanna a scríobh mar a léirítear i Liostú
> 9-5, an uair seo ag baint úsáide as dúnta agus an modh `unwrap_or_else`:
>
> <!-- NÍ FÉIDIR Sliocht FÉACH https://github.com/rust-lang/mdBook/issues/1127 -->
>
> ```rust,ignore
> use std::fs::File;
> use std::io::ErrorKind;
>
> fn main() {
>     let greeting_file = File::open("hello.txt").unwrap_or_else(|error| {
>         if error.kind() == ErrorKind::NotFound {
>             File::create("hello.txt").unwrap_or_else(|error| {
>                 panic!("Problem creating the file: {error:?}");
>             })
>         } else {
>             panic!("Problem opening the file: {error:?}");
>         }
>     });
> }
> ```
>
> Cé go bhfuil an t-iompar céanna ag an gcód seo agus atá i Liostú 9-5, níl sé ann
> aon nathanna `match` atá níos glaine le léamh. Tar ar ais chuig an sampla seo
> tar éis duit Caibidil 13 a léamh, agus breathnaigh ar an modh `unwrap_or_else` sa
> doiciméid chaighdeánacha leabharlainne. Is féidir le go leor níos mó de na modhanna seo a ghlanadh ollmhór
> neadaigh na habairtí `match` agus tú ag déileáil le hearráidí.

#### Aicearraí le haghaidh Scaoill ar Earráid: `unwrap` agus `expect`

Oibríonn baint úsáide as `match` go maith go leor, ach féadann sé a bheith beagán briathartha agus ní bhíonn sé i gcónaí
rún a chur in iúl go maith. Tá go leor modhanna cúntóra ag an gcineál `Result<T, E>`
sainithe air chun tascanna éagsúla, níos sainiúla a dhéanamh. Is é an modh `unwrap` a
modh aicearra curtha i bhfeidhm díreach cosúil leis an slonn `match` a scríobh muid ann
Liostáil 9-4. Más é an luach `Result` an leagan `Ok`', fillfidh `unwrap`
an luach taobh istigh den `Ok`. Más é an `Result` an leagan `Err`, déanfaidh `unwrap`
cuir glaoch ar an macra `panic!` dúinn. Seo sampla de `unwrap` i ngníomh:

<Listing file-name="src/main.rs">

```rust,should_panic
{{#rustdoc_include ../../listings/ch09-error-handling/no-listing-04-unwrap/src/main.rs}}
```

</Listing>

Má rithimid an cód seo gan comhad _hello.txt_, feicfidh muid teachtaireacht earráide uaidh
an glao `panic!` a dhéanann an modh `unwrap`:

<!-- manual-regeneration
cd listings/ch09-error-handling/no-listing-04-unwrap
cargo run
copy and paste relevant text
-->

```text
thread 'main' panicked at src/main.rs:4:49:
called `Result::unwrap()` on an `Err` value: Os { code: 2, kind: NotFound, message: "No such file or directory" }
```

Mar an gcéanna, ligeann an modh `expect` dúinn an teachtaireacht earráide `panic!` a roghnú freisin.
Is féidir úsáid a bhaint as `expect` in ionad `unwrap`' agus ag soláthar teachtaireachtaí earráide maithe
do rún agus a dhéanamh rianú síos an fhoinse scaoll níos éasca. Comhréir na
Breathnaíonn `expect` mar seo:

<Listing file-name="src/main.rs">

```rust,should_panic
{{#rustdoc_include ../../listings/ch09-error-handling/no-listing-05-expect/src/main.rs}}
```

</Listing>

Bainimid úsáid as `expect` ar an mbealach céanna le `unwrap`: chun láimhseáil an chomhaid nó glao a chur ar ais
an macra `panic!`. An teachtaireacht earráide a úsáideann `expect` ina ghlao ar `panic!`
an paraiméadar a thabharfaimid ar aghaidh chuig `expect`, seachas an réamhshocrú
teachtaireacht `panic!` a úsáideann `unwrap`. Seo an chuma atá air:

<!-- manual-regeneration
cd listings/ch09-error-handling/no-listing-05-expect
cargo run
copy and paste relevant text
-->

```text
thread 'main' panicked at src/main.rs:5:10:
hello.txt should be included in this project: Os { code: 2, kind: NotFound, message: "No such file or directory" }
```

I gcód cáilíochta táirgthe, roghnaíonn an chuid is mó de na Rustaceans `expect` seachas
`unwrap` agus tabhair comhthéacs níos mó faoi na fáthanna a bhfuiltear ag súil go mbeidh an oibríocht i gcónaí
éirigh. Ar an mbealach sin, má chruthaítear go bhfuil do chuid boinn tuisceana mícheart riamh, tá níos mó agat
faisnéis le húsáid le linn dífhabhtaithe.

### Earráidí Iomadaithe

Nuair a ghlaonn feidhmiú feidhme rud éigin a d’fhéadfadh teip, ina ionad
láimhseáil an earráid laistigh den fheidhm féin is féidir leat an earráid ar ais chuig an
cód glaonna ionas gur féidir leis cinneadh a dhéanamh ar cad atá le déanamh. Tugtar _iomadú_ air seo
an earráid agus tugann sé níos mó smachta ar an gcód glaonna, áit a bhféadfadh níos mó a bheith ann
faisnéis nó loighic a ordaíonn conas ba chóir an earráid a láimhseáil ná cad
atá ar fáil duit i gcomhthéacs do chód.

Mar shampla, taispeánann Liostú 9-6 feidhm a léann ainm úsáideora ó chomhad. Más rud é
níl an comhad ann nó ní féidir é a léamh, cuirfidh an fheidhm seo na hearráidí sin ar ais
chuig an gcód ar a dtugtar an fheidhm.

<Listing number="9-6" file-name="src/main.rs" caption="A function that returns errors to the calling code using `match`">

<!-- Deliberately not using rustdoc_include here; the `main` function in the
file panics. We do want to include it for reader experimentation purposes, but
don't want to include it for rustdoc testing purposes. -->

```rust
{{#include ../../listings/ch09-error-handling/listing-09-06/src/main.rs:here}}
```

</Listing>

Is féidir an fheidhm seo a scríobh ar bhealach i bhfad níos giorra, ach táimid chun tosú ag
go leor de a dhéanamh de láimh chun láimhseáil earráidí a iniúchadh; ag deireadh,
taispeánfaimid an bealach is giorra. Breathnaímid ar an gcineál aischuir den fheidhm
ar dtús: `Result<String, io::Error>`. Ciallaíonn sé seo go bhfuil an fheidhm ag filleadh a
luach an chineáil `Result<T, E>`, áit a bhfuil an paraiméadar cineálach `T` curtha
líonadh isteach leis an gcineál coincréite `String` agus an cineál cineálach `E` curtha
líonadh isteach leis an gcineál coincréite `io::Error`.

Má éiríonn leis an bhfeidhm seo gan aon fhadhbanna, is é an cód a ghlaonn seo
gheobhaidh an fheidhm luach `Ok` a shealbhaíonn `String` - an `username` sin
léigh an fheidhm seo ón gcomhad. Má bhíonn aon fhadhbanna ag an bhfeidhm seo, beidh an
gheobhaidh cód glaonna luach `Err` a bhfuil sampla de `io::Error` ann
go bhfuil tuilleadh eolais faoi cad a bhí ar na fadhbanna. Roghnaigh muid
`io::Error` mar chineál tuairisceáin na feidhme seo toisc go dtarlaíonn sé gurb é sin an
cineál an luach earráide a fuarthas ar ais ón dá oibríocht a bhfuilimid ag glaoch isteach
corp na feidhme seo a d’fhéadfadh a theipeann: an fheidhm `File::open` agus an
modh `read_to_string`.

Tosaíonn corp na feidhme trí ghlao a chur ar an bhfeidhm `File::open`. Ansin muid
láimhseáil an luach `Result` le `match` cosúil leis an `match` i Liostú 9-4.
Má éiríonn le `File::open`, láimhseáil an chomhaid san athróg patrún `file`
thiocfaidh chun bheith ina luach san athróg mutable `username_file` agus an fheidhm
leanann. Sa chás `Err`, in ionad `panic!` a ghlaoch, úsáidimid an `return`
eochairfhocal a thabhairt ar ais go luath amach as an fheidhm go hiomlán agus pas a fháil sa luach earráide
ó `File::open`, anois san athróg patrún `e`, ar ais go dtí an cód glaonna mar
luach earráide na feidhme seo.

Mar sin, má tá láimhseáil comhaid againn in `username_file`, cruthaíonn an fheidhm ansin a
nua `String` in athróg `username` agus cuireann sé an modh `read_to_string` ar siúl
láimhseáil an chomhaid in `username_file` chun ábhar an chomhaid a léamh isteach
`username`. Tugann an modh `read_to_string` `Result` ar ais freisin mar gheall air
b'fhéidir go dteipfeadh, cé gur éirigh le `File::open`. Mar sin teastaíonn `comait` eile uainn
láimhseáil an `Result` sin: má éiríonn le `read_to_string`, ansin tá an fheidhm atá againn
éirigh leis, agus cuirimid an t-ainm úsáideora ar ais ón gcomhad atá in `username` anois
fillte i `Ok`. Má theipeann ar `read_to_string`, cuirimid ar ais an luach earráide sa
ar an mbealach céanna a thugamar ar ais an luach earráide sa `match` a láimhseáil an
luach aischuir `File::open`. Mar sin féin, ní gá dúinn a rá go soiléir
`return`, mar is é seo an slonn deiridh san fheidhm.

Ansin láimhseálfaidh an cód a ghlaonn an cód seo luach `Ok` a fháil
ina bhfuil ainm úsáideora nó luach `Err` ina bhfuil `io::Error`. Tá sé
suas go dtí an cód glaonna chun cinneadh a dhéanamh cad ba cheart a dhéanamh leis na luachanna sin. Má tá an glaoch
Faigheann cód luach `Err`, d'fhéadfadh sé `panic!` a ghlaoch agus an clár a thuairteáil, bain úsáid as a
ainm úsáideora réamhshocraithe, nó féach ar an ainm úsáideora ó áit éigin eile seachas comhad, le haghaidh
shampla. Níl go leor faisnéise againn maidir le cad é an cód glaonna i ndáiríre
ag iarraidh a dhéanamh, mar sin táimid ag iomadú gach eolas faoi rath nó earráid aníos le haghaidh
é a láimhseáil go cuí.

Tá patrún seo na n-earráidí iomadaithe chomh coitianta i Rust go soláthraíonn Rust an
oibreoir comhartha ceiste `?` chun é seo a dhéanamh níos éasca.

#### Aicearra le haghaidh Earráidí Iomadaithe: an t-oibreoir `?`

Léiríonn liostú 9-7 cur i bhfeidhm `read_username_from_file` a bhfuil an
feidhmiúlacht chéanna agus atá i Liostú 9-6, ach úsáideann an cur i bhfeidhm seo an `?`
oibreoir.

<Listing number="9-7" file-name="src/main.rs" caption="A function that returns errors to the calling code using the `?` operator">

<!-- Deliberately not using rustdoc_include here; the `main` function in the
file panics. We do want to include it for reader experimentation purposes, but
don't want to include it for rustdoc testing purposes. -->

```rust
{{#include  ../../listings/ch09-error-handling/listing-09-07/src/main.rs:here}}
```

</Listing>

Sainmhínítear an `?` a chuirtear i ndiaidh luach `Result` chun oibriú ar an mbealach céanna beagnach
mar na habairtí `match` a shainmhíomar chun na luachanna `Result` sa Liostú a láimhseáil
9-6. Más `OK` luach an `Result`, déanfaidh an luach taobh istigh den `Ok`
faigh ar ais ón slonn seo, agus leanfaidh an clár ar aghaidh. Má tá an luach
is an `Err`, cuirfear an `Err` ar ais ón bhfeidhm iomlán amhail is dá mbeadh
d'úsáid an eochairfhocal `return` ionas go n-aistrítear luach na hearráide chuig an nglao
cód.

Tá difríocht idir cad a dhéanann an slonn `match` ó Liosta 9-6
agus cad a dhéanann an t-oibreoir `?`: luachanna earráide ar a dtugtar an t-oibreoir `?`
orthu dul tríd an bhfeidhm `ó`, sainmhínithe sa `Ó` trait sa
leabharlann caighdeánach, a úsáidtear chun luachanna a thiontú ó chineál amháin go cineál eile.
Nuair a ghlaonn an t-oibreoir `?` ar an bhfeidhm `ó`, is é an cineál earráide a fhaightear
thiontú go cineál earráide atá sainithe i gcineál tuairisceáin an tsrutha
feidhm. Tá sé seo úsáideach nuair a fhilleann feidhm cineál earráide amháin chun a léiriú
na bealaí ar fad a d'fhéadfadh feidhm a theipeann, fiú dá dteipfeadh ar pháirteanna do go leor cineálacha éagsúla
cúiseanna.

Mar shampla, d'fhéadfaimis an fheidhm `read_username_from_file` a athrú i Liostú
9-7 chun cineál earráide saincheaptha darb ainm `OurError` a shainímid a thabhairt ar ais. Má táimid freisin
sainmhínigh `impl From<io::Error> for OurError` chun sampla de
`OurError` ó `io::Error`, ansin glaonna an t-oibreoir `?` i gcorp na
Cuirfidh `read_username_from_file` glaoch ar `ó` agus tiontóidh sé na cineálacha earráide gan
gá cód ar bith eile a chur leis an bhfeidhm.

I gcomhthéacs Liostú 9-7, beidh an `?` ag deireadh an ghlao `File::open`
cuir an luach taobh istigh de `OK` ar ais chuig an athróg `username_file`. Más earráid
tharlaíonn, beidh an t-oibreoir `?` ar ais go luath as an fheidhm iomlán agus a thabhairt
aon luach 'Earráid' leis an gcód glaonna. Baineann an rud céanna leis an `?` ag an
deireadh an ghlao `read_to_string`.

Cuireann an t-oibreoir `?` deireadh le go leor pláta coire agus déanann sé an fheidhm seo
cur i bhfeidhm níos simplí. D'fhéadfaimis an cód seo a ghiorrú níos faide fiú trí shlabhraiú
glaonna modh díreach tar éis an `?`, mar a thaispeántar i Liosta 9-8.

<Listing number="9-8" file-name="src/main.rs" caption="Chaining method calls after the `?` operator">

<!-- Deliberately not using rustdoc_include here; the `main` function in the
file panics. We do want to include it for reader experimentation purposes, but
don't want to include it for rustdoc testing purposes. -->

```rust
{{#include ../../listings/ch09-error-handling/listing-09-08/src/main.rs:here}}
```

</Listing>

Táimid tar éis cruthú na `String` nua in `username` a bhogadh go dtí tús na
an fheidhm; níl aon athrú ar an gcuid sin. In ionad athróg a chruthú
`username_file`, shlabhraíomar an glao go `read_to_string` díreach ar an
toradh `Comhad::open("hello.txt")?`. Tá `?` fós againn ag deireadh an
glao `read_to_string`, agus tugaimid ar ais fós luach `OK` ina bhfuil `username`
nuair a éiríonn leis an dá `File::open` agus `read_to_string` seachas filleadh
earráidí. Tá an fheidhmiúlacht mar an gcéanna arís agus atá i Liostú 9-6 agus Liostú 9-7;
níl anseo ach bealach difriúil, níos eirgeanamaíochta chun é a scríobh.

Léiríonn liostú 9-9 bealach chun é seo a dhéanamh níos giorra fós trí úsáid a bhaint as `fs::read_to_string`.

<Listing number="9-9" file-name="src/main.rs" caption="Using `fs::read_to_string` instead of opening and then reading the file">

<!-- Deliberately not using rustdoc_include here; the `main` function in the
file panics. We do want to include it for reader experimentation purposes, but
don't want to include it for rustdoc testing purposes. -->

```rust
{{#include ../../listings/ch09-error-handling/listing-09-09/src/main.rs:here}}
```

</Listing>

Is oibríocht choitianta go leor é comhad a léamh ina teaghrán, mar sin an caighdeán
soláthraíonn an leabharlann an fheidhm áisiúil `fs::read_to_string` a osclaíonn an
comhad, cruthaíonn sé `String` nua, léann inneachar an chomhaid, cuireann sé an t-ábhar
isteach sa `String` sin, agus ar ais é. Ar ndóigh, ag baint úsáide as `fs::read_to_string`
Ní thugann sé seo an deis dúinn an láimhseáil earráide go léir a mhíniú, mar sin rinneamar é
an bealach is faide ar dtús.

#### An Áit ar féidir an tOibreoir `?` a Úsáid

Ní féidir an t-oibreoir `?` a úsáid ach amháin i bhfeidhmeanna a bhfuil a gcineál fillte comhoiriúnach
leis an luach a úsáidtear an `?` ar. Tá sé seo toisc go bhfuil an t-oibreoir `?` sainmhínithe
chun luach a chur ar ais go luath as an bhfeidhm, ar an mbealach céanna
mar an slonn `match` a shainmhíníomar i Liostú 9-6. I Liosta 9-6, tá an
Bhí `match` ag baint úsáide as luach `Result`, agus thug an lámh fillte luath ar ais an
luach `Err(e)`. Caithfidh `Result` a bheith i gcineál aischuir na feidhme ionas go mbeidh
tá sé ag luí leis an `return` seo.

I Liostú 9-10, breathnaímid ar an earráid a gheobhaidh muid má úsáidimid an t-oibreoir `?`
i bhfeidhm `main` le cineál tuairisceáin nach luíonn leis an gcineál
an luach a úsáidimid `?` ar.

<Listing number="9-10" file-name="src/main.rs" caption="Attempting to use the `?` in the `main` function that returns `()` won’t compile.">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch09-error-handling/listing-09-10/src/main.rs}}
```

</Listing>

Osclaíonn an cód seo comhad, rud a d'fhéadfadh teip. Leanann an t-oibreoir `?` an `Result`
luach ar ais le `File::open`, ach tá an cineál tuairisceáin ag an bpríomhfheidhm seo
`()`, ní `Result`. Nuair a dhéanaimid an cód seo a thiomsú, faigheann muid an earráid seo a leanas
teachtaireacht:

```console
{{#include ../../listings/ch09-error-handling/listing-09-10/output.txt}}
```

Léiríonn an earráid seo nach bhfuil cead againn ach an t-oibreoir `?` a úsáid in a
feidhm a fhilleann `Result`, `Option`, nó cineál eile a chuireann i bhfeidhm
`FromResidual`.

Chun an earráid a shocrú, tá dhá rogha agat. Rogha amháin is ea an cineál tuairisceáin a athrú
d’fheidhm a bheith comhoiriúnach leis an luach atá á úsáid agat as an oibreoir `?`
ar chomh fada agus nach bhfuil aon srianta agat chun é sin a chosc. Is é an rogha eile a
bain úsáid as `match` nó ceann de na modhanna `Result<T, E>` chun `Result<T, E>` a láimhseáil
pé slí is cuí.

Luaigh an teachtaireacht earráide freisin gur féidir `?` a úsáid le luachanna `Option<T>`
chomh maith. Mar is amhlaidh le húsáid `?` ar `Result`, ní féidir leat ach `?` a úsáid ar `Option` in a
feidhm a thugann `Option` ar ais. Iompar an oibreora `?` nuair a ghlaoitear air
ar `Option<T>` atá cosúil lena hiompraíocht nuair a ghlaoitear air ar `Result<T, E>`:
más é an luach `None`, cuirfear an `None` ar ais go luath ón bhfeidhm ag
an pointe sin. Más `Some` an luach, is é an luach taobh istigh den `Some` an
luach iarmhartach an slonn, agus leanann an fheidhm. Ag liostú 9-11 tá
sampla d’fheidhm a aimsíonn carachtar deiridh na chéad líne sa
téacs tugtha.

<Listing number="9-11" caption="Using the `?` operator on an `Option<T>` value">

```rust
{{#rustdoc_include ../../listings/ch09-error-handling/listing-09-11/src/main.rs:here}}
```

</Listing>

Filleann an fheidhm seo `Option <char>` toisc go bhfuil seans ann go bhfuil
carachtar ann, ach is féidir freisin nach bhfuil. Glacann an cód seo an
argóint slisnithe teaghrán `text` agus glaoitear an modh `lines` air, a fhilleann
iterator thar na línte sa téad. Toisc gur mian leis an fheidhm seo
scrúdaigh an chéad líne, glaonn sé `next` ar an atrialltóir chun an chéad luach a fháil
ón iterator. Más é `text` an teaghrán folamh, déanfaidh an glao seo go `next`
tabhair `None` ar ais, agus sa chás sin úsáidimid `?` chun `None` a stopadh agus a thabhairt ar ais ó
`last_char_of_first_line`. Murab é `text` an teaghrán folamh, déanfaidh `next`
cuir ar ais luach `Some` ina bhfuil sreangán den chéad líne i `text`.

Sliocht an `?` an téad sliseog, agus is féidir linn `chars` a ghlaoch ar an téadshlis sin
chun iterator a fháil ar a charachtair. Tá suim againn sa charachtar deireanach i
an chéad líne seo, mar sin tugaimid `last` chun an mhír dheiridh san atrialltóir a thabhairt ar ais.
Is `Option` é seo mar is féidir gur folamh an chéad líne
téad ; mar shampla, má thosaíonn `text` le líne bhán ach go bhfuil carachtair air
línte eile, mar atá in `"\nhi"`. Mar sin féin, má tá carachtar deireanach ar an gcéad
líne, cuirfear ar ais é sa leagan `Some`. An t-oibreoir `?` sa lár
tugann sé bealach gonta dúinn leis an loighic seo a chur in iúl, rud a ligeann dúinn cur i bhfeidhm an
feidhm i líne amháin. Mura bhféadfaimis an t-oibreoir `?` a úsáid ar `Option`, bheimis
caithfidh siad an loighic seo a chur i bhfeidhm ag baint úsáide as tuilleadh glaonna modha nó slonn `match`.

Tabhair faoi deara gur féidir leat an t-oibreoir `?` a úsáid ar `Result` in fheidhm a fhilleann
`Result`, agus is féidir leat an t-oibreoir `?` a úsáid ar `Option` san fheidhm a
Filleann sé `Option`, ach ní féidir leat a mheascadh agus a mheaitseáil. Ní dhéanfaidh an t-oibreoir `?`
tiontaigh `Result` go huathoibríoch go `Option` nó vice versa; sna cásanna sin,
is féidir leat modhanna a úsáid mar an modh `ok` ar `Result` nó an modh `ok_or` ar
`Option` chun an comhshó a dhéanamh go sainráite.

Go dtí seo, filleann na `main` ar fad a d'úsáideamar `()`. Is í an fheidhm `main`
speisialta toisc gurb é pointe iontrála agus pointe scoir ríomhchláir inrite é,
agus tá srianta ar an gcineál tuairisceáin is féidir a bheith ag an gclár
iompar mar a bheifí ag súil leis.

Ar ámharaí an tsaoil, is féidir le `main` `Result<(), E>` a thabhairt ar ais freisin. Tá an cód ag liostú 9-12
ó Liostú 9-10, ach d'athraigh muid an cineál fillte `main` le bheith
`Result<(), Box<dyn Error>>` agus chuir sé luach fillte `Ok(())` leis go dtí an deireadh. seo
tiomsófar an cód anois.

<Listing number="9-12" file-name="src/main.rs" caption="Changing `main` to return `Result<(), E>` allows the use of the `?` operator on `Result` values.">

```rust,ignore
{{#rustdoc_include ../../listings/ch09-error-handling/listing-09-12/src/main.rs}}
```

</Listing>

Is é an cineál `Box<dyn Error>` ná _trait object_, a labhróimid faoi sa
[“Ag baint úsáide as Réada Trait a Ligeann Luachanna Éagsúla
Cineálacha”][trait-objects]<!-- neamhaird a dhéanamh ar --> alt i gCaibidil 18. Faoi láthair, is féidir leat
léigh `Box<dyn Error>` a chiallaíonn "earráid de chineál ar bith." Ag baint úsáide as `?` ar `Result`
luach i bhfeidhm `main` leis an gcineál earráide `Box<dyn Error>` ceadaithe
toisc go gceadaíonn sé aon luach `Err` a thabhairt ar ais go luath. Cé go bhfuil an comhlacht ar
ní thabharfaidh an `main` seo ar ais ach earráidí den chineál `std::io::Error`, le
ag sonrú `Box<dyn Error>`, leanfaidh an síniú seo de bheith ceart fiú má
cuirtear tuilleadh cód a thugann earráidí eile ar ais le corp na `main`.

Nuair a fhilleann feidhm `main` `Result<(), E>`, scoirfidh an inrite le
luach `0` má fhilleann `main``Ok(())` agus scoirfidh sé le luach neamhzero má
Tugann `main` luach `Err` ar ais. Inrite atá scríofa i slánuimhreacha tuairisceáin C nuair
scoireann siad: cuireann cláir a scoir an slánuimhir `0` ar ais go rathúil, agus cláir
an earráid sin cuir slánuimhir éigin ar ais seachas `0`. Tugann Rust ar ais slánuimhreacha ó
inrite a bheith ag luí leis an gcoinbhinsiún seo.

Féadfaidh an `main` aon chineálacha a chuireann i bhfeidhm [an
`std::process::Termination` trait][termination] <!-- neamhaird -->, ina bhfuil
feidhm `report` a thugann `ExitCode` ar ais. Téigh i gcomhairle leis an leabharlann chaighdeánach
doiciméadú le haghaidh tuilleadh eolais ar chur i bhfeidhm na tréithe `Termination` le haghaidh
do chineálacha féin.

Anois go bhfuil na sonraí pléite againn maidir le ‘scaoll!’ a ghlaoch nó ‘Toradh’ a sheoladh ar ais,
filleadh ar an topaic maidir le conas a chinneadh cé acu is cuí a úsáid ina
cásanna.

[handle_failure]: ch02-00-guessing-game-tutorial.html#handling-potential-failure-with-result
[trait-objects]: ch18-02-trait-objects.html#using-trait-objects-that-allow-for-values-of-different-types
[termination]: ../std/process/trait.Termination.html

