## Conas Trialacha a Scríobh

Is feidhmeanna Rust iad tástálacha a fhíoraíonn go bhfuil an cód neamhthástála ag feidhmiú i
an modh ionchais. Is gnách go ndéanann coirp na bhfeidhmeanna tástála na trí cinn seo
gníomhartha:

- Socraigh aon sonraí nó stáit atá ag teastáil.
- Rith an cód is mian leat a thástáil.
- Dearbhaigh gurb iad na torthaí a bhfuil tú ag súil leo.

Breathnaímid ar na gnéithe a sholáthraíonn Rust go sonrach chun tástálacha a scríobh
déan na gníomhartha seo, lena n-áirítear an tréith `test`, cúpla macra, agus an
tréith `should_panic`.

### Anatamaíocht na Feidhme Tástála

Ar a simplí, is feidhm í tástáil in Rust atá anótáilte leis an `test`
tréith. Is meiteashonraí iad tréithe faoi phíosaí de chód Meirge; sampla amháin is ea
an tréith `derive` a d'úsáideamar le structs i gCaibidil 5. Feidhm a athrú
isteach i bhfeidhm tástála, cuir `#[test]` ar an líne roimh `fn`. Nuair a ritheann tú do
tástálacha leis an ordú `cargo test`, tógann Rust dénártha rádala tástála a ritheann
na feidhmeanna agus na tuarascálacha anótáilte ar cibé acu an n-éiríonn le gach feidhm tástála nó
theipeann.

Aon uair a dhéanaimid tionscadal leabharlainne nua le Cargo, modúl tástála le tástáil
gintear feidhm ann go huathoibríoch dúinn. Tugann an modúl seo duit a
teimpléad chun do thástálacha a scríobh ionas nach mbeidh ort féachaint suas go cruinn
struchtúr agus comhréir gach uair a chuireann tú tús le tionscadal nua. Is féidir leat an oiread
feidhmeanna tástála breise agus an oiread modúil tástála agus is mian leat!

Fiosróimid roinnt gnéithe den chaoi a n-oibríonn tástálacha trí thástáil a dhéanamh leis an teimpléad
tástáil sula ndéanaimid tástáil iarbhír ar aon chód. Ansin scríobhfaimid roinnt tástálacha sa saol fíor
a thugann roinnt cód scríofa againn agus a dhearbhaíonn go bhfuil a iompar ceart.

Cruthaímid tionscadal leabharlainne nua darb ainm `adder` a chuirfidh dhá uimhir leis:

```console
$ cargo new adder --lib
     Created library `adder` project
$ cd adder
```

Ba cheart go mbeadh cuma ar a bhfuil sa chomhad _src/lib.rs_ i do leabharlann `adder`
Liostáil 11-1.

<Listing number="11-1" file-name="src/lib.rs" caption="The code generated automatically by `cargo new`">

<!-- manual-regeneration
cd listings/ch11-writing-automated-tests
rm -rf listing-11-01
cargo new listing-11-01 --lib --name adder
cd listing-11-01
echo "$ cargo test" > output.txt
RUSTFLAGS="-A unused_variables -A dead_code" RUST_TEST_THREADS=1 cargo test >> output.txt 2>&1
git diff output.txt # commit any relevant changes; discard irrelevant ones
cd ../../..
-->

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/listing-11-01/src/lib.rs}}
```

</Listing>

Tosaíonn an comhad le sampla `add` feidhm, ionas go mbeidh rud éigin againn
a thástáil.

Faoi láthair, dírímid ar an bhfeidhm `it_works` amháin. Tabhair faoi deara an `#[test]`
nóta: léiríonn an tréith seo feidhm tástála, mar sin an tástáil
tá a fhios ag rádala an fheidhm seo a chóireáil mar thástáil. Seans go mbeidh neamhthástáil againn freisin
feidhmeanna sa mhodúl `tests` chun cuidiú le cásanna comónta a shocrú nó le cur i gcrích
oibríochtaí coitianta, mar sin ní mór dúinn a chur in iúl i gcónaí cé na feidhmeanna atá ina dtrialacha.

