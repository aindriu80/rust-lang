## Cineálacha Sonraí

Tá gach luach i Rust de chineál _data_ áirithe, a insíonn do Rust cén cineál
sonraí á shonrú ionas go mbeidh a fhios aige conas oibriú leis na sonraí sin. Breathnóimid ar
dhá fhothacar de chineál sonraí: scálach agus cumaisc.

Coinnigh i gcuimhne gur teanga _statically typed_ í Rust, rud a chiallaíonn go bhfuil sé
ní mór go mbeadh a fhios ag na cineálacha athróg go léir ag am tiomsaithe. Is féidir leis an tiomsaitheoir de ghnáth
tátal a bhaint as cén cineál ba mhaith linn a úsáid bunaithe ar an luach agus conas a úsáidimid é. I gcásanna
nuair is féidir go leor cineálacha a dhéanamh, mar shampla nuair a d'iompaíomar `String` go huimhriúil
clóscríobh ag baint úsáide as `parse` sa [“Ag Comparáid an Tomhais leis an Rúnduine”][comparing-the-guess-to-the-secret-number]<!-- neamhaird a dhéanamh ar --> alt sa
Caibidil 2, ní mór dúinn nóta cineáil a chur leis, mar seo:

```rust
let guess: u32 = "42".parse().expect("Not a number!");
```

Mura gcuirfimid an nóta cineál `: u32` a thaispeántar sa chód roimhe seo, Rust
taispeánfaidh sé an earráid seo a leanas, rud a chiallaíonn go dteastaíonn níos mó ón tiomsaitheoir
faisnéis uainn chun a fháil amach cén cineál ba mhaith linn a úsáid:

```console
{{#include ../../listings/ch03-common-programming-concepts/output-only-01-no-type-annotations/output.txt}}
```         

Feicfidh tú nótaí cineálacha éagsúla le haghaidh cineálacha eile sonraí.

### Cineálacha Scalar

Is ionann cineál _scalar_ agus luach amháin. Tá ceithre phríomhchineál scálach ag meirge:
slánuimhreacha, uimhreacha snámhphointe, Booles, agus carachtair. Seans go n-aithníonn tú
iad seo ó theangacha ríomhchlárúcháin eile. Léimid an chaoi a n-oibríonn siad i Rust.

#### Cineálacha Slánuimhir

Is uimhir é _ slánuimhir_ gan comhpháirt codánach. D’úsáideamar slánuimhir amháin
clóscríobh i gCaibidil 2, an cineál `u32`. Tugann an dearbhú cineál seo le fios go bhfuil an
ba cheart gur slánuimhir gan síniú (cineálacha slánuimhir sínithe a bheadh ​​sa luach a bhaineann leis
tosú le `i` in ionad `u`) a thógann suas le 32 giotán spáis. Léiríonn Tábla 3-1
na cineálacha slánuimhir ionsuite i Rust. Is féidir linn aon cheann de na leaganacha seo a úsáid chun a dhearbhú
an cineál luach slánuimhir.

<span class="caption">Tábla 3-1: Cineálacha Slánuimhir i Meirge</span>

| Fad        | Sínithe | Gan síniú |
| ---------- | ------- | --------- |
| 8-giotán   | `i8`    | `u8`      |
| 16-giotán  | `i16`   | `u16`     |
| 32-giotán  | `i32`   | `u32`     |
| 64-giotán  | `i64`   | `u64`     |
| 128-giotán | `i128`  | `u128`    |
| arch       | `isize` | `usize`   |

