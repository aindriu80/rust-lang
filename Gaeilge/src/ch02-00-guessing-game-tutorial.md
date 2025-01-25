# Cluiche Tomhais a Ríomhchlárú

Léimid isteach i Rust trí thionscadal praiticiúil a oibriú le chéile! seo
Tugann caibidil cúpla coincheap Rust coitianta duit trína thaispeáint duit conas é a úsáid
iad i gclár fíor. Foghlaimeoidh tú faoi `let`, `match`, modhanna, gaolmhar
feidhmeanna, cliathbhoscaí seachtracha, agus go leor eile! Sna caibidlí seo a leanas, déanfaimid iniúchadh
na smaointe seo níos mine. Sa chaibidil seo, ní dhéanfaidh tú ach cleachtadh ar an
bunúsacha.

Cuirfimid fadhb ríomhchláraithe clasaiceach do thosaitheoirí i bhfeidhm: cluiche tomhais. Seo chugaibh
conas a oibríonn sé: ginfidh an clár slánuimhir randamach idir 1 agus 100. It
spreagfaidh an t-imreoir ansin buille faoi thuairim a thabhairt. Tar éis buille faoi thuairim a iontráil, cuirtear an
léireoidh an clár an bhfuil an buille faoi thuairim ró-íseal nó ró-ard. Má tá an buille faoi thuairim
ceart, beidh an cluiche a phriontáil teachtaireacht comhghairdeas agus scoir.

## Tionscadal Nua a Bhunú

Chun tionscadal nua a shocrú, téigh chuig an eolaire _projects_ a chruthaigh tú ann
Caibidil 1 agus déan tionscadal nua ag baint úsáide as Cargo, mar a leanas:

```console
$ cargo new guessing_game
$ cd guessing_game
```

Glacann an chéad ordú, `cargo new`, ainm an tionscadail (`guessing_game`)
mar an chéad argóint. Athraíonn an dara ordú go dtí na tionscadail nua
eolaire.

Féach ar an gcomhad _Cargo.toml_ ginte:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial
rm -rf no-listing-01-cargo-new
cargo new no-listing-01-cargo-new --name guessing_game
cd no-listing-01-cargo-new
cargo run > output.txt 2>&1
cd ../../..
-->

<span class="filename">Ainm comhaid: Cargo.toml</span>

```toml
{{#include ../../listings/ch02-guessing-game-tutorial/no-listing-01-cargo-new/Cargo.toml}}
```

Mar a chonaic tú i gCaibidil 1, gineann `cargo new` "Dia duit, domhan!" clár le haghaidh
leat. Seiceáil an comhad _src/main.rs_:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/no-listing-01-cargo-new/src/main.rs}}
```

Anois déanaimis an "Dia duit, a domhan!" clár agus é a reáchtáil sa chéim chéanna
ag baint úsáide as an ordú `cargo run`:

```console
{{#include ../../listings/ch02-guessing-game-tutorial/no-listing-01-cargo-new/output.txt}}
```

Bíonn an t-ordú `run` áisiúil nuair is gá duit athrá tapa a dhéanamh ar thionscadal,
mar a dhéanfaimid sa chluiche seo, tástáil tapa a dhéanamh ar gach atriall roimh bogadh ar aghaidh go dtí
an tarna ceann.

Athoscail an comhad _src/main.rs_. Beidh an cód ar fad á scríobh agat sa chomhad seo.

## Buille faoi thuairim a phróiseáil

Iarrfaidh an chéad chuid den chlár cluiche buille faoi thuairim ionchur úsáideora, próiseas
an t-ionchur sin, agus seiceáil go bhfuil an t-ionchur san fhoirm a bhfuiltear ag súil léi. Chun tús a chur, déanfaimid
lig don imreoir buille faoi thuairim a ionchur. Cuir isteach an cód i Liostú 2-1 isteach
_src/main.rs_.

<Listing number="2-1" file-name="src/main.rs" caption="Cód a fhaigheann buille faoi thuairim ón úsáideoir agus a phrionnaíonn sé">

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:all}}
```

</Listing>

Tá go leor faisnéise sa chód seo, mar sin déanaimis dul thairis air líne ar líne. Chuig
ionchur úsáideora a fháil agus ansin an toradh a phriontáil mar aschur, ní mór dúinn an
leabharlann ionchuir/aschuir `io` isteach sa scóip. Tagann an leabharlann `io` ón gcaighdeán
leabharlann, ar a dtugtar `std`:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:io}}
```

De réir réamhshocraithe, tá sraith míreanna sainithe ag Rust sa leabharlann chaighdeánach atá aige
a thugann isteach raon feidhme gach cláir. Tugtar an _prelude_ ar an tacar seo, agus
is féidir leat gach rud atá ann a fheiceáil [i gcáipéisíocht chaighdeánach na leabharlainne][prelude].

Mura bhfuil cineál is mian leat a úsáid sa réamhrá, caithfidh tú an cineál sin a thabhairt leat
isteach sa raon feidhme go sainráite le ráiteas `use`. Ag baint úsáide as an leabharlann `std::io`
ar fáil duit le roinnt gnéithe úsáideacha, lena n-áirítear an cumas chun glacadh leis
ionchur úsáideora.

Mar a chonaic tú i gCaibidil 1, is é an fheidhm `main` an pointe iontrála isteach sa
clár:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:main}}
```

Dearbhaíonn an chomhréir `fn` feidhm nua; na lúibíní, `()`, cuir in iúl ann
nach bhfuil aon pharaiméadair; agus cuireann an lúibín chatach, `{`, tús le corp na feidhme.