Úsáideann an comhlacht feidhme samplach an macra `assert_eq!` chun a dhearbhú go bhfuil `result`,
ina bhfuil an toradh ar ghlaoch `add` le 2 agus 2, cothrom le 4. Seo
feidhmíonn dearbhú mar shampla den fhormáid do ghnáththástáil. Rithfimid é
féachaint go n-éiríonn leis an tástáil seo.

Ritheann an t-ordú `cargo test` na tástálacha go léir inár dtionscadal, mar a thaispeántar i Liostú
11-2.

<Listing number="11-2" caption="The output from running the automatically generated test">

```console
{{#include ../../listings/ch11-writing-automated-tests/listing-11-01/output.txt}}
```

</Listing>

Chuir lasta le chéile agus rith an tástáil. Feicimid an líne `running 1 test`. An chéad cheann eile
léiríonn an líne ainm na feidhme tástála ginte, ar a dtugtar `tests::it_works`,
agus go bhfuil toradh na trialach sin `ok`. An achoimre iomlán `test
result: ok.` ciallaíonn sé gur ritheadh ​​na tástálacha go léir, agus an chuid a léann `1
passed; 0 failed` líon na dtrialacha a d'éirigh leo nó ar theip orthu.

Is féidir triail a mharcáil mar thástáil nach dtugtar aird uirthi agus mar sin ní ritheann sé go háirithe
shampla ; clúdóimid é sin sa [“Neamhaird a thabhairt ar Roinnt Trialacha Mura Go Sonrach
Iarrtha”][ignoring]<!-- neamhaird --> alt níos déanaí sa chaibidil seo
nach bhfuil déanta agat anseo, léiríonn an achoimre `0 ignored`.

Baineann an staitistic `0 measured` le tástálacha tagarmhairc a thomhaiseann feidhmíocht.
Níl tástálacha tagarmharcála ar fáil, ón scríbhinn seo, ach amháin i Rust gach oíche. Féach
[na doiciméid faoi thástálacha tagarmharcála][bench] chun tuilleadh a fhoghlaim.

Is féidir linn argóint a chur ar aghaidh chuig an ordú `cargo test` gan ach tástálacha a bhfuil a
oireann an t-ainm le teaghrán; tugtar _filtering_ air seo agus clúdóimid é sin sa
[“Fothacar Trialacha á Rith de réir Ainm”][subset]<!-- neamhaird a dhéanamh ar --> alt. Seo muid
nár scagadh na tástálacha atá á rith, mar sin taispeánann deireadh na hachoimre `0
filtered out`.

Tá an chéad chuid eile den aschur tástála ag tosú ag `Doc-tests adder` le haghaidh an
torthaí aon tástálacha doiciméadachta. Níl aon tástálacha doiciméadaithe againn go fóill,
ach is féidir le Rust aon samplaí cód atá le feiceáil inár ndoiciméadú API a thiomsú.
Cuidíonn an ghné seo le do dhoiciméid agus do chód a choinneáil ar comhchiall! Déanfaimid plé ar conas
scríobh trialacha doiciméadúcháin sa [“Tuairimí Cáipéisíochta mar
Tástálacha”][doc-comments]<!-- neamhaird --> alt de Chaibidil 14. Go dtí seo, beidh muid
neamhaird a dhéanamh den aschur `Doc-tests`.

Tosaímid ar an tástáil a shaincheapadh dár riachtanais féin. Ar dtús, athraigh ainm
an fheidhm `it_works` chuig ainm eile, mar `exploration`, mar sin:

<span class="filename">Filename: src/lib.rs</span>

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/no-listing-01-changing-test-name/src/lib.rs}}
```

Then run `cargo test` again. The output now shows `exploration` instead of
`it_works`:

```console
{{#include ../../listings/ch11-writing-automated-tests/no-listing-01-changing-test-name/output.txt}}
```

Anois cuirfimid triail eile leis, ach an uair seo déanfaimid tástáil a mhainneoidh! Tástálacha
theipeann nuair a scaoll rud éigin sa fheidhm tástála. Reáchtáiltear gach tástáil i gceann nua
snáithe, agus nuair a fheiceann an príomh-snáithe go bhfuil snáithe tástála bás, is é an tástáil
marcáilte mar theip. I gCaibidil 9, labhair muid faoi conas an bealach is simplí chun scaoll
Is é an macra `panic!` a ghlaoch. Cuir isteach an tástáil nua mar fheidhm ainmnithe
`another`, mar sin tá cuma ar do chomhad _src/lib.rs_ Liostú 11-3.

<Listing number="11-3" file-name="src/lib.rs" caption="Adding a second test that will fail because we call the `panic!` macro">

```rust,panics,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/listing-11-03/src/lib.rs}}
```

</Listing>

Rith na tástálacha arís ag úsáid `cargo test`. Ba cheart go mbeadh cuma Liostú ar an aschur
11-4, a thaispeánann gur theip ar ár dtástáil `exploration` agus ar `another`.

<Listing number="11-4" caption="Test results when one test passes and one test fails">

```console
{{#include ../../listings/ch11-writing-automated-tests/listing-11-03/output.txt}}
```

</Listing>

<!-- manual-regeneration
rg panicked listings/ch11-writing-automated-tests/listing-11-03/output.txt
check the line number of the panic matches the line number in the following paragraph
 -->

 In ionad `ok`, taispeánann an líne `test tests::another` `FAILED`. Beirt nua
ailt le feiceáil idir na torthaí aonair agus an achoimre: an chéad
léiríonn sé an chúis mhionsonraithe le gach teip tástála. Sa chás seo, faigheann muid an
sonraí ar theip ar `another` toisc go raibh scaoll air ag 'Make this test fail'` ar
líne 17 sa chomhad _src/lib.rs_. Níl sa chéad chuid eile ach ainmneacha gach duine
na tástálacha a dteipeann orthu, rud atá úsáideach nuair a bhíonn go leor tástálacha agus go leor
aschur tástála teip mhionsonraithe. Is féidir linn an t-ainm tástála teip a úsáid chun rith díreach
an tástáil sin chun é a dhífhabhtú ar bhealach níos éasca; Labhróimid níos mó faoi bhealaí le tástálacha a reáchtáil
an [“Conas a Reáchtáiltear Tástálacha a Rialú”][rialú-conas-a-rithtear na tástálacha]<!-- neamhaird a dhéanamh
--> alt.

Taispeánann an líne achoimre ag an deireadh: tríd is tríd, is é toradh ár dtástála `FAILED`. muid
bhí pas tástála amháin agus teip tástála amháin.

Anois go bhfuil cuma thorthaí na dtástálacha i gcásanna éagsúla feicthe agat,
Breathnaímid ar roinnt macraí seachas `panic!` atá úsáideach i dtrialacha.

### Torthaí á Seiceáil leis an Macra `Asert!`

Tá an macra `assert!`, a sholáthraíonn an leabharlann chaighdeánach, úsáideach nuair is mian leat
chun a chinntiú go meastar riocht éigin i dtástáil go `true`. Tugann muid an
macra `assert!` argóint a dhéanann meastóireacht ar Boole. Má tá an luach
`true`, ní tharlaíonn aon rud agus éiríonn leis an tástáil. Más `false` an luach, beidh an
Glaonn an macra ar `panic!` chun teip a chur ar an tástáil. Ag baint úsáide as an `assert!`
Cuidíonn macra linn seiceáil go bhfuil ár gcód ag feidhmiú ar an mbealach atá beartaithe againn.

I gCaibidil 5, Liosta 5-15, d'úsáideamar struchtúr `Rectangle` agus `can_hold`
modh, a dhéantar arís anseo i Liosta 11-5. Cuirimis an cód seo sa
_src/lib.rs_, ansin scríobh roinnt tástálacha dó ag baint úsáide as an macra `assert!`.

<Listing number="11-5" file-name="src/lib.rs" caption="The `Rectangle` struct and its `can_hold` method from Chapter 5">

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/listing-11-05/src/lib.rs}}
```

</Listing>

Tugann an modh `can_hold` Boole ar ais, rud a chiallaíonn gur cás úsáide foirfe é
don mhacra `asert!`. I Liostáil 11-6, scríobhaimid triail a chleachtann an
modh `can_hold` trí shampla `Rectangle` a chruthú a bhfuil leithead 8 agus
airde 7 agus ag maíomh gur féidir leis sampla eile `Rectangle` a choinneáil
tá leithead 5 agus airde 1 aige.

<Listing number="11-6" file-name="src/lib.rs" caption="A test for `can_hold` that checks whether a larger rectangle can indeed hold a smaller rectangle">

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/listing-11-06/src/lib.rs:here}}
```