Is féidir le gach malairt a bheith sínithe nó gan síniú agus tá méid follasach aige.
Tagraíonn _Signed_ agus _unsigned_ do cibé an féidir an uimhir a bheith
diúltach - i bhfocail eile, cibé an gá comhartha a bheith ag an uimhir
(sínithe) nó cibé an mbeidh sé dearfach choíche agus an féidir a bheith mar sin
ionadaíocht gan comhartha (gan síniú). Tá sé cosúil le huimhreacha a scríobh ar pháipéar: cathain
tá an comhartha tábhachtach, taispeántar uimhir le comhartha móide nó comhartha lúide; áfach,
nuair atá sé sábháilte glacadh leis go bhfuil an uimhir deimhneach, taispeántar é gan aon chomhartha.
Stóráiltear uimhreacha sínithe trí úsáid a bhaint as [dhá chomhlánú][twos-complement]<!-- neamhaird
--> ionadaíocht.

Is féidir le gach leagan sínithe uimhreacha a stóráil ó -(2<sup>n - 1</sup>) go 2<sup>n -
1</sup> - 1 san áireamh, áit arb é _n_ líon na ngiotán a úsáideann an leagan. Mar sin an
Is féidir le `i8` uimhreacha a stóráil ó -(2<sup>7</sup>) go 2<sup>7</sup> - 1, arb ionann é
-128 go 127. Is féidir le leaganacha neamhshínithe uimhreacha a stóráil ó 0 go 2<sup>n</sup> - 1,
mar sin is féidir le `u8` uimhreacha a stóráil ó 0 go 2<sup>8</sup> - 1, arb ionann é agus 0 go 255.

Ina theannta sin, braitheann na cineálacha `isize` agus `usize` ar ailtireacht an
ríomhaire a bhfuil do ríomhchlár ar siúl air, atá sonraithe sa tábla mar “áirse”:
64 giotán má tá tú ar ailtireacht 64-giotán agus 32 giotán má tá tú ar 32-giotán
ailtireacht.

Is féidir leat slánuimhreacha a scríobh in aon cheann de na foirmeacha a thaispeántar i dTábla 3-2. Nóta
go gceadaítear iarmhír cineáil i lítir uimhreacha ar féidir a bheith ina gcineálacha iolracha uimhriúla,
mar `57u8`, chun an cineál a ainmniú. Is féidir le huimhreacha `_` a úsáid mar a
deighilteoir amhairc chun an uimhir a dhéanamh níos éasca le léamh, mar `1_000`, a dhéanfaidh
beidh an luach céanna agat agus dá mbeadh `1000` sonraithe agat.

<span class="caption">Tábla 3-2: Slánuimhir Liteartha i Meirge</span>

| Uimhreacha litrithe | Sampla 		  |
| ------------------- | ------------- |
| Deachúil   	      | `98_222`      |
| Heics   	 		  | `0xff` 		  |
| Octal      		  | `0o77` 		  |
| Dénártha			  | `0b1111_0000` |
| Beart (`u8` amháin) | `b'A'` 		  |

Mar sin cén chaoi a bhfuil a fhios agat cén cineál slánuimhir atá le húsáid? Mura bhfuil tú cinnte, Rust's
is áiteanna maithe iad mainneachtainí de ghnáth le tosú: réamhshocrú cineálacha slánuimhir go `i32`.
Is é an príomhstaid ina n-úsáidfeá `isize` nó `usize` agus tú ag innéacsú
bailiúchán de shaghas éigin.

