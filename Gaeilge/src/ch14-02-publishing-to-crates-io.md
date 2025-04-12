## Foilsitheoireacht Crate go Crates.io

D'úsáideamar pacáistí ó [crates.io](https://crates.io/) <!-- neamhaird --> mar
spleáchais ár dtionscadal, ach is féidir leat do chód a roinnt le daoine eile freisin
trí do phacáistí féin a fhoilsiú. Clárlann na gcliathbhosca ag
[crates.io]( https://crates.io/) <!-- neamhaird --> dáileann an cód foinse
do phacáistí, mar sin go príomha óstálann sé cód foinse oscailte.

Tá gnéithe ag Rust and Cargo a dhéanann do phacáiste foilsithe níos éasca do dhaoine
a aimsiú agus a úsáid. Labhróimid faoi chuid de na gnéithe seo ina dhiaidh sin agus míneoimid ansin
conas pacáiste a fhoilsiú.

### Tráchtanna Doiciméadúcháin Úsáideacha a Dhéanamh

Má dhéantar do phacáistí a dhoiciméadú go cruinn cabhróidh sé seo le húsáideoirí eile a bheith ar an eolas faoi conas agus cathain
iad a úsáid, mar sin is fiú an t-am a infheistiú chun doiciméid a scríobh. I gCaibidil
3, phléamar conas trácht a dhéanamh ar chód meirge ag baint úsáide as dhá slais, `//`. Tá meirge freisin
trácht de chineál ar leith maidir le doiciméadú, ar a dtugtar go caothúil a
_documentation comment_, a ghinfidh doiciméadú HTML. An HTML
taispeánann sé an t-ábhar tuairimí doiciméadú le haghaidh míreanna API poiblí atá beartaithe
do ríomhchláraitheoirí a bhfuil suim acu fios a bheith agat conas do chliabhán a _úsáid_ seachas conas
tá do chliabhán _curtha i bhfeidhm_.

Úsáideann tuairimí doiciméadaithe trí shlis, `///`, in ionad dhá cheann agus tacaíocht
Nodaireacht marcáil síos chun an téacs a fhormáidiú. Cuir tuairimí doiciméadaithe díreach
roimh an mír atá á dhoiciméadú acu. Léiríonn liostú 14-1 tuairimí doiciméadachta
le haghaidh feidhm `add_one` i gcliathbhosca darb ainm `my_crate`.

<Listing number="14-1" file-name="src/lib.rs" caption="A documentation comment for a function">

```rust,ignore
{{#rustdoc_include ../../listings/ch14-more-about-cargo/listing-14-01/src/lib.rs}}
```

</Listing>

Anseo, tugaimid cur síos ar cad a dhéanann an fheidhm `add_one`, tús a
alt leis an gceannteideal `Examples`, agus ansin cuir cód ar fáil a thaispeánann
conas an fheidhm `add_one` a úsáid. Is féidir linn na doiciméid HTML a ghiniúint ó
tráchtann an doiciméadú seo trí `cargo doc` a rith. Ritheann an t-ordú seo an
uirlis `rustdoc` a dháiltear le Rust agus cuireann sé an doiciméadú HTML ginte
san eolaire _target/doc_.

Ar mhaithe le caoithiúlacht, tógfar HTML do do chuid nuair a ritheann tú `cargo doc --open`'
doiciméid reatha an chliabháin (chomh maith leis na doiciméid le haghaidh do chuid
spleáchais an chliabháin) agus oscail an toradh i mbrabhsálaí gréasáin. Déan nascleanúint go dtí an
feidhm `add_one` agus feicfidh tú conas atá an téacs sna tuairimí doiciméadachta
rindreáilte, mar a thaispeántar i bhFíor 14-1:

<img alt="Rendered HTML documentation for the `add_one` function of `my_crate`" src="img/trpl14-01.png" class="center" />

<span class="caption">Fíor 14-1: Doiciméadúchán HTML don `add_one`
feidhm</span>

#### Rannóga a Úsáidtear go Coitianta

D’úsáideamar an ceannteideal Markdown `# Examples` i Liostú 14-1 chun roinn a chruthú
sa HTML leis an teideal "Examples." Seo a leanas roinnt ailt eile a cliathbhoscaí
úsáideann údair go coitianta ina gcuid doiciméad:

- **Panics**: Na cásanna ina bhféadfadh an fheidhm atá á doiciméadú
 scaoll. Ba cheart do ghlaoiteoirí na feidhme nach dteastaíonn uathu a gcláir scaoll
 déan cinnte nach dtugann siad an fheidhm sna cásanna seo.
- **Earráidí**: Má thugann an fheidhm `Result` ar ais, ag cur síos ar na cineálacha
 earráidí a d’fhéadfadh tarlú agus cad iad na coinníollacha a d’fhéadfadh a bheith ina gcúis leis na hearráidí sin
 d'fhéadfadh sé a bheith cabhrach do ghlaoiteoirí ionas gur féidir leo cód a scríobh chun an
 cineálacha éagsúla earráidí ar bhealaí éagsúla.
- **Sábháilteacht**: Má tá an fheidhm 'neamhshábháilte' le glaoch (pléimid neamhshábháilteacht i
 Caibidil 20), ba chóir go mbeadh alt ann a mhíníonn cén fáth a bhfuil an fheidhm neamhshábháilte
 agus ag clúdach na malairtí a bhfuil an fheidhm ag súil go seasfaidh glaoiteoirí leo.

Ní bhíonn na hailt seo go léir ag teastáil ó fhormhór na dtuairimí doiciméadaithe, ach is a
seicliosta maith chun na gnéithe de do chuid úsáideoirí cód a chur i gcuimhne duit
suim acu eolas a fháil faoi.

#### Tuairimí Doiciméadúcháin mar Thrialacha

Is féidir cabhrú le bloic shamplacha de chóid a chur i do thuairimí doiciméadaithe a léiriú
conas do leabharlann a úsáid, agus tá bónas breise ag baint leis sin: ag rith `cargo
test` reáchtálfar na samplaí cód i do dhoiciméadú mar thástálacha! Ní dhéanfaidh aon ní
níos fearr ná doiciméadú le samplaí. Ach níl aon rud níos measa ná samplaí
nach n-oibríonn toisc go bhfuil an cód athraithe ó bhí an doiciméadú
scríofa. Má rithimid `cargo test` leis na doiciméid don `add_one`
fheidhm ó Liostú 14-1, feicfimid roinn sna torthaí tástála mar seo:

<!-- manual-regeneration
cd listings/ch14-more-about-cargo/listing-14-01/
cargo test
copy just the doc-tests section below
-->

```text
   Doc-tests my_crate

running 1 test
test src/lib.rs - add_one (line 5) ... ok

test result: ok. 1 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.27s
```

Anois má athraíonn muid an fheidhm nó an sampla mar sin beidh an `assert_eq!` sa
mar shampla scaoll agus rith `cargo test` arís, feicfidh muid go nglacann na tástálacha doc
go bhfuil an sampla agus an cód as info lena chéile!

#### Ag Trácht ar Mhíreanna Cuimsithe

Cuireann an stíl doc comment `//!` doiciméadú leis an mír ina bhfuil an
tuairimí seachas na míreanna a leanann na tuairimí. Úsáidimid de ghnáth
na tuairimí doc seo taobh istigh den fhréamhchomhad cliathbhosca (_src/lib.rs_ de réir an ghnáis) nó
taobh istigh de mhodúl chun an gcliathbhosca nó an modúl ina iomláine a dhoiciméadú.

Mar shampla, doiciméadú a chur leis a chuireann síos ar chuspóir an `my_crate`
cliathbhosca ina bhfuil an fheidhm `add_one`, cuirimid tuairimí doiciméadaithe leis sin
tosú le `//!` go dtí tús an chomhaid _src/lib.rs_, mar a thaispeántar i Liostú
14-2:

<Listing number="14-2" file-name="src/lib.rs" caption="Documentation for the `my_crate` crate as a whole">

```rust,ignore
{{#rustdoc_include ../../listings/ch14-more-about-cargo/listing-14-02/src/lib.rs:here}}
```

</Listing>

Tabhair faoi deara nach bhfuil aon chód tar éis na líne deiridh a thosaíonn le `//!`. Toisc
chuireamar tús leis na tuairimí le `//!` in ionad `///`, táimid ag doiciméadú na míre
ina bhfuil an trácht seo seachas mír a leanann an nóta tráchta seo. I
sa chás seo, is é an mhír sin an comhad _src/lib.rs_, arb é fréamh an chliabháin é. iad seo
cuireann tuairimí síos ar an gcliathbhosca iomlán.

Nuair a rithimid `cargo doc --open`, taispeánfar na tuairimí seo ar an tosach
leathanach den cháipéisíocht le haghaidh `my_crate` os cionn liosta na míreanna poiblí sa
cliathbhosca, mar a thaispeántar i bhFíor 14-2:

<img alt="Cáipéisíocht HTML soláthraithe le nóta tráchta don chliathán ina iomláine" src="img/trpl14-02.png" class="center" />

<span class="caption">Fíor 14-2: Doiciméadú rindreáilte do `my_crate`,
lena n-áirítear an trácht a dhéanann cur síos ar an gcliathbhosca ina iomláine</span>

Tá tuairimí doiciméadúcháin laistigh de mhíreanna úsáideach chun cur síos a dhéanamh ar chliabháin agus
modúil go háirithe. Úsáid iad le cuspóir iomlán an choimeádáin a mhíniú
cabhrú le do chuid úsáideoirí eagraíocht an chliabháin a thuiscint.

### API Áisiúil Poiblí á heaspórtáil le `pub use`

Is mór an breithniú é struchtúr d’API poiblí agus tú ag foilsiú a
cliathbhosca. Is lú an eolas atá ag daoine a úsáideann do chliabhán ar an struchtúr ná mar atá tú féin
Tá agus b'fhéidir go mbeadh deacracht acu na píosaí is mian leo a úsáid a fháil má tá do chliabhán
tá ordlathas mór modúl aige.

I gCaibidil 7, chlúdaíomar conas míreanna a phoibliú ag baint úsáide as an eochairfhocal `pub`, agus
míreanna a thabhairt isteach i scóip leis an eochairfhocal `use`. Mar sin féin, an struchtúr a
a dhéanann ciall duit agus tú ag forbairt cliathbhosca seans nach mbeadh sé an-áisiúil
do d'úsáideoirí. B'fhéidir gur mhaith leat do struchtúir a eagrú in ordlathas
ina bhfuil leibhéil iolracha, ach ansin daoine atá ag iarraidh cineál atá agat a úsáid
sainmhínithe go domhain san ordlathas d'fhéadfadh sé go mbeadh deacracht ag fáil amach go bhfuil cineál ann.
D'fhéadfadh sé go mbeadh siad buartha freisin go mbeadh orthu `use` a chur isteach
`my_crate::some_module::another_module::UsefulType;`  seachas `use`
`my_crate::UsefulType;`.

Is é an dea-scéal ná mura bhfuil an struchtúr áisiúil do dhaoine eile a úsáid
ó leabharlann eile, ní gá duit d’eagraíocht inmheánach a atheagrú:
ina ionad sin, is féidir leat míreanna a ath-onnmhairiú chun struchtúr poiblí éagsúil a dhéanamh
ó do struchtúr príobháideach trí úsáid a bhaint as `pub use`. Tógann ath-onnmhairiú poiblí
mír in aon áit amháin agus cuireann sé go poiblí é in áit eile, amhail is dá mba
sainithe sa suíomh eile ina ionad sin.

Mar shampla, abair go ndearnamar leabharlann darb ainm `art` chun coincheapa ealaíne a shamhaltú.
Laistigh den leabharlann seo tá dhá mhodúl: modúl `kinds` ina bhfuil dhá enum
darb ainm `PrimaryColor` agus `SecondaryColor` agus modúl `utils` ina bhfuil a
feidhm darb ainm `mix`, mar a thaispeántar i Liostú 14-3:

<Listing number="14-3" file-name="src/lib.rs" caption="Leabharlann `art` le míreanna eagraithe i modúil `kinds` agus `utils`">

```rust,noplayground,test_harness
{{#rustdoc_include ../../listings/ch14-more-about-cargo/listing-14-03/src/lib.rs:here}}
```

</Listing>

Léiríonn Fíor 14-3 cad é an leathanach tosaigh de na doiciméid don chliathbhosca seo
ghintear le `cargo doc` cuma:

<img alt="Cáipéisíocht rindreáilte don chliathán `art` a liostaíonn na modúil `kinds` agus `utils`" src="img/trpl14-03.png" class="center" />

<span class="caption">Fíor 14-3: Leathanach tosaigh na doiciméid le haghaidh `art`
a liostaíonn na modúil `kinds` agus `utils`</span>

Tabhair faoi deara nach bhfuil na cineálacha `PrimaryColor` agus `SecondaryColor` liostaithe ar an
leathanach tosaigh, ná an fheidhm `mix`. Ní mór dúinn `kinds` agus `utils` a chliceáil chun
iad a fheiceáil.

Teastaíonn ráitis `use` ar chliathbhosca eile a bhraitheann ar an leabharlann seo
na míreanna ó `art` a thabhairt isteach sa scóip, ag sonrú struchtúr an mhodúil sin
sainithe faoi láthair. Taispeánann liosta 14-4 sampla de chliabhán a úsáideann an
`PrimaryColor` agus `mix` míreanna ón gcliathbhosca `art`:

<Listing number="14-4" file-name="src/main.rs" caption="Cliathbhosca ag baint úsáide as míreanna an chliabháin `art` agus a struchtúr inmheánach easpórtáilte">

```rust,ignore
{{#rustdoc_include ../../listings/ch14-more-about-cargo/listing-14-04/src/main.rs}}
```

</Listing>


B'éigean d'údar an chóid i Liostú 14-4, a úsáideann an cliathbhosca `art`
déan amach go bhfuil `PrimaryColor` sa mhodúl `kinds` agus go bhfuil `mix` sa mhodúl
modúl `utils`. Tá struchtúr modúil an chliathbhosca `art` níos ábhartha do
forbróirí atá ag obair ar an gcliathbhosca `art` ná dóibh siúd a úsáideann é. An inmheánach
níl aon fhaisnéis úsáideach sa struchtúr do dhuine atá ag iarraidh
tuiscint a fháil ar conas an cliathbhosca `art` a úsáid, ach is cúis le mearbhall mar gheall ar
ní mór d'fhorbróirí a úsáideann é a dhéanamh amach cá háit le breathnú, agus ní mór dóibh an
ainmneacha modúil sna ráitis `use`.

Chun an eagraíocht inmheánach a bhaint den API poiblí, is féidir linn an
cód cliathbhosca `art` i Liostú 14-3 chun ráitis `pub use` a chur leis chun an
míreanna ar an leibhéal is airde, mar a thaispeántar i Liostú 14-5:

<Listing number="14-5" file-name="src/lib.rs" caption="Ag cur ráitis `úsáid tí tábhairne` chun míreanna a athonnmhairiú">

```rust,ignore
{{#rustdoc_include ../../listings/ch14-more-about-cargo/listing-14-05/src/lib.rs:here}}
```

</Listing>

Liostálfar anois na doiciméid API a ghineann `cargo doc` don chliathbhosca seo
agus nasc ath-onnmhairí ar an leathanach tosaigh, mar a thaispeántar i bhFíor 14-4, ag déanamh an
Cineálacha `PrimaryColor` agus `SecondaryColor` agus is fusa teacht ar an bhfeidhm `mix`.

<img alt="Cáipéisíocht rindreáilte don chliathán `art` leis na hathonnmhairí ar an leathanach tosaigh" src="img/trpl14-04.png" class="center" />

<span class="caption">Fíor 14-4: Leathanach tosaigh an doiciméid le haghaidh `art`
a liostaíonn na hathonnmhairí</span>

Is féidir leis an gcliathbhosca `art` fós an struchtúr inmheánach ó Liostú a fheiceáil agus a úsáid
14-3 mar a léirítear i Liosta 14-4, nó is féidir leo an ceann is áisiúla a úsáid
struchtúr i Liostú 14-5, mar a thaispeántar i Liostú 14-6:

<Listing number="14-6" file-name="src/main.rs" caption="Clár a úsáideann na míreanna ath-onnmhairithe ón gcliathbhosca `art`">

```rust,ignore
{{#rustdoc_include ../../listings/ch14-more-about-cargo/listing-14-06/src/main.rs:here}}
```

</Listing>

I gcásanna ina bhfuil go leor modúil neadaithe, ath-onnmhairiú na cineálacha ag an mbarr
leibhéal le `pub use` difríocht shuntasach a dhéanamh i dtaithí na
daoine a bhaineann úsáid as an gcliathbhosca. Úsáid choitianta eile a bhaintear as `pub use` is ea ath-onnmhairiú
sainmhínithe ar spleáchas sa chliathbhosca reatha chun na cliathbhoscaí sin a dhéanamh
sainmhínithe mar chuid de API poiblí do chliabhán.

Is ealaín níos mó ná eolaíocht é struchtúr API poiblí úsáideach a chruthú, agus
is féidir leat athrá chun an API is fearr a oibríonn do d’úsáideoirí a aimsiú. Ag roghnú `pub use` solúbthacht duit maidir leis an gcaoi a struchtúraíonn tú do chliabhán go hinmheánach agus
díchúpláil an struchtúr inmheánach sin ón méid a chuireann tú i láthair d’úsáideoirí. Féach ar
cuid den chód cliathbhoscaí atá suiteáilte agat féachaint an bhfuil a struchtúr inmheánach
difriúil óna API poiblí.

### Cuntas Crates.io a Bhunú

Sular féidir leat cliathbhoscaí ar bith a fhoilsiú, ní mór duit cuntas a chruthú ar
[crates.io]( https://crates.io/) <!-- neamhaird --> agus faigh comhartha API. Chun é sin a dhéanamh,
tabhair cuairt ar an leathanach baile ag [crates.io](https://crates.io/) <!-- neamhaird --> agus logáil isteach
isteach trí chuntas GitHub. (Tá an cuntas GitHub ina riachtanas faoi láthair, ach
seans go dtacódh an suíomh le bealaí eile chun cuntas a chruthú amach anseo.) Uair amháin
tá tú logáilte isteach, tabhair cuairt ar do shocruithe cuntais ag
[https://crates.io/me/]( https://crates.io/me/) <!-- neamhaird --> agus faigh ar ais do
Eochair API. Ansin rith an t-ordú `cargo login` agus greamaigh d'eochair API nuair a iarrtar ort é, mar seo:

```console
$ cargo login
abcdefghijklmnopqrstuvwxyz012345
```

Cuirfidh an t-ordú seo in iúl do cargo faoi do chomhartha API agus stórálfar isteach go háitiúil é
~/.cargo/credentials. Tabhair faoi deara gur _secret_ é an comhartha seo: ná roinn é
le haon duine eile. Má roinneann tú é le duine ar bith ar chúis ar bith, ba cheart duit
é a chúlghairm agus giniúint comhartha nua ar [crates.io](https://crates.io/)<!-- neamhaird
-->.

### Meiteashonraí á gcur le cliathbhosca Nua

Ligean le rá go bhfuil cliathbhosca agat is mian leat a fhoilsiú. Roimh fhoilsiú, beidh ort
roinnt meiteashonraí a chur leis sa rannán `[package]` de _Cargo.toml_ an chliathbhosca
comhad.

Beidh ainm uathúil ag teastáil ó do chliabhán. Agus tú ag obair ar chliabhán go háitiúil,
is féidir leat cliathbhosca a ainmniú cibé rud is mian leat. Mar sin féin, ainmneacha cliathbhoscaí ar
[crates.io](https://crates.io/)<!-- neamhaird --> a leithdháileadh ar an gcéad teacht,
bonn freastail ar an gcéad dul síos. Nuair a ghlactar ainm cliathbhosca, ní féidir le haon duine eile cliathbhosca a fhoilsiú
leis an ainm sin. Sula ndéanann tú iarracht cliathbhosca a fhoilsiú, cuardaigh an t-ainm atá ort
ag iarraidh a úsáid. Má úsáideadh an t-ainm, beidh ort ainm eile a aimsiú agus
cuir an réimse `name` in eagar sa chomhad _Cargo.toml_ faoin rannán `[package]` go
úsáid an t-ainm nua le haghaidh foilsitheoireachta, mar sin:

<span class="filename">Ainm comhaid: Cargo.toml</span>

```toml
[package]
name = "guessing_game"
```

Fiú má tá ainm ar leith roghnaithe agat, nuair a ritheann tú ‘cargo publish’ le foilsiú
an cliathbhosca ag an bpointe seo, gheobhaidh tú rabhadh agus ansin earráid:

<!-- manual-regeneration
cd listings/ch14-more-about-cargo/listing-14-01/
cargo publish
copy just the relevant lines below
-->

```console
$ cargo publish
    Updating crates.io index
warning: manifest has no description, license, license-file, documentation, homepage or repository.
See https://doc.rust-lang.org/cargo/reference/manifest.html#package-metadata for more info.
--snip--
error: failed to publish to registry at https://crates.io

Caused by:
  the remote server responded with an error (status 400 Bad Request): missing or empty metadata fields: description, license. Please see https://doc.rust-lang.org/cargo/reference/manifest.html for more information on configuring these field
```

Earraíonn sé seo toisc go bhfuil roinnt faisnéise ríthábhachtach in easnamh ort: cur síos agus
tá ceadúnas ag teastáil le go mbeidh a fhios ag daoine cad a dhéanann do chliabhán agus faoina bhfuil
téarmaí is féidir leo é a úsáid. In _Cargo.toml_, cuir cur síos nach bhfuil ann ach a
abairt nó dhó, mar go mbeidh sé le feiceáil le do chliabhán sna torthaí cuardaigh. Le haghaidh
sa réimse `license`, ní mór duit luach aitheantóra _cheadúnas_ a thabhairt. Tá an [Linux
Liostaíonn Malartú Sonraí Pacáiste Bogearraí an Fhorais (SPDX)][spdx] na haitheantóirí
is féidir leat é a úsáid don luach seo. Mar shampla, a shonrú go bhfuil do cheadúnas agat
cliathbhosca ag baint úsáide as an gCeadúnas MIT, cuir an t-aitheantóir `MIT` leis:

<span class="filename">Ainm comhaid: Cargo.toml</span>

```toml
[package]
name = "guessing_game"
license = "MIT"
```
Más mian leat ceadúnas a úsáid nach bhfuil le feiceáil sa SPDX, ní mór duit é a chur
téacs an cheadúnais sin i gcomhad, cuir an comhad san áireamh i do thionscadal, agus ansin
úsáid `license-file` chun ainm an chomhaid sin a shonrú in ionad an comhad ceadúnais a úsáid
eochair `license`.

Tá treoir maidir le cén ceadúnas atá oiriúnach do do thionscadal thar an raon feidhme
den leabhar seo. Ceadaíonn go leor daoine sa phobal Rust a gcuid tionscadal sa
ar an mbealach céanna le Rust trí úsáid a bhaint as ceadúnas dé de `MIT OR Apache-2.0`. An cleachtas seo
léiríonn sé gur féidir leat a shonrú freisin aitheantóirí ceadúnais iolrach scartha
ag `OR` chun ceadúnais iolracha a bheith agat do do thionscadal.

Le hainm uathúil, an leagan, do chur síos, agus ceadúnas curtha leis, beidh an
Seans go mbeidh cuma mar seo ar chomhad _Cargo.toml_ do thionscadal atá réidh le foilsiú:

<span class="filename">Filename: Cargo.toml</span>

```toml
[package]
name = "guessing_game"
version = "0.1.0"
edition = "2021"
description = "A fun game where you guess what number the computer has chosen."
license = "MIT OR Apache-2.0"

[dependencies]
```
Déanann [doiciméadú cargo](https://doc.rust-lang.org/cargo/) cur síos ar cheann eile
meiteashonraí is féidir leat a shonrú chun a chinntiú gur féidir le daoine eile do chliabhán a aimsiú agus a úsáid níos mó
go héasca.

### Foilsitheoireacht chuig Crates.io

Anois go bhfuil cuntas cruthaithe agat, shábháil tú do chomhartha API, roghnaigh tú ainm dó
do chliabhán, agus na meiteashonraí riachtanacha sonraithe agat, tá tú réidh le foilsiú!
Uaslódálann foilsiú cliathbhosca leagan ar leith go
[crates.io]( https://crates.io/) <!-- neamhaird --> le húsáid ag daoine eile.

Bí cúramach, mar tá foilsiú _buan_. Ní féidir leis an leagan a bheith riamh
forscríofa, agus ní féidir an cód a scriosadh. Príomhsprioc amháin de
[crates.io]( https://crates.io/) <!-- neamhaird --> chun feidhmiú mar chartlann bhuan
de chód ionas go mbeidh tógáil de gach tionscadal atá ag brath ar cliathbhoscaí ó
[crates.io]( https://crates.io/) <!-- neamhaird --> leanfaidh sé ag obair. Ag ceadú
dá scriosfaí an leagan bheadh ​​sé dodhéanta an sprioc sin a chomhlíonadh. Mar sin féin, tá
gan teorainn le líon na leaganacha cliathbhoscaí is féidir leat a fhoilsiú.

Rith an t-ordú `cargo publish` arís. Ba cheart go n-éireodh leis anois:

<!-- manual-regeneration
go to some valid crate, publish a new version
cargo publish
copy just the relevant lines below
-->

```console
$ cargo publish
    Updating crates.io index
   Packaging guessing_game v0.1.0 (file:///projects/guessing_game)
   Verifying guessing_game v0.1.0 (file:///projects/guessing_game)
   Compiling guessing_game v0.1.0
(file:///projects/guessing_game/target/package/guessing_game-0.1.0)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.19s
   Uploading guessing_game v0.1.0 (file:///projects/guessing_game)
```

Comhghairdeachas! Tá do chód roinnte agat anois le pobal Rust, agus
is féidir le duine ar bith do chliabhán a chur leis go héasca mar spleáchas dá dtionscadal.

### Leagan Nua de Chliathbhosca Reatha a Fhoilsiú

Nuair a bheidh athruithe déanta agat ar do chliabhán agus tú réidh le leagan nua a scaoileadh,
athraíonn tú an luach `version` atá sonraithe i do chomhad _Cargo.toml_ agus
athfhoilsiú. Bain úsáid as na [rialacha maidir le Leagan Séimeantach][semver] le socrú cad is
tá uimhir chuí an chéad leagain eile bunaithe ar na cineálacha athruithe atá déanta agat.
Ansin rith `cargo publish` chun an leagan nua a uaslódáil.

<!-- Seannasc, ná bain -->

<a id="removing-versions-from-cratesio-with-cargo-yank"></a>

### Leaganacha á dtarraingt siar ó Crates.io le `cargo yank`

Cé nach féidir leat leaganacha roimhe seo de chliabhán a bhaint, is féidir leat aon cheann a chosc
tionscadail amach anseo ó chur leo mar spleáchas nua. Tá sé seo úsáideach nuair a
Tá leagan an gcliathbhosca briste ar chúis amháin nó ar chúis eile. I gcásanna den sórt sin, cargo
tacaíonn _yanking_ leagan gcliathbhosca.

Cuireann Yanking a version cosc ​​ar thionscadail nua ó bheith ag brath ar an leagan sin fad a bheidh sé
ag ligean do gach tionscadal reatha atá ag brath air leanúint ar aghaidh. Go bunúsach, a
ciallaíonn yank nach bhriseadh gach tionscadal le _Cargo.lock_, agus aon todhchaí
Ní bhainfidh comhaid _Cargo.lock_ úsáid as an leagan yanked.

Chun leagan de chliathbhosca a yancáil, in eolaire an chliathbhosca atá agat
foilsithe roimhe seo, rith `cargo yank` agus sonraigh an leagan atá uait
yanc. Mar shampla, má tá cliathbhosca darb ainm `guessing_game` foilsithe againn
1.0.1 agus ba mhaith linn é a yank, san eolaire tionscadail do `guessing_game` ba mhaith linn
rith:

<!-- manual-regeneration:
cargo yank carol-test --version 2.1.0
cargo yank carol-test --version 2.1.0 --undo
-->

```console
$ cargo yank --vers 1.0.1
    Updating crates.io index
        Yank guessing_game@1.0.1
```

Trí `--undo` a chur leis an ordú, is féidir leat yank a chealú agus tionscadail a cheadú
chun tosú ag brath ar leagan arís:

```console
$ cargo yank --vers 1.0.1 --undo
    Updating crates.io index
      Unyank guessing_game@1.0.1
```

A yank _ní_ scriosann sé cód ar bith. Ní féidir, mar shampla, é a scriosadh de thaisme
rúin uaslódáilte. Má tharlaíonn sé sin, ní mór duit na rúin sin a athshocrú láithreach.

[spdx]: http://spdx.org/licenses/
[semver]: http://semver.org/