Mar a d'fhoghlaim tú i gCaibidil 1 freisin, is macra é `println!` a phrionnaíonn teaghrán go
an scáileán:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:print}}
```

Tá leid á phriontáil ag an gcód seo á rá cad é an cluiche agus ag iarraidh ionchur
ón úsáideoir.

### Luachanna a Stóráil le Athróga

Ansin, cruthóimid _athraitheach_ chun ionchur an úsáideora a stóráil, mar seo:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:string}}
```

Anois tá an clár ag éirí suimiúil! Tá go leor ar siúl sa bheagán seo
líne. Bainimid úsáid as an ráiteas `let` chun an athróg a chruthú. Seo sampla eile:

```rust,ignore
let úlla = 5;
```

Cruthaíonn an líne seo athróg nua darb ainm `úlla` agus ceanglaíonn sí é leis an luach 5. In
Meirge, tá athróga do-mharú de réir réamhshocraithe, rud a chiallaíonn nuair a thugaimid an athróg a
luach, ní athróidh an luach. Beidh an coincheap seo á phlé againn go mion
an [“Athróga agus Comhshócmhainneacht”][athróga-agus-shó-shó-athróga]<!-- neamhaird a dhéanamh ar -->
alt i gCaibidil 3. Chun athróg mutable a dhéanamh, cuirimid `mut` roimh an
ainm athróg:

```rust,ignore
let úlla = 5; // do-athraithe
let bananaí mut = 5; // inathraithe
```

> Nóta: Tosaíonn an chomhréir `//` trácht a leanann go dtí deireadh an
> líne. Déanann Rust neamhaird ar gach rud i dtuairimí. Déanfaimid trácht níos mó a phlé
> sonraí i [Caibidil 3][tráchtanna] <!-- neamhaird -->.

Ag filleadh ar an gclár cluiche buille faoi thuairim, tá a fhios agat anois go mbeidh `let mut tomhas`
athróg chomhshóite a thabhairt isteach darb ainm `tomhas`. Insíonn an comhartha comhionann (`=`) Rust dúinn
ag iarraidh rud éigin a cheangal leis an athróg anois. Ar thaobh na láimhe deise den chomhartha comhionann
an luach atá faoi cheangal ag `tomhas`, atá mar thoradh ar ghlaoch
`String::new`, feidhm a thugann sampla nua de `String` ar ais.
[`Teaghrán`][teaghrán] Is cineál teaghrán é <!-- neamhaird --> a sholáthraíonn an caighdeán
leabharlann atá ina giotán téacs ionchódaithe UTF-8 infhás.

Léiríonn an chomhréir `::` sa líne `::new` go bhfuil baint ag `new`
feidhm den chineál `String`. Feidhm _ghaolmhar_ is ea feidhm atá
curtha i bhfeidhm ar chineál, sa chás seo `String`. Cruthaíonn an fheidhm `new` seo a
teaghrán nua, folamh. Gheobhaidh tú feidhm `new` ar go leor cineálacha toisc gur a
ainm coitianta ar fheidhm a dhéanann luach nua de shaghas éigin.

Ina hiomláine, chruthaigh an líne `let mut tomhas = String::new();` mutable
athróg atá ceangailte faoi láthair le sampla nua, folamh de `String`. Tá sin réidh!

### Ag fáil Ionchur Úsáideora

Thabhairt chun cuimhne gur chuimsigh muid an fheidhmiúlacht ionchuir/aschuir ón gcaighdeán
leabharlann le `use std::io;` ar an gcéad líne den chlár. Anois cuirfimid glaoch
an fheidhm `stdin` ón modúl `io`, a ligfidh dúinn úsáideoir a láimhseáil
ionchur:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:read}}
```

Murar iompórtáladh muid an leabharlann `io` le `use std::io;` ag tús na
an chláir, d'fhéadfaimis an fheidhm a úsáid fós tríd an nglao feidhme seo a scríobh mar
`std::io::stdin`. Tugann an fheidhm `stdin` sampla de
[`std::io::Stdin`][iostdin] <!-- déan neamhaird de -->, ar cineál é a sheasann do
láimhseáil go dtí an t-ionchur caighdeánach do do teirminéal.

Ansin, glaonn an líne `.read_line(&mut tomhas)` ar [`read_line`][read_line]<!--
neamhaird --> modh ar an láimhseáil ionchur caighdeánach chun ionchur a fháil ón úsáideoir.
Tá `&mut tomhas` á rith againn freisin mar argóint chun `léamh_líne` a insint cad é
teaghrán chun ionchur an úsáideora a stóráil. Is é an jab iomlán de `read_line` a ghlacadh
is cuma cad iad na cineálacha úsáideora isteach i ionchur caighdeánach agus cuir é sin i sreangán
(gan a bhfuil ann a fhorscríobh), mar sin cuirimid an teaghrán sin ar aghaidh mar
argóint. Ní mór an argóint téad a bheith mutable ionas gur féidir an modh a athrú
ábhar an téad.

Léiríonn an `&` gur _reference_ atá san argóint seo, rud a thugann bealach duit
lig do chodanna iolracha de do chód rochtain a fháil ar phíosa amháin sonraí gan gá a dhéanamh
na sonraí sin a chóipeáil isteach i gcuimhne arís agus arís eile. Is gné chasta iad tagairtí,
agus ceann de mhórbhuntáistí Rust ná cé chomh sábháilte agus éasca é a úsáid
tagairtí. Ní gá go mbeadh a lán de na sonraí sin ar eolas agat chun é seo a chríochnú
clár. Faoi láthair, níl a fhios agat ach, cosúil le hathróga, is tagairtí iad
immutable de réir réamhshocraithe. Mar sin, ní mór duit `&mut tomhas` a scríobh seachas
`&tomhas` chun é a dhéanamh mutable. (Míneoidh Caibidil 4 tagairtí níos mó
go críochnúil.)

<!-- Old heading. Do not remove or links may break. -->

<a id="handling-potential-failure-with-the-result-type"></a>

### Teip Féideartha a Láimhseáil le `Toradh`

Táimid fós ag obair ar an líne cód seo. Tá an tríú líne á phlé againn anois
téacs, ach tabhair faoi deara go bhfuil sé fós mar chuid de líne chóid loighciúil amháin. An chéad cheann eile
Is cuid den mhodh seo:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:expect}}
```