> ##### Sárshreabhadh Slánuimhir
>
> Ligean le rá go bhfuil athróg de chineál `u8` agat ar féidir leis luachanna a choinneáil idir 0 agus
> 255. Má dhéanann tú iarracht an athróg a athrú go luach lasmuigh den raon sin, mar
> 256, tarlóidh _integer overflow_, agus is féidir ceann amháin de dhá iompar a bheith mar thoradh air.
> Agus tú ag tiomsú i mód dífhabhtaithe, cuimsíonn Rust seiceálacha le haghaidh ró-shreabhadh slánuimhir
> a chuireann faoi deara do chlár _panic_ ag am rite má tharlaíonn an t-iompar seo. Meirge
> úsáideann an téarma _panicking_ nuair a scoireann clár le hearráid; pléifimid
> scaoll níos doimhne sa [“Earráidí Do-aisghabhála le
> `panic!`”][unrecoverable-errors-with-panic]<!-- neamhaird a dhéanamh ar --> alt i gCaibidil 9.
>
>
> Agus tú ag tiomsú i mód scaoilte leis an mbratach `--release`, déanann Rust amhlaidh
> _not_ seiceálacha a chur san áireamh le haghaidh ró-shreabhadh slánuimhir a bhíonn ina chúis le scaoll. Ina áit sin, más rud é
> tarlaíonn ró-shreabhadh, feidhmíonn Rust _two's compliment wrapping_. I mbeagán focal, luachanna
> níos mó ná an t-uasluach is féidir leis an gcineál “timfhilleadh” a choinneáil chomh híseal agus is féidir
> de na luachanna is féidir leis an gcineál a choinneáil. I gcás `u8`, déantar an luach 256
> 0, éiríonn an luach 257 1, agus mar sin de. Ní bheidh an clár scanraithe, ach beidh an
> beidh luach ag an athróg is dócha nach é an luach a raibh tú ag súil leis
> bhfuil. Meastar gur earráid é a bheith ag brath ar iompar fillte an tslánuimhir thar maoil.
>
> Chun an fhéidearthacht ró-shreabhadh a láimhseáil go sainráite, is féidir leat na teaghlaigh seo a úsáid
> modhanna a sholáthraíonn an leabharlann chaighdeánach do chineálacha uimhriúla primitive:
>
> - Wrap i ngach modh leis na modhanna `wrapping_*`, mar shampla `wrapping_add`.
> - Tabhair ar ais an luach `None` má tá cur thar maoil leis na modhanna `checked_*`.
> - Tabhair ar ais an luach agus Boole ag cur in iúl an raibh cur thar maoil le
> na modhanna `overflowing_*`.
> - Sáithithe ag íosluachanna nó uasluachanna an luacha leis an `saturating_*`
> modhanna.

#### Cineálacha Snámhphointe

Tá dhá chineál primitive ag Rust freisin le haghaidh _floating-point numbers_, is iad sin
uimhreacha le pointí deachúla. Is iad cineálacha snámhphointe meirge ná `f32` agus `f64`,
atá 32 giotán agus 64 giotán i méid, faoi seach. Is é an cineál réamhshocraithe `f64`
mar gheall ar LAPanna nua-aimseartha, tá sé thart ar an luas céanna le `f32` ach tá sé in ann
níos cruinne. Tá gach cineál snámhphointe sínithe.

Seo sampla a thaispeánann uimhreacha snámhphointe i ngníomh:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-06-floating-point/src/main.rs}}
```

Léirítear uimhreacha snámhphointe de réir an chaighdeáin IEEE-754.  Is snámhphointe aon-chruinneas é an cineál `f32`, agus tá cruinneas dúbailte ag `f64`.

#### Oibríochtaí Uimhriúla

Tacaíonn Rust leis na hoibríochtaí bunúsacha matamaitice a mbeifeá ag súil leo don uimhir ar fad
cineálacha: suimiú, dealú, iolrú, roinnt, agus fuílleach. Slánuimhir
teascadh an rannán i dtreo náid go dtí an tslánuimhir is gaire. Léiríonn an cód seo a leanas
conas a d’úsáidfeá gach oibríocht uimhriúil i ráiteas `let`:


<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-07-numeric-operations/src/main.rs}}
```

Úsáideann gach slonn sna ráitis seo oibreoir matamaitice agus déanann sé meastóireacht
go luach aonair, atá ceangailte ansin le hathróg. [Aguisín
B][appendix_b]<!-- neamhaird --> tá liosta de na hoibreoirí go léir a Rust
soláthraíonn.

#### An Cineál Boole