</Listing>

Tabhair faoi deara an líne `use super::*;` taobh istigh den mhodúl `tests`. Is é an modúl `tests`
modúl rialta a leanann na gnáthrialacha infheictheachta a chlúdaíomar i gCaibidil
7 sa [“Cosáin chun Tagairt a Dhéanamh do Mhír sa Mhodúl
Crann”][cosáin-le-tagairt-go-mír-sa-crann-mhodúil]<!-- neamhaird -->
alt. Toisc gur modúl istigh é an modúl `tests`, caithfimid an
cód faoi thástáil sa mhodúl seachtrach isteach i raon feidhme an mhodúil istigh. úsáidimid
glob anseo, mar sin tá aon rud a shainímid sa mhodúl seachtrach ar fáil dó seo
modúl `tests`.

D’ainmnigh muid ár dtástáil ‘larger_can_hold_smaller’, agus chruthaíomar an dá cheann
Cásanna `Rectangle` a theastaíonn uainn. Ansin thugamar an macra `assert!` agus
rith sé mar thoradh ar ghlaoch ar `more.can_hold(&smaller)`. Tá an abairt seo
ceaptha a thabhairt ar ais `` fíor, mar sin ba chóir ár tástáil pas a fháil. Faighimis amach!

```console
{{#include ../../listings/ch11-writing-automated-tests/listing-11-06/output.txt}}
```

Ritheann sé! Cuirimis tástáil eile leis, an uair seo á dhearbhú go bhfuil níos lú
ní féidir le dronuilleog dronuilleog níos mó a choinneáil:

<span class="filename">Filename: src/lib.rs</span>

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/no-listing-02-adding-another-rectangle-test/src/lib.rs:here}}
```

Toisc go bhfuil toradh ceart na feidhme `can_hold` sa chás seo `false`,
caithfimid an toradh sin a dhiúltú sula gcuirfimid ar aghaidh chuig an macra `assert!` é. Mar a
Mar thoradh air sin, rithfidh ár dtástáil má fhilleann `can_hold` `false`:

```console
{{#include ../../listings/ch11-writing-automated-tests/no-listing-02-adding-another-rectangle-test/output.txt}}
```

Dhá thástáil a éiríonn! Anois féachaimis cad a tharlóidh dár dtorthaí tástála nuair a dhéanaimid
bug a thabhairt isteach inár gcód. Athróimid cur i bhfeidhm an `can_hold`
trí chomhartha níos lú ná an comhartha a chur in ionad an chomhartha is mó ná é
i gcomparáid leis na leithead:

```rust,not_desired_behavior,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/no-listing-03-introducing-a-bug/src/lib.rs:here}}
```

Táirgeann rith na dtrialacha na nithe seo a leanas anois:

```console
{{#include ../../listings/ch11-writing-automated-tests/no-listing-03-introducing-a-bug/output.txt}}
```

Fuair ​​​​ár tástálacha an fabht! Toisc go bhfuil `larger.width` `8` agus `smaller.width` is
`5`, filleann an chomparáid idir na leithead in `can_hold` anois `false`: níl 8
níos lú ná 5.

### Comhionannas á Thástáil leis na Macraí `assert_eq!` agus `assert_ne!`

Bealach coiteann chun feidhmiúlacht a fhíorú is ea tástáil le haghaidh comhionannais idir an toradh
den chód atá faoi thástáil agus an luach a bhfuil súil agat go dtabharfaidh an cód ar ais. D'fhéadfá
Déan é seo tríd an macra `assert!` a úsáid agus slonn a chur air ag baint úsáide as an
`==` oibreoir. Mar sin féin, tá sé seo chomh coitianta go bhfuil an leabharlann caighdeánach
soláthraíonn sé péire macraí —`assert_eq!` agus `assert_ne!`—chun an triail seo a dhéanamh
níos áisiúla. Déanann na macraí seo comparáid idir dhá argóint ar son comhionannais nó
éagothroime, faoi seach. Déanfaidh siad an dá luach a phriontáil freisin más é an dearbhú
theipeann, rud a fhágann gur fusa _why_ theip ar an tástáil a fheiceáil; a mhalairt, an
Ní thugann macra `assert!` le fios ach go bhfuair sé luach `false` don `==`
léiriú, gan na luachanna ba chúis leis an luach `false` a phriontáil.

I Liostú 11-7, scríobhaimid feidhm darb ainm `add_two` a chuireann `2` lena
paraiméadar, ansin déanaimid tástáil ar an bhfeidhm seo ag baint úsáide as an macra `assert_eq!`.

<Listing number="11-7" file-name="src/lib.rs" caption="Testing the function `add_two` using the `assert_eq!` macro">

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/listing-11-07/src/lib.rs}}
```

</Listing>

Déanaimis seiceáil go n-éiríonn leis!

```console
{{#include ../../listings/ch11-writing-automated-tests/listing-11-07/output.txt}}
```

Cruthaímid athróg darb ainm `result` a choinníonn toradh an ghlao
`add_two(2)`. Ansin cuirimid `result` agus `4` ar aghaidh mar na hargóintí go `assert_eq!`.
Is é an líne aschuir don triail seo ná `test tests::it_adds_two ... ok`, agus an `ok`
téacs le fios go bhfuil ár tástáil a rith!

Cuirimis fabht isteach inár gcód féachaint cén chuma atá ar `assert_eq!` nuair atá sé
theipeann. Athraigh cur i bhfeidhm na feidhme `add_two` chun `3` a chur leis ina ionad sin:

```rust,not_desired_behavior,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/no-listing-04-bug-in-add-two/src/lib.rs:here}}
```

Rith na tástálacha arís:

```console
{{#include ../../listings/ch11-writing-automated-tests/no-listing-04-bug-in-add-two/output.txt}}
```

Fuair ​​​​ár dtástáil an fabht! Theip ar an tástáil `it_adds_two`, agus insíonn an teachtaireacht
dúinn ``assertion `left == right` failed`` agus cad iad na luachanna `left` agus `right`
bhfuil. Cuidíonn an teachtaireacht seo linn tús a chur le dífhabhtaithe: an argóint `left`, áit a raibh againn
ba é an toradh ar ghlaoch `add_two(2)`, ná `5` ach ba é `4` an argóint `right`.
Is féidir leat a shamhlú go mbeadh sé seo cabhrach go háirithe nuair a bhíonn go leor againn
tástálacha ar siúl.

Tabhair faoi deara, i roinnt teangacha agus creataí tástála, na paraiméadair don chomhionannas
Tugtar `expected` agus `actual` ar fheidhmeanna dearbhaithe, agus an t-ord ina bhfuil
sonraímid cúrsaí na n-argóintí. Mar sin féin, i Rust, tugtar `left` agus
`right`, agus an t-ord ina sonraímid an luach a mbeimid ag súil leis agus an luach
is cuma leis an gcód a tháirgtear. D’fhéadfaimis an dearbhú a scríobh sa triail seo mar
`assert_eq!(4, result)`, rud a thabharfadh an teachtaireacht teipe céanna
a thaispeánann `` assertion failed: `(left == right)` ``.

Rachaidh an macra `assert_ne!` mura bhfuil an dá luach a thugaimid dó cothrom agus
teip má tá siad comhionann. Tá an macra seo an-úsáideach i gcásanna nuair nach bhfuilimid cinnte
cén luach _will_, ach tá a fhios againn cad é an luach nár cheart a bheith.
Mar shampla, má táimid ag tástáil feidhm atá ráthaithe a hionchur a athrú
ar bhealach éigin, ach braitheann an bealach a athraítear an t-ionchur ar an lá de
an tseachtain a bhfuil ár dtrialacha á reáchtáil againn, b'fhéidir gurb é an rud is fearr le dearbhú go bhfuil an
nach bhfuil aschur na feidhme comhionann leis an ionchur.

Faoin dromchla, úsáideann na macraí `assert_eq!` agus `assert_ne!` na hoibreoirí
`==` agus `!=`, faoi seach. Nuair a theipeann ar na dearbhuithe, déanann na macraí seo a gcuid
argóintí a úsáideann formáidiú dífhabhtaithe, rud a chiallaíonn go gcaithfidh na luachanna atá á gcur i gcomparáid
na tréithe `PartialEq` agus `Debug` a chur i bhfeidhm. Gach cineál primitive agus an chuid is mó de
cuireann na gnáthchineálacha leabharlainne na tréithe seo i bhfeidhm. Le haghaidh struchtúir agus enums go
a shainíonn tú féin, beidh ort `PartialEq` a chur i bhfeidhm chun comhionannas a dhearbhú
na cineálacha sin. Beidh ort `Debug` a chur i bhfeidhm freisin chun na luachanna a phriontáil nuair a bheidh an
theipeann ar dhearbhú. Toisc gur tréithe díorthaithe iad an dá thréith, mar a luadh i
Ag liostú 5-12 i gCaibidil 5, bíonn sé seo chomh simplí de ghnáth le cur leis an
`#[derive(PartialEq, Debug)]` anótáil le do shainmhíniú struchtúr nó enum. Féach
Aguisín C, [“Tréithe In-Díorthaithe,”][tréithe derivable]<!-- neamhaird a dhéanamh ar --> le haghaidh tuilleadh
sonraí faoi na tréithe seo agus tréithe díorthacha eile.

### Teachtaireachtaí Teip Saincheaptha á gcur leis

Is féidir leat freisin teachtaireacht saincheaptha a phriontáil leis an teachtaireacht teip mar
argóintí roghnacha leis na macraí `assert!`, `assert_eq!`, agus `asert_ne!`. ar bith
argóintí a shonraítear tar éis na hargóintí riachtanacha a chur ar aghaidh chuig an
macra `format!` (a pléadh i gCaibidil 8 sa [“Concatenation with the `+`
Oibreoir nó an `format!`
Macra”][concatenation-with-the--operator-nó-an-format-macra]<!-- neamhaird -->
alt), ionas gur féidir leat teaghrán formáide a chur ar aghaidh ina bhfuil sealbhóirí áitribh `{}` agus
luachanna le dul sna háitsealbhóirí sin. Tá teachtaireachtaí saincheaptha úsáideach le doiciméadú
cad is brí le dearbhú; nuair a theipeann ar thástáil, beidh tuiscint níos fearr agat ar cad é
Is í an fhadhb leis an gcód.

Mar shampla, déarfaimis go bhfuil feidhm againn a thugann beannú do dhaoine de réir ainm agus muid
ag iarraidh a thástáil go bhfuil an t-ainm a chuirimid isteach san fheidhm le feiceáil san aschur:

<span class="filename">Filename: src/lib.rs</span>

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/no-listing-05-greeter/src/lib.rs}}
```

Níl na riachtanais don chlár seo aontaithe go fóill, agus táimid
cinnte go n-athrófar an téacs `Hello` ag tús na Beannachta. muid
chinn nach dteastaíonn uainn go mbeadh orainn an tástáil a nuashonrú nuair a athraíonn na riachtanais,
mar sin in ionad a sheiceáil le haghaidh comhionannais beacht leis an luach ar ais ó na
feidhm `greeting`, ní dhéanfaidh muid ach dearbhú go bhfuil téacs an
paraiméadar ionchuir.

Anois cuirimis fabht isteach sa chód seo trí `greeting` a athrú chun eisiamh
`name` chun a fheiceáil cén chuma atá ar an teip tástála réamhshocraithe:

```rust,not_desired_behavior,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/no-listing-06-greeter-with-bug/src/lib.rs:here}}
```

Táirgeann an tástáil seo a leanas:

```console
{{#include ../../listings/ch11-writing-automated-tests/no-listing-06-greeter-with-bug/output.txt}}
```

Tugann an toradh seo le fios gur theip ar an dearbhú agus cén líne an
tá dearbhú ar siúl. Dhéanfadh teachtaireacht teip níos úsáidí an luach a phriontáil ón
feidhm `greeting`. Cuirimis teachtaireacht teipe saincheaptha leis comhdhéanta d’fhormáid
teaghrán le áitshealbhóir líonta isteach leis an luach iarbhír a fuaireamar ón
feidhm `greeting`:

```rust,ignore
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/no-listing-07-custom-failure-message/src/lib.rs:here}}
```

Anois agus an tástáil á rith againn, gheobhaidh muid teachtaireacht earráide níos faisnéiseach:

```console
{{#include ../../listings/ch11-writing-automated-tests/no-listing-07-custom-failure-message/output.txt}}
```

Is féidir linn an luach a fuaireamar i ndáiríre san aschur tástála a fheiceáil, rud a chabhródh linn
debug cad a tharla in ionad an méid a bhí muid ag súil a tharlóidh.

### Ag seiceáil le haghaidh Panics le `should_panic`

Chomh maith le luachanna fillte a sheiceáil, tá sé tábhachtach a sheiceáil go bhfuil ár gcód
láimhseálann sé coinníollacha earráide agus muid ag súil leis. Mar shampla, smaoinigh ar an gcineál `Guess`
a chruthaíomar i gCaibidil 9, Liosta 9-13. Cód eile a úsáideann `Guess`
ag brath ar an ráthaíocht nach mbeidh ach luachanna sna cásanna `Guess`
idir 1 agus 100. Is féidir linn triail a scríobh a chinntíonn go ndéanfar iarracht a dhéanamh a
`Guess` shampla le luach lasmuigh den raon scaoll.

Déanaimid é seo tríd an tréith `should_panic` a chur lenár bhfeidhm tástála. Tá an
Gabhann tástáil má tá an cód laistigh den fheidhm scaoll; theipeann ar an tástáil má tá an cód
taobh istigh den fheidhm ní scaoll.

Léiríonn liostú 11-8 tástáil a sheiceálann go dtarlaíonn coinníollacha earráide `Guess::new`
 nuair a mbeimid ag súil leo.

<Listing number="11-8" file-name="src/lib.rs" caption="Testing that a condition will cause a `panic!`">

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/listing-11-08/src/lib.rs}}
```

</Listing>

Cuirimid an aitreabúid `#[should_panic]` tar éis an aitreabúid `#[test]` agus
roimh an fheidhm tástála a mbaineann sé léi. Breathnaímid ar an toradh nuair a bheidh an tástáil seo
Gabhann:

```console
{{#include ../../listings/ch11-writing-automated-tests/listing-11-08/output.txt}}
```

Breathnaíonn go maith! Anois tugaimid fabht isteach inár gcód tríd an riocht a bhaint
go rachaidh an fheidhm `new` i scaoll má tá an luach níos mó ná 100:

```rust,not_desired_behavior,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/no-listing-08-guess-with-bug/src/lib.rs:here}}
```

Nuair a rithfimid an tástáil i Liostú 11-8, teipfidh uirthi:

```console
{{#include ../../listings/ch11-writing-automated-tests/no-listing-08-guess-with-bug/output.txt}}
```

Ní fhaighimid teachtaireacht an-chabhrach sa chás seo, ach nuair a fhéachaimid ar an triail
fheidhm, feicimid go bhfuil sé anótáilte le `#[should_panic]`. An teip a fuair muid
Ciallaíonn sé sin nach raibh an cód san fheidhm tástála ina chúis le scaoll.

Is féidir le tástálacha a úsáideann `should_panic` a bheith neamhchruinn. Dhéanfadh tástáil `should_panic`
pas a fháil fiú má tá an scaoll tástála ar chúis eile ón gceann a bhí muid
ag súil. Chun tástálacha `should_panic` a dhéanamh níos cruinne, is féidir linn rogha roghnach a chur leis
paraiméadar `expected` don aitreabúid `should_panic`. Déanfaidh an úim tástála
déan cinnte go bhfuil an téacs curtha ar fáil sa teachtaireacht teip. Mar shampla,
smaoinigh ar an gcód modhnaithe do `Guess` i Liostú 11-9 mar a bhfuil an fheidhm `new`
panics le teachtaireachtaí éagsúla ag brath ar cibé an bhfuil an luach ró-bheag nó
ró-mhór.

<Listing number="11-9" file-name="src/lib.rs" caption="Testing for a `panic!` with a panic message containing a specified substring">

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/listing-11-09/src/lib.rs:here}}
```

</Listing>

Rachaidh an tástáil seo thar mar gheall ar an luach a chuireamar san aitreabúid `should_panic`''s
Fotheaghrán is ea an paraiméadar `expected` den teachtaireacht a thugann an `Guess::new`
scaoll feidhm le . D'fhéadfaimis an teachtaireacht scaoll iomlán a shonraigh muid
ag súil leis, a bheadh ​​sa chás seo a bheith `Guess value must be less than or equal to
100, got 200`. Braitheann an méid a roghnaíonn tú a shonrú ar cé mhéad den scaoll
tá an teachtaireacht uathúil nó dinimiciúil agus cé chomh beacht is mian leat do thástáil a bheith. I seo
cás, tá fotheideal den teachtaireacht scaoll go leor chun a chinntiú go bhfuil an cód sa
feidhmíonn an fheidhm tástála an cás `else if value > 100`.

Féach cad a tharlaíonn nuair a thástáil `should_panic` le teachtaireacht `expected`
theipeann, cuirimis fabht isteach inár gcód arís trí chorpáin an
`if value < 1` agus na bloic `else if value > 100`:

```rust,ignore,not_desired_behavior
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/no-listing-09-guess-with-panic-msg-bug/src/lib.rs:here}}
```

An uair seo nuair a ritheann muid an tástáil `should_panic`, teipfidh sé:

```console
{{#include ../../listings/ch11-writing-automated-tests/no-listing-09-guess-with-panic-msg-bug/output.txt}}
```

Tugann an teachtaireacht teip le fios go ndearna an tástáil seo scaoll go deimhin agus muid ag súil leis,
ach níor chuimsigh an teachtaireacht scaoill an teaghrán ionchais `níos lú ná nó cothrom
go dtí 100`. Ba é an teachtaireacht scaoll a fuair muid sa chás seo ná `Guess value must
a bheith níos mó ná nó cothrom le 1, fuair 200.` Anois is féidir linn tosú figuring amach cén áit
Is é ár fabht!

### Ag baint úsáide as `Result<T, E>` i dTrialacha

Ár tástálacha go dtí seo go léir scaoll nuair a theipeann orthu. Is féidir linn tástálacha a scríobh freisin a úsáideann
`Result<T, E>`! Seo an tástáil ó Liostú 11-1, athscríofa chun `Result<T,
E>` agus seol ar ais `Err` in ionad scaoll a dhéanamh:

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/no-listing-10-result-in-tests/src/lib.rs:here}}
```

Tá an cineál tuairisceáin `Result<(), String>` anois ag an bhfeidhm `it_works`. Sna
comhlacht na feidhme, seachas glaoch ar an `assert_eq!` macra, táimid ar ais
`Ok(())` nuair a éiríonn leis an triail agus `Err` le `String` istigh nuair a bheidh an tástáil
theipeann.

Trialacha a scríobh ionas go dtabharfaidh siad `Result<T, E>` ar do chumas an cheist a úsáid
oibreoir marc i gcorp na tástálacha, is féidir a bheith ina bhealach áisiúil a scríobh
tástálacha ba cheart a theipeann orthu má thugann oibríocht ar bith laistigh díobh leagan `Err` ar ais.

Ní féidir leat an nóta `#[should_panic]` a úsáid ar thástálacha a úsáideann `Result<T,
E>`. Chun a dhearbhú go dtugann oibríocht athróg `Err` ar ais, _ná_ húsáid an
oibreoir comhartha ceiste ar an luach `Result<T, E>`. Ina áit sin, bain úsáid as
`assert!(value.is_err())`.

Anois go bhfuil roinnt bealaí ar eolas agat chun trialacha a scríobh, féachaimis ar a bhfuil ag tarlú
nuair a rithimid ár dtrialacha agus nuair a dhéanaimid iniúchadh ar na roghanna éagsúla is féidir linn a úsáid le `cargo
test`.

[concatenation-with-the--operator-or-the-format-macro]: ch08-02-strings.html#concatenation-with-the--operator-or-the-format-macro
[bench]: ../unstable-book/library-features/test.html
[ignoring]: ch11-02-running-tests.html#ignoring-some-tests-unless-specifically-requested
[subset]: ch11-02-running-tests.html#running-a-subset-of-tests-by-name
[controlling-how-tests-are-run]: ch11-02-running-tests.html#controlling-how-tests-are-run
[derivable-traits]: appendix-03-derivable-traits.html
[doc-comments]: ch14-02-publishing-to-crates-io.html#documentation-comments-as-tests
[paths-for-referring-to-an-item-in-the-module-tree]: ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html