D’fhéadfaimis an cód seo a scríobh mar:

```rust,ignore
io::stdin().read_line(&mut guess).expect("Failed to read line");
```

Is deacair líne fhada amháin a léamh, áfach, mar sin is fearr í a roinnt. Tá sé
Is minic a bhíonn sé ciallmhar líne nua agus spás bán eile a thabhairt isteach chun cabhrú le briseadh fada
línte nuair a ghlaonn tú ar mhodh leis an gcomhréir `.method_name()`. Anois déanaimis
pléigh cad a dhéanann an líne seo.

Mar a luadh cheana, cuireann `read_line` cibé rud a chuireann an t-úsáideoir isteach sa teaghrán
tugaimid air, ach tugann sé luach `Torthaí` ar ais freisin. [`Toradh`][toradh]<!--
neamhaird a dhéanamh ar --> is [_enumeration_][enums]<!-- neamhaird -->, ar a dtugtar _enum_ go minic,
atá cineál is féidir a bheith i gceann de na stáit iolracha. Glaoimid ar gach ceann acu
b'fhéidir luaigh _variant_.

[Caibidil 6][enums] Clúdóidh <!-- neamhaird --> enums níos mine. An cuspóir
de na cineálacha `Torthaí` seo is ea faisnéis láimhseála earráidí a ionchódú.

Is iad na leaganacha `Torthaí` ná `OK` agus `Err`. Léiríonn an leagan `Ok` an
D'éirigh leis an oibríocht, agus tá an luach a ghintear go rathúil ann.
Ciallaíonn an leagan `Err` gur theip ar an oibríocht, agus tá faisnéis ann
faoi ​​conas nó cén fáth ar theip ar an oibríocht.

Tá modhanna sainmhínithe ar luachanna an chineáil `Result`, cosúil le luachanna d'aon chineál
leo. Mar shampla de `Result` tá [`expect` method][expect] <!-- neamhaird -->
gur féidir leat glaoch. Más luach `Err` é an t-úsáír seo de `Result`, `expect`
a chur faoi deara an clár a tuairteála agus a thaispeáint ar an teachtaireacht a rith tú mar
argóint le `expect`. Má thugann an modh `read_line` `Err` ar ais, dhéanfadh sé
is dócha go bhfuil sé mar thoradh ar earráid a tháinig ón gcóras oibriúcháin bunúsach.
Más luach `OK` é an t-úsaid seo de `Result`, glacfaidh `expect` an tuairisceán
an luach atá ag `Ok` agus cuir an luach sin ar ais chugat ionas gur féidir leat é a úsáid.
Sa chás seo, is é an luach sin líon na mbeart in ionchur an úsáideora.

Mura nglaoann tú ‘ag súil’, tiomsóidh an clár, ach gheobhaidh tú rabhadh:

```console
{{#include ../../listings/ch02-guessing-game-tutorial/no-listing-02-without-expect/output.txt}}
```

Tugann Rust foláireamh nár úsáid tú an luach `Result' a fuarthas ar ais ó `read_line`,
ag tabhairt le fios nár láimhseáladh an clár earráid fhéideartha.

Is é an bealach ceart chun an rabhadh a chosc ná cód láimhseála earráidí a scríobh,
ach inár gcás ba mhaith linn ach a tuairteála an clár seo nuair a tharlaíonn fadhb, mar sin againn
is féidir `expect` a úsáid. Foghlaimeoidh tú faoi earráidí a athshlánú i [Chapter
9][recover] <!-- neamhaird a dhéanamh -->.

### Luachanna Priontála le Sealbhóirí Áite `println!`

Seachas an lúibín chatach deiridh, níl ach líne amháin eile le plé ann
an cód go dtí seo:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:print_guess}}
```

Priontálann an líne seo an teaghrán ina bhfuil ionchur an úsáideora anois. An tacar `{}` de
lúibíní curly is a placeholder: smaoineamh ar `{}` as little crab pincers that hold
luach i bhfeidhm. Nuair a bhíonn luach athróige á phriontáil, is féidir leis an ainm athróg
dul taobh istigh de na lúibíní curly. Nuair a phriontáil an toradh ar mheastóireacht ar
abairt, cuir lúibíní chatach folamh sa teaghrán formáid, ansin lean an
teaghrán formáide le liosta slonn scartha le camóg le priontáil i ngach folamh
lúibín curly placeholder san ord céanna. Athróg a phriontáil agus an toradh
de shloinneadh in aon ghlao amháin chun `println!` a bheadh ​​mar seo:

```rust
let x = 5;
let y = 10;

println!("x = {x} and y + 2 = {}", y + 2);
```

Phriontálfadh an cód seo `x = 5 agus y + 2 = 12`.

### An Chéad Chuid a Thástáil