Mar atá i bhformhór na dteangacha ríomhchlárúcháin eile, tá dhá fhéidearthacht ag cineál Boole in Rust
luachanna: `true` agus `false`. Is beart amháin iad Booleans. An cineál Boole i
Sonraítear meirge ag baint úsáide as `bool`. Mar shampla:

<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-08-boolean/src/main.rs}}
```

Is é an príomhbhealach chun luachanna Boole a úsáid ná trí choinníollacha, mar `if`
léiriú. Clúdóimid conas a oibríonn nathanna `if` i Rust sa [“Control
Sreabhadh”][control-flow]<!-- neamhaird a dhéanamh --> alt.

#### An Cineál Carachtair

Is é an cineál `char` Rust an cineál aibítre is primitíbhí sa teanga. Seo iad
roinnt samplaí de luachanna `char` a dhearbhú:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-09-char/src/main.rs}}
```

Tabhair faoi deara go sonraimid `char` litriúil le comharthaí athfhriotail singil, seachas teaghrán
litriúil, a úsáideann Sleachta dúbailte. Tá cineál `char` Rust ceithre beart i méid agus
Léiríonn Luach Scálar Unicode, rud a chiallaíonn gur féidir leis a lán níos mó a léiriú ná
ach ASCII. Litreacha accented; Carachtair na Síne, na Seapáine agus na Cóiré; emoji;
agus is luachanna `char` bailí iad spásanna ar leithead nialasach i Rust. Scálar Unicode
Réimníonn luachanna ó `U+0000` go `U+D7FF` agus `U+E000` go `U+10FFFF` san áireamh.
Mar sin féin, ní coincheap in Unicode é “carachtar” i ndáiríre, mar sin do dhuine
b'fhéidir nach bhfuil an intuiscint maidir le cad is “carachtar” ann ag teacht leis an rud atá i ‘char’
Meirge. Déanfaimid an t-ábhar seo a phlé go mion i [“Ag stóráil Téacs Ionchódaithe UTF-8 le
Teaghráin”][strings]<!-- neamhaird --> i gCaibidil 8.

### Cineálacha Comhdhúile

Is féidir le _Compound types_ luachanna iolracha a ghrúpáil i gcineál amháin. Tá dhá cheann ag meirge
cineálacha cumaisc primitive: tuples agus eagair.

#### An Cineál Tuple

Is bealach ginearálta é A _tuple_ chun líon luachanna a ghrúpáil le chéile le a
éagsúlacht cineálacha isteach i gcineál cumaisc amháin. Tá fad seasta ag tuples: uair amháin
dearbhaithe, ní féidir leo fás nó crapadh i méid.

Cruthaímid tuple trí liosta luachanna atá scartha le camóga a scríobh taobh istigh
lúibíní. Tá cineál ag gach seasamh sa tuple, agus cineálacha an
ní gá go mbeadh luachanna difriúla sa tuple mar an gcéanna. Chuireamar roghnach leis
clóscríobh nótaí sa sampla seo:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-10-tuples/src/main.rs}}
```

Ceanglaíonn an athróg `tup` leis an tuple iomlán toisc go meastar tuple a
eilimint cumaisc amháin. Chun na luachanna aonair a bhaint as tuple, is féidir linn
bain úsáid as meaitseáil patrún chun luach tuple a scrios, mar seo:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-11-destructuring-tuples/src/main.rs}}
```
Cruthaíonn an clár seo tuple ar dtús agus ceanglaíonn sé leis an athróg `tup`. Tá sé ansin
úsáideann patrún le `let` chun `tup` a ghlacadh agus é a iompú ina thrí ar leith
athróga, `x`, `y`, agus `z`. Tugtar _destructuring_ air seo toisc go mbriseann sé
an tuple aonair i dtrí chuid. Ar deireadh, priontaí an clár luach na
`y`, atá `6.4`.

Is féidir linn eilimint tuple a rochtain go díreach freisin trí úsáid a bhaint as tréimhse (`.`) ina dhiaidh sin
innéacs an luacha ba mhaith linn a rochtain. Mar shampla:


<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-12-tuple-indexing/src/main.rs}}
```

Cruthaíonn an clár seo an `x` tuple agus ansin rochtain a fháil ar gach eilimint den tuple
ag baint úsáide as a n-innéacsanna faoi seach. Mar is amhlaidh le formhór na dteangacha ríomhchlárúcháin, an chéad cheann
Is é 0 innéacs i tuple.

Tá ainm speisialta ar an tuple gan luachanna, _unit_. An luach seo agus a
tá an dá chineál comhfhreagrach scríofa `()` agus seasann siad do luach folamh nó luach
cineál fillte folamh. Go hintuigthe tugann na habairtí an luach aonaid ar ais mura ndéanann siad
aon luach eile a thabhairt ar ais.

#### An Cineál Eagar

Bealach eile le bailiúchán illuachanna a bheith agat is ea _array_. Murab ionann
tuple, ní mór go mbeadh an cineál céanna ag gach eilimint d'eagar. Murab ionann agus arrays i
roinnt teangacha eile, tá fad seasta ag eagair i Rust.

Scríobhaimid na luachanna in eagar mar liosta camóg-scartha taobh istigh de chearnóg
lúibíní:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-13-arrays/src/main.rs}}
```

Bíonn eagair úsáideach nuair is mian leat do shonraí a leithdháileadh ar an gcruach, mar a chéile
na cineálacha eile atá feicthe againn go dtí seo, seachas an gcarn (beidh muid ag plé na
chairn agus an gcarn níos mó i [Caibidil 4][stack-and-heap]<!-- neamhaird -->) nó nuair
ba mhaith leat a chinntiú go mbíonn líon seasta eilimintí agat i gcónaí. Níl eagar mar
solúbtha mar an cineál veicteora, áfach. Is cineál bailiúcháin den chineál céanna é _veicteoir_
ar fáil ag an leabharlann chaighdeánach a _is_ cead chun fás nó crapadh i méid. Más rud é
níl tú cinnte cé acu eagar nó veicteoir a úsáid, seans gur cheart duit a
veicteoir. [Caibidil 8][vectors] <!-- neamhaird --> pléitear veicteoirí níos mine.

Mar sin féin, tá arrays níos úsáidí nuair a fhios agat ar líon na n-eilimintí nach mbeidh
gá a athrú. Mar shampla, má bhí tú ag baint úsáide as ainmneacha na míosa i
ríomhchlár, is dócha go n-úsáidfeá eagar seachas veicteoir mar is eol duit
beidh 12 eilimint ann i gcónaí:

```rust
let míonna = ["Eanáir", "Feabhra", "Márta", "Aibreán", "Bealtaine", "Meitheamh", "Iúil",
 "Lúnasa", "Meán Fómhair", "Deireadh Fómhair", "Samhain", "Nollaig"];
```

Scríobhann tú cineál eagar ag baint úsáide as lúibíní cearnacha le cineál gach dúil,
leathstad, agus ansin líon na n-eilimintí san eagar, mar seo:

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```
Anseo, is é `i32` an cineál gach eilimint. Tar éis an leathstad, an uimhir `5`
Léiríonn an eagar go bhfuil cúig eilimint.

Is féidir leat freisin eagar a thúsú chun an luach céanna a bheith ann do gach eilimint trí
ag sonrú an luach tosaigh, agus leathstad ina dhiaidh sin, agus ansin fad
an t-eagar idir lúibíní cearnacha, mar a thaispeántar anseo:

```rust
let a = [3; 5];
```


San eagar darb ainm `a` beidh gnéithe `5` a shocrófar ar fad ar an luach
`3` ar dtús. Tá sé seo mar an gcéanna le scríobh `let a = [3, 3, 3, 3, 3];` ach in a
bhealach níos gonta.

##### Rochtain a fháil ar Eilimintí Eagar

Is éard atá in eagar ná smután amháin de chuimhne ar mhéid aitheanta seasta agus is féidir a bheith
leithroinnte ar an chairn. Is féidir leat teacht ar eilimintí d'eagar trí úsáid a bhaint as innéacsú,
mar seo:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-14-array-indexing/src/main.rs}}
```