Déanaimis an chéad chuid den chluiche buille faoi thuairim a thástáil. Rith é ag úsáid `cargo run`:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-01/
cargo clean
cargo run
input 6 -->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 6.44s
     Running `target/debug/guessing_game`
Guess the number!
Please input your guess.
6
You guessed: 6
```

Ag an bpointe seo, déantar an chéad chuid den chluiche: táimid ag fáil ionchur ó na
méarchlár agus ansin é a phriontáil.

## Uimhir Rúnda a Ghiniúint

Ansin, ní mór dúinn uimhir rúnda a ghiniúint a dhéanfaidh an t-úsáideoir iarracht a buille faoi thuairim. Tá an
chóir uimhir rúnda a bheith difriúil gach uair mar sin tá an cluiche spraoi a imirt níos mó
ná uair amháin. Úsáidfimid uimhir randamach idir 1 agus 100 ionas nach mbeidh an cluiche ann freisin
deacair. Ní chuimsíonn Rust feidhmiúlacht uimhreacha randamacha ina chaighdeán fós
leabharlann. Mar sin féin, soláthraíonn foireann Rust cliathbhosca [`rand` crate][randcrate] leis
dúirt feidhmiúlacht.

### Ag Úsáid cliathbhosca chun Feidhmiúlacht Níos Mó a Fháil

Cuimhnigh gur bailiúchán de chomhaid cód foinse Rust é cliathbhosca. An tionscadal
táimid ag tógáil cliathbhosca _dénártha_, atá inrite. An `rand`
cliathbhosca _library_ é an gcliathbhosca, ina bhfuil cód a bheartaítear a úsáid ann
cláir eile agus ní féidir iad a chur i gcrích leis féin.

Is é comhordú lasta na cliathbhoscaí seachtracha an áit a bhfuil an lasta ag taitneamh i ndáiríre. Roimh dúinn
in ann cód a scríobh a úsáideann `rand`, ní mór dúinn an comhad _Cargo.toml_ a mhodhnú go
cuir an cliathbhosca `rand` san áireamh mar spleáchas. Oscail an comhad sin anois agus cuir an
líne seo a leanas go dtí an bun, faoi bhun an ceanntásc alt `[dependencies]` go
Lasta cruthaithe duit. Bí cinnte `rand` a shonrú go díreach mar atá againn anseo, le
seans nach n-oibreoidh an uimhir leagain seo, nó na samplaí cóid sa rang teagaisc seo:

<!-- When updating the version of `rand` used, also update the version of
`rand` used in these files so they all match:
* ch07-04-bringing-paths-into-scope-with-the-use-keyword.md
* ch14-03-cargo-workspaces.md
-->

<span class="filename">Filename: Cargo.toml</span>

```toml
{{#include ../../listings/ch02-guessing-game-tutorial/listing-02-02/Cargo.toml:8:}}
```

Sa chomhad _Cargo.toml_, tá gach rud a leanann ceanntásc mar chuid de sin
alt a leanann ar aghaidh go dtí go dtosaíonn alt eile. I `[dependencies]` tú
inis do lasta cad iad na cliathbhoscaí seachtracha a bhraitheann do thionscadal agus cé na leaganacha díobh
na cliathbhoscaí sin atá uait. Sa chás seo, sonraimid an gcliathbhosca `rand` leis an
sonróir leagan shéimeantach `0.8.5`. Tuigeann lasta [Séimeantach
Leagan [semver] <!-- neamhaird --> (uaireanta ar a dtugtar _SemVer_), arb é a
caighdeánach chun uimhreacha leagan a scríobh. Is é an sonróir `0.8.5` i ndáiríre
gearrscríbhinn le haghaidh `^0.8.5`, rud a chiallaíonn aon leagan go bhfuil ar a laghad 0.8.5 ach
faoi ​​bhun 0.9.0.

Measann lasta go bhfuil API poiblí ag na leaganacha seo atá comhoiriúnach leis an leagan
0.8.5, agus cinntíonn an tsonraíocht seo go bhfaighidh tú an scaoileadh paiste is déanaí sin
fós le chéile leis an gcód sa chaibidil seo. Aon leagan 0.9.0 nó níos mó
Ní ráthaítear go mbeidh an API céanna ann agus a úsáideann na samplaí seo a leanas.

Anois, gan aon cheann den chód a athrú, déanaimis an tionscadal a thógáil, mar a thaispeántar i
Liostáil 2-2.

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-02/
rm Cargo.lock
cargo clean
cargo build -->

<Listing number="2-2" caption="The output from running `cargo build` after adding the rand crate as a dependency">

```console
$ cargo build
    Updating crates.io index
     Locking 16 packages to latest compatible versions
      Adding wasi v0.11.0+wasi-snapshot-preview1 (latest: v0.13.3+wasi-0.2.2)
      Adding zerocopy v0.7.35 (latest: v0.8.9)
      Adding zerocopy-derive v0.7.35 (latest: v0.8.9)
  Downloaded syn v2.0.87
  Downloaded 1 crate (278.1 KB) in 0.16s
   Compiling proc-macro2 v1.0.89
   Compiling unicode-ident v1.0.13
   Compiling libc v0.2.161
   Compiling cfg-if v1.0.0
   Compiling byteorder v1.5.0
   Compiling getrandom v0.2.15
   Compiling rand_core v0.6.4
   Compiling quote v1.0.37
   Compiling syn v2.0.87
   Compiling zerocopy-derive v0.7.35
   Compiling zerocopy v0.7.35
   Compiling ppv-lite86 v0.2.20
   Compiling rand_chacha v0.3.1
   Compiling rand v0.8.5
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 3.69s
```

</Listing>

Seans go bhfeicfidh tú uimhreacha leaganacha éagsúla (ach beidh siad go léir ag luí leis an
cód, a bhuíochas le SemVer!) agus línte éagsúla (ag brath ar an oibríocht
córas), agus féadfaidh na línte a bheith in ord difriúil.

Nuair a chuirimid spleáchas seachtrach san áireamh, faigheann lasta na leaganacha is déanaí de
gach rud a theastaíonn ó spleáchas ón _registry_, is cóip de shonraí é
ó [Crates.io][cratesio]. Is é Crates.io áit a bhfuil daoine san éiceachóras Rust
postáil a dtionscadail foinse oscailte Rust do dhaoine eile le húsáid.

Tar éis an chlár a nuashonrú, seiceálann Cargo an rannán `[dependencies]` agus
íoslódáil aon cliathbhoscaí liostaithe nach bhfuil íoslódáilte cheana. Sa chás seo,
cé nár liostaíomar ach `rand` mar spleáchas, rug lasta cliathbhoscaí eile freisin
go mbraitheann `rand` ar a bheith ag obair. Tar éis na cliathbhoscaí a íoslódáil, tiomsaíonn Rust
iad agus ansin déanann sé an tionscadal a thiomsú leis na spleáchais atá ar fáil.

Má ritheann tú `cargo build` láithreach láithreach gan aon athruithe a dhéanamh, ní mór duit
ní bhfaighidh tú aon aschur ach amháin ón líne `Finished`. Tá a fhios ag lasta cheana féin
íoslódáil agus tiomsaíodh na spleáchais, agus níl aon rud athraithe agat
fúthu i do chomhad _Cargo.toml_. Tá a fhios ag lasta freisin nach bhfuil tú tar éis athrú
rud ar bith faoi do chód, mar sin ní athchruinníonn sé é sin ach an oiread. Gan faic le
a dhéanamh, fágann sé go simplí.

Má osclaíonn tú an comhad _src/main.rs_, déan athrú fánach, agus ansin é a shábháil agus
tóg arís, ní fheicfidh tú ach dhá líne aschuir:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-02/
touch src/main.rs
cargo build -->

```console
$ cargo build
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.13s
```

Léiríonn na línte seo nach ndéanann lasta an tógáil a nuashonrú ach amháin le d'athrú beag ar an
_src/main.rs_ comhad. Níor athraigh do spleáchais, mar sin tá a fhios ag Cargo gur féidir
athúsáid a bhfuil íoslódáilte aige cheana féin agus tiomsaithe dóibh siúd.

#### Tógálacha In-atáirgthe a Chinntiú leis an gComhad _Cargo.lock_

Tá meicníocht ag lasta a chinntíonn gur féidir leat an déantán céanna a atógáil gach uair
tógann tusa nó aon duine eile do chód: ní úsáidfidh lasta ach na leaganacha de na
spleáchais a shonraigh tú go dtí go léiríonn tú a mhalairt. Mar shampla, abair é sin
an tseachtain seo chugainn tagann leagan 0.8.6 den gcliathbhosca `rand` amach, agus an leagan sin
tá ceartúchán tábhachtach ar fhabht, ach tá aischéimniú ann freisin a dhéanfaidh
briseadh do chód. Chun é seo a láimhseáil, cruthaíonn Rust an comhad _Cargo.lock_ ar dtús
an t-am a ritheann tú `cargo build`, mar sin tá sé seo againn anois sa chluiche _guessing_
eolaire.

Nuair a thógann tú tionscadal den chéad uair, déanann lasta na leaganacha go léir a léiriú
de na spleáchais a oireann do na critéir agus ansin iad a scríobh chuig an
_Cargo.lock_ comhad. Nuair a bheidh tú ag tógáil do thionscadal sa todhchaí, feicfidh lasta
go bhfuil an comhad _Cargo.lock_ ann agus go n-úsáidfidh sé na leaganacha atá sonraithe ann
seachas an obair ar fad a dhéanamh chun leaganacha a aimsiú arís. Ligeann sé seo duit
tógáil in-atáirgthe go huathoibríoch. I bhfocail eile, beidh do thionscadal
fanacht ag 0.8.5 go dtí go n-uasghrádóidh tú go sainráite, a bhuíochas leis an gcomhad _Cargo.lock_.
Toisc go bhfuil an comhad _Cargo.lock_ tábhachtach le haghaidh tógála in-atáirgthe, is minic a bhíonn
sheiceáil i rialú foinse leis an gcuid eile den chód i do thionscadal.

#### cliathbhosca á nuashonrú chun leagan nua a fháil

Nuair is mian leat _do_ cliathbhosca a nuashonrú, soláthraíonn Cargo an t-ordú `update`,
a dhéanfaidh neamhaird ar an gcomhad _Cargo.lock_ agus figiúr amach go léir na leaganacha is déanaí
a oireann do shonraíochtaí i _Cargo.toml_. Scríobhfaidh lasta iad siúd ansin
leaganacha don chomhad _Cargo.lock_. Sa chás seo, ní bheidh ach lorg ag Cargo
leaganacha níos mó ná 0.8.5 agus níos lú ná 0.9.0. Má tá an gcliathbhosca `rand`
scaoileadh an dá leagan nua 0.8.6 agus 0.9.0, d'fheicfeá an méid seo a leanas más rud é
rith tú `cargo update`:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-02/
cargo update
assuming there is a new 0.8.x version of rand; otherwise use another update
as a guide to creating the hypothetical output shown here -->

```console
$ cargo update
    Updating crates.io index
    Updating rand v0.8.5 -> v0.8.6
```

Déanann lasta neamhaird ar an scaoileadh 0.9.0. Ag an bpointe seo, thabharfá athrú faoi deara freisin
i do chomhad _Cargo.lock_ ag tabhairt faoi deara gurb é an leagan den chliabhán `rand` atá tú
ag baint úsáide as anois tá 0.8.6. Chun `rand` leagan 0.9.0 nó aon leagan sa 0.9._x_ a úsáid
sraith, bheadh ​​ort an comhad _Cargo.toml_ a nuashonrú chun breathnú mar seo ina ionad:

```toml
[dependencies]
rand = "0.9.0"
```

An chéad uair eile a ritheann tú `cargo build`, déanfaidh lasta clár na gcliathbhosca a nuashonrú
ar fáil agus déan do riachtanais `rand` a athmheas de réir an leagain nua
atá sonraithe agat.

Tá go leor eile le rá faoi [Cargo][doccargo] <!-- neamhaird --> agus [dá
éiceachóras][doccratesio]<!-- neamhaird a dhéanamh ar -->, a phléfaimid i gCaibidil 14, ach
faoi ​​láthair, sin é gach ní mór duit fios a bheith agat. Déanann lasta an-éasca é a athúsáid
leabharlanna, mar sin tá Rustaceans in ann tionscadail níos lú a scríobh a chuirtear le chéile
ó roinnt pacáistí.

### Uimhir Randamach á giniúint

Cuirimis tús le `rand` a úsáid chun uimhir a ghiniúint le buille faoi thuairim. Is é an chéad chéim eile
nuashonraigh _src/main.rs_, mar a thaispeántar i Liostú 2-3.

<Listing number="2-3" file-name="src/main.rs" caption="Adding code to generate a random number">

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-03/src/main.rs:all}}
```

</Listing>

Ar dtús cuirimid an líne `use rand::Rng;`. Sainmhíníonn an tréithe `Rng` modhanna a
cuireann gineadóirí uimhreacha randamacha i bhfeidhm, agus caithfidh an tréith seo a bheith laistigh den scóip dúinn
na modhanna sin a úsáid. Clúdóidh Caibidil 10 tréithe go mion.

Ansin, cuirfimid dhá líne sa lár. Sa chéad líne, tugaimid an
feidhm `rand::thread_rng` a thugann an uimhir randamach ar leith dúinn
gineadóir a úsáidfimid: ceann atá áitiúil don snáithe reatha de
fhorghníomhú agus tá síolú ag an gcóras oibriúcháin. Ansin tugaimid an `gen_range`
modh ar an ngineadóir uimhreacha randamacha. Tá an modh seo sainmhínithe ag an `Rng`
tréithe a thugamar isteach sa scóip leis an ráiteas `use rand::Rng;`. Tá an
Glacann modh `gen_range` slonn raoin mar argóint agus gineann sé a
uimhir randamach sa raon. Glacann an cineál slonn raoin atá á úsáid againn anseo
an fhoirm `start..=end` agus tá sé san áireamh ar na teorainneacha íochtair agus uachtair, mar sin againn
Ní mór `1..=100` a shonrú chun uimhir idir 1 agus 100 a iarraidh.

> Tabhair faoi deara: Ní bheidh a fhios agat cad iad na tréithe is cóir a úsáid agus cé na modhanna agus na feidhmeanna
> chun glaoch ó chliathbhosca, ionas go mbeidh doiciméadú le treoracha le haghaidh gach cliathbhosca
> é a úsáid. Gné néata eile de lasta is ea an doiciméad lasta a rith
> Tógfaidh --open`ordú doiciméadú a sholáthraíonn do chuid spleáchais go léir
go háitiúil agus oscail i do bhrabhsálaí é. Má tá suim agat i gceann eile
feidhmiúlacht sa gcliathbhosca`rand`, mar shampla, rith `cargo doc --open`agus
cliceáil`rand` sa bharra taoibh ar chlé.

Déanann an dara líne nua an uimhir rúnda a phriontáil. Tá sé seo úsáideach agus muid
an clár a fhorbairt le bheith in ann é a thástáil, ach scriosfaimid as an
leagan deiridh. Ní mór an cluiche é má phriontáileann an clár an freagra chomh luath
mar a thosaíonn sé!

Bain triail as an gclár a rith cúpla uair:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-03/
cargo run
4
cargo run
5
-->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.02s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 7
Please input your guess.
4
You guessed: 4

$ cargo run
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.02s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 83
Please input your guess.
5
You guessed: 5
```

Ba cheart duit uimhreacha randamacha éagsúla a fháil, agus ba cheart gur uimhreacha idir iad go léir
1 agus 100. Jab iontach!

## An Bhuille faoi thuairim a chur i gcomparáid leis an Uimhir Rúnda

Anois go bhfuil ionchur úsáideora agus uimhir randamach againn, is féidir linn iad a chur i gcomparáid. An chéim sin
léirithe i Liostú 2-4. Tabhair faoi deara nach mbeidh an cód seo le chéile go fóill, mar a dhéanfaimid
mínigh.

<Listing number="2-4" file-name="src/main.rs" caption="Handling the possible return values of comparing two numbers">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-04/src/main.rs:here}}
```

</Listing>

Ar dtús cuirimid ráiteas `use` eile leis, ag tabhairt cineál ar a dtugtar
`std::cmp::Ordering`isteach sa raon feidhme ón leabharlann chaighdeánach. An cineál `Ordering`
Is enum eile é agus tá na leaganacha `Less`, `Greater`, agus `Equal` ann. Is iad seo
na trí thoradh is féidir nuair a dhéanann tú comparáid idir dhá luach.

Ansin cuirimid cúig líne nua ag bun a úsáideann an cineál `Ordering`. Tá an
Déanann modh `cmp` dhá luach i gcomparáid agus is féidir glaoch a chur air ar aon rud is féidir
i gcomparáid. Déanann sé tagairt do cibé rud is mian leat a chur i gcomparáid leis: seo é
comparáid a dhéanamh idir `buille faoi thuairim` agus `uimhir_rúnda`. Ansin filleann sé leagan de na
‘Ordú’ enum thugamar isteach scóip leis an ráiteas ‘úsáide’. Úsáidimid a
[`match`][match]<!-- neamhaird a dhéanamh ar --> slonn le socrú cad é an chéad rud eile le déanamh bunaithe air
cén leagan de `Ordú` a cuireadh ar ais ón nglao go `cmp` leis na luachanna
in `buille faoi thuairim` agus `uimhir_rúnda`.

Tá slonn `match` comhdhéanta de _arms_. Is éard atá i lámh ná _pattern_ to
mheaitseáil i gcoinne, agus an cód ba chóir a rith má tá an luach a thugtar do `match`
oireann patrún na láimhe sin. Glacann meirge an luach a thugtar do `mheaitseáil` agus cuma
trí phatrún gach lámh ar a seal. Is iad patrúin agus an tógáil `meaits`
gnéithe cumhachtacha meirge: ligeann siad duit do chód a chur in iúl ar chásanna éagsúla
d'fhéadfadh teacht trasna orthu agus déanann siad cinnte go láimhseálann tú iad go léir. Beidh na gnéithe seo
clúdaithe go mion i gCaibidil 6 agus i gCaibidil 19, faoi seach.

Siúlfaimid trí shampla leis an slonn `match` a úsáidimid anseo. Abair é sin
tá buille faoi thuairim ag an úsáideoir 50 agus is é an uimhir rúnda a ghintear go randamach an uair seo 38.

Nuair a chuirtear an cód i gcomparáid le 50 go 38, fillfidh an modh `cmp`
`Ordering::Greater` toisc go bhfuil 50 níos mó ná 38. Faigheann an slonn `match`
an luach `Ordering::Greater` agus tosaíonn sé ag seiceáil patrún gach lámh. Breathnaíonn sé
ag patrún an chéad lámh, `Ordering::Less`, agus feiceann sé go bhfuil an luach
Ní hionann `Ordering::Greater` le `Ordering::Less`, mar sin déanann sé neamhaird den chód i
an lámh sin agus a ghluaiseann go dtí an chéad lámh eile. Is é patrún an chéad lámh eile
`Ordering::Greater`, a _dhéanann_ mar a chéile le `Ordering::Greater`! An gaolmhar
déanfar cód sa lámh sin a fhorghníomhú agus a phriontáil `Too big!` ar an scáileán. An `match`
críochnaíonn an abairt tar éis an chéad chluiche rathúil, mar sin ní bhreathnóidh sé ar an gceann deireanach
lámh sa chás seo.

Mar sin féin, ní thiomsóidh an cód i Liostú 2-4 fós. Déanaimis iarracht é:

<!--
The error numbers in this output should be that of the code **WITHOUT** the
anchor or snip comments
-->

```console
{{#include ../../listings/ch02-guessing-game-tutorial/listing-02-04/output.txt}}
```

Luaitear i gcroílár na hearráide go bhfuil _cineálacha mímheaitseála_ ann. Tá meirge ag
córas cineál láidir statach. Mar sin féin, tá tátal cineáil aige freisin. Nuair a scríobhamar
`let mut guess = String::new()`, bhí Rust in ann a thuiscint gur cheart go mbeadh `guess`
a `String` agus níor chuir sé orm an cineál a scríobh. An `secret_number`, ar an taobh eile
láimhe, is cineál uimhreach é. Is féidir luach idir 1 a bheith ag roinnt cineálacha uimhreacha Rust
agus 100: `i32`, uimhir 32 ghiotán; `u32`, uimhir 32-giotán gan síniú; `i64`, a
uimhir 64-giotán; chomh maith le daoine eile. Mura sonraítear a mhalairt, mainneachtainí Rust
an `i32`, is é sin an cineál `secret_number` mura gcuireann tú cineál faisnéise leis
in áiteanna eile a chuirfeadh Rust le tátal a bhaint as cineál uimhriúil difriúil. An chúis
is é an earráid ná nach féidir le Rust teaghrán agus cineál uimhreach a chur i gcomparáid.

I ndeireadh na dála, ba mhaith linn an `String` a léann an clár mar ionchur a thiontú ina
cineál uimhreach ionas gur féidir linn é a chur i gcomparáid go huimhriúil leis an uimhir rúnda. Déanaimid amhlaidh trí
an líne seo a chur leis an gcorp feidhme `main`:

span class="filename">Filename: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/no-listing-03-convert-string-to-number/src/main.rs:here}}
```

Is é an líne:

```rust,ignore
let guess: u32 = guess.trim().parse().expect("Please type a number!");
```

Cruthaímid athróg darb ainm `buille faoi thuairim`. Ach fan, nach bhfuil an clár cheana féin
athróg darb ainm `buille faoi thuairim`? Déanann sé, ach cuiditheach ligeann Rust dúinn scáthú an
luach `buille faoi thuairim` roimhe seo le ceann nua. Ligeann _Scáthú_ dúinn an `buille faoi thuairim` a athúsáid
ainm athróg seachas iallach a chur orainn dhá athróg uathúla a chruthú, mar shampla
`guess_str` agus `buille faoi thuairim`, mar shampla. Clúdóimid é seo níos mine i
[Caibidil 3][scáthú] <!-- neamhaird -->, ach faoi láthair, fios go bhfuil an ghné seo
a úsáidtear go minic nuair is mian leat luach a thiontú ó chineál amháin go cineál eile.

Ceanglaíonn muid an athróg nua seo leis an slonn `guess.trim().parse()`. An `buille faoi thuairim`
tagraíonn an abairt don bhunathróg `buille faoi thuairim` ina raibh an
ionchur mar teaghrán. Cuirfidh an modh `trim` ar shampla `Teaghrán` deireadh le haon cheann
spás bán ag tús agus deireadh, rud nach mór dúinn a dhéanamh sular féidir linn a thiontú ar an
teaghrán go `u32`, nach féidir ach sonraí uimhriúla a bheith ann. Caithfidh an t-úsáideoir brúigh
<kbd>iontráil</kbd> chun `read_line` a shásamh agus chun a gcuid buille faoi thuairim a ionchur, rud a chuireann le
carachtar nualíne don teaghrán. Mar shampla, má chuireann an t-úsáideoir cineál <kbd>5</kbd> agus
brúigh <kbd>iontráil</kbd>, breathnaíonn `buille faoi thuairim` mar seo: `5\n`. Léiríonn an `\n`
"líne nua." (Ar Windows, má bhrúnn tú <kbd>enter</kbd> beidh tuairisceán iompair ann
agus líne nua, `\r\n`.) Cuireann an modh `Baile Átha Troim` deireadh le `\n` nó `\r\n`, agus mar thoradh air sin
i `5` díreach.

Tiontaíonn an modh [`parsáil` ar teaghráin][parsáil] <!-- neamhaird --> teaghrán go
cineál eile. Anseo, bainimid úsáid as é a thiontú ó teaghrán go uimhir. Caithfimid
inis do Rust an cineál uimhreach cruinn atá uainn trí úsáid a bhaint as `lig faoi thuairim: u32`. An colon
(`:`) Tar éis do 'buille faoi thuairim' a rá le Rust déanfaimid cineál na hathróige anótáil. Tá meirge ag
cúpla cineál uimhreacha ionsuite; is slánuimhir 32-giotán gan síniú é an `u32` a fheictear anseo.
Is rogha réamhshocraithe maith é do líon beag dearfach. Foghlaimeoidh tú faoi
cineálacha uimhreacha eile i [Caibidil 3][sláine]<!-- neamhaird a dhéanamh ar -->.

Ina theannta sin, tá an nóta `u32` sa chlár samplach seo agus an chomparáid
le `secret_number` ciallaíonn sé go mbainfidh Rust le tuiscint gur cheart go mbeadh `uimhir_rúnda` ina
`u32` chomh maith. Mar sin anois beidh an chomparáid idir dhá luach mar an gcéanna
cineál!

Ní oibreoidh an modh `parse` ach ar charachtair ar féidir iad a thiontú go loighciúil
isteach uimhreacha agus mar sin is féidir earráidí a chruthú go héasca. Más rud é, mar shampla, an teaghrán
ina bhfuil `A👍%`, ní bheadh ​​aon bhealach ann é sin a thiontú go huimhir. Mar gheall air
b'fhéidir go dteipeann orthu, tugann an modh `parsáil` cineál `Torthaí` ar ais, cosúil leis an `léamh_líne`
(a pléadh níos luaithe in [“Ag Láimhseáil Teip Féideartha le
`Toradh`”](#handling-potential-teip-le-toradh) <!-- neamhaird-->). Déileálfaimid
an `Toradh` seo ar an mbealach céanna trí úsáid a bhaint as an modh `súil` arís. Má `parse`
seolann sé leagan ` Err``Result ` ar ais toisc nach raibh sé in ann uimhir a chruthú ón
teaghrán, beidh an glao `ag súil` tuairteála an cluiche agus a phriontáil an teachtaireacht a thugaimid dó.
Más féidir le `parse` an teaghrán a thiontú go huimhir go rathúil, seolfaidh sé an
Leagan `Ok` de `Toradh`, agus tabharfaidh `ag súil` ar ais an uimhir a theastaíonn uainn
an luach `Ok`.

Rithfimid an clár anois:

[prelude]: ../std/prelude/index.html
[variables-and-mutability]: ch03-01-variables-and-mutability.html#variables-and-mutability
[comments]: ch03-04-comments.html
[string]: ../std/string/struct.String.html
[iostdin]: ../std/io/struct.Stdin.html
[read_line]: ../std/io/struct.Stdin.html#method.read_line
[result]: ../std/result/enum.Result.html
[enums]: ch06-00-enums.html
[expect]: ../std/result/enum.Result.html#method.expect
[recover]: ch09-02-recoverable-errors-with-result.html
[randcrate]: https://crates.io/crates/rand
[semver]: http://semver.org
[cratesio]: https://crates.io/
[doccargo]: https://doc.rust-lang.org/cargo/
[doccratesio]: https://doc.rust-lang.org/cargo/reference/publishing.html
[match]: ch06-02-match.html
[shadowing]: ch03-01-variables-and-mutability.html#shadowing
[parse]: ../std/primitive.str.html#method.parse
[integers]: ch03-02-data-types.html#integer-types