Sa sampla seo, gheobhaidh an athróg darb ainm `first` an luach `1` mar sin
is é an luach ag innéacs `[0]` san eagar. Gheobhaidh an athróg darb ainm `second`
an luach `2` ón innéacs `[1]` san eagar.

##### Rochtain Neamhbhailí ar Eilimint Eagar

Feicfimid cad a tharlóidh má dhéanann tú iarracht rochtain a fháil ar eilimint d'eagar atá caite
deireadh an eagar. Abair go ritheann tú an cód seo, cosúil leis an gcluiche buille faoi thuairim i
Caibidil 2, chun innéacs eagair a fháil ón úsáideoir:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust,ignore,panics
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-15-invalid-array-access/src/main.rs}}
```

D'éirigh leis an gcód seo a thiomsú. Má ritheann tú an cód seo ag baint úsáide as `cargo run` agus
cuir isteach `0`, `1`, `2`,`3`, nó `4`, priontálfaidh an clár an ceann comhfhreagrach
luach ag an innéacs sin san eagar. Má chuireann tú isteach ina ionad sin uimhir thar dheireadh na
an eagar, mar `10`, feicfidh tú aschur mar seo:

<!-- manual-regeneration
cd listings/ch03-common-programming-concepts/no-listing-15-invalid-array-access
cargo run
10
-->

```console
thread 'main' panicked at src/main.rs:19:19:
index out of bounds: the len is 5 but the index is 10
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

Bhí earráid _runtime_ mar thoradh ar an gclár nuair a úsáideadh neamhbhailí
luach san oibríocht innéacsaithe. Chuaigh an clár amach le teachtaireacht earráide agus
níor rith an ráiteas `println!` deiridh. Nuair a dhéanann tú iarracht rochtain a fháil ar
eilimint ag baint úsáide as innéacsú, seiceálfaidh Rust go bhfuil an t-innéacs a shonraigh tú níos lú
ná an fad eagar. Má tá an t-innéacs níos mó ná nó cothrom leis an fad,
Beidh meirge scaoll. Caithfidh an tseiceáil seo tarlú ag am rite, go háirithe sa chás seo,
mar ní féidir a fhios ag an tiomsaitheoir cén luach a chuirfidh úsáideoir isteach nuair a bheidh sé
rith an cód níos déanaí.

Is sampla é seo de phrionsabail sábháilteachta cuimhne Rust i ngníomh. I go leor
teangacha ísealleibhéil, ní dhéantar seiceáil den chineál seo, agus nuair a chuireann tú seiceáil ar fáil
innéacs mícheart, is féidir rochtain a fháil ar chuimhne neamhbhailí. Cosnaíonn meirge tú ina choinne seo
cineál earráide trí dhul amach láithreach in ionad an rochtain chuimhne a cheadú agus
ag leanúint. Pléann Caibidil 9 níos mó de láimhseáil earráidí Rust agus conas is féidir leat
scríobh cód inléite, sábháilte nach scaoll ná nach gceadaíonn rochtain neamhbhailí ar chuimhne.



[comparing-the-guess-to-the-secret-number]: ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number
[twos-complement]: https://en.wikipedia.org/wiki/Two%27s_complement
[control-flow]: ch03-05-control-flow.html#control-flow
[strings]: ch08-02-strings.html#storing-utf-8-encoded-text-with-strings
[stack-and-heap]: ch04-01-what-is-ownership.html#the-stack-and-the-heap
[vectors]: ch08-01-vectors.html
[unrecoverable-errors-with-panic]: ch09-01-unrecoverable-errors-with-panic.html
[appendix_b]: appendix-02-operators.md