## Conas a Reáchtáiltear Tástálacha a Rialú

Díreach mar a thiomsaíonn `cargo run` do chód agus ansin ritheann sé an dénártha iarmhartach,
Tiomsaíonn `cargo test` do chód sa mhód tástála agus ritheann sé an tástáil iarmhartach
dhénártha. Is é iompar réamhshocraithe an dhénártha a tháirgtear le `cargo test` a rith
na tástálacha go léir go comhthreomhar agus an t-aschur gabhála a ghintear le linn rití tástála,
an t-aschur a chosc ó bheith ar taispeáint agus é a dhéanamh níos éasca an t-aschur a léamh
aschur a bhaineann leis na torthaí tástála. Is féidir leat, áfach, ordú a shonrú
roghanna chun an t-iompar réamhshocraithe seo a athrú.

Téann roinnt roghanna na n-orduithe chuig `cargo test`, agus téann cuid acu chuig an tástáil iarmhartach
dhénártha. Chun an dá chineál argóintí seo a scaradh, liostaíonn tú na hargóintí sin
téigh go dtí `cargo test` agus ansin an deighilteoir `--` agus ansin na cinn a théann go dtí
an dénártha tástála. Agus `cargo test --help` á rith, taispeántar na roghanna is féidir leat a úsáid
le `cargo test`, agus ag rith `cargo test -- --help` taispeántar na roghanna atá agat
Is féidir úsáid a bhaint as tar éis an deighilteoir. Déantar na roghanna sin a dhoiciméadú freisin i atlt [na “Tástálacha”][tástálacha] den [leabhar rustc][rustc].

[tástálacha]: https://doc.rust-lang.org/rustc/tests/index.html
[rustc]: https://doc.rust-lang.org/rustc/index.html

### Trialacha a Reáchtáil go Comhuaineach nó i ndiaidh a chéile

Nuair a ritheann tú tástálacha iolracha, de réir réamhshocraithe ritheann siad go comhthreomhar ag baint úsáide as snáitheanna,
rud a chiallaíonn go gcríochnaíonn siad ag rith níos tapúla agus go bhfaigheann tú aiseolas níos tapúla. Toisc go bhfuil an
tá tástálacha ar siúl ag an am céanna, ní mór duit a chinntiú nach mbraitheann do thástálacha
ar a chéile nó ar aon stát comhroinnte, lena n-áirítear timpeallacht chomhroinnte, mar shampla
an t-eolaire oibre reatha nó na hathróga timpeallachta.

Mar shampla, abair go ritheann gach ceann de do thástálacha cód éigin a chruthaíonn comhad ar diosca
ainmnithe _test-output.txt_ agus scríobhann sé roinnt sonraí chuig an gcomhad sin. Ansin léann gach tástáil
na sonraí sa chomhad sin agus dearbhaíonn sé go bhfuil luach áirithe sa chomhad,
atá difriúil i ngach tástáil. Toisc go ritheann na tástálacha ag an am céanna, ceann amháin
d'fhéadfadh an tástáil an comhad a fhorscríobh san am idir triail eile a scríobh agus
ag léamh an chomhaid. Beidh an dara tástáil theipeann ansin, ní toisc go bhfuil an cód
mícheart ach toisc gur chuir na tástálacha isteach ar a chéile agus iad ar siúl
i gcomhthreo. Réiteach amháin is ea a chinntiú go scríobhann gach tástáil chuig comhad eile;
réiteach eile is ea na tástálacha a rith ceann i ndiaidh a chéile.

Más rud é nach bhfuil tú ag iarraidh na tástálacha a reáchtáil ag an am céanna nó más mian leat níos míne
smacht a fháil ar líon na snáitheanna a úsáidtear, is féidir leat an bhratach `--test-threads` a sheoladh
agus líon na snáitheanna is mian leat a úsáid don dénártha tástála. Féach ar
an sampla seo a leanas:

```console
$ cargo test -- --test-threads=1
```

Shocraigh muid líon na snáitheanna tástála go `1`, ag rá leis an gclár gan úsáid a bhaint as
comhthreomhaireacht. Tógfaidh sé níos mó ama ná rith na tástálacha ag baint úsáide as snáithe amháin
iad ag an am céanna, ach ní chuirfidh na tástálacha isteach ar a chéile má roinneann siad
stáit.

### Aschur Feidhme á Thaispeáint

De réir réamhshocraithe, má éiríonn le tástáil, gabhann leabharlann tástála Rust aon rud a phriontáiltear chuige
aschur caighdeánach. Mar shampla, má thugaimid `println!` i dtástáil agus sa triail
Gabhann, ní fheicfimid an t-aschur `println!` sa teirminéal; ní fheicfimid ach an
líne a léiríonn an tástáil a ritheadh. Má theipeann ar thástáil, feicfimid cibé rud a bhí ann
clóite go dtí aschur caighdeánach leis an gcuid eile den teachtaireacht teip.

Mar shampla, tá feidhm amaideach ag Liostú 11-10 a phrionnaíonn luach a chuid
paraiméadar agus tuairisceáin 10, chomh maith le tástáil a éiríonn agus tástáil a theipeann.

<Listing number="11-10" file-name="src/lib.rs" caption="Tests for a function that calls `println!`">

```rust,panics,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/listing-11-10/src/lib.rs}}
```

</Listing>

Nuair a dhéanaimid na tástálacha seo le `cargo test`, feicfidh muid an t-aschur seo a leanas:

```console
{{#include ../../listings/ch11-writing-automated-tests/listing-11-10/output.txt}}
```

Tabhair faoi deara nach bhfeicimid `I got the value 4`, mar atá
priontáilte nuair a ritheann an tástáil a ritheann. Tá an t-aschur sin gafa. Tá an
aschur ón tástáil ar theip air, `I got the value 8`, le feiceáil sa chuid
den aschur achoimre tástála, a léiríonn freisin cúis an teip tástála.

Más mian linn luachanna clóite a fheiceáil chun tástálacha a rith freisin, is féidir linn a rá le Rust
taispeáin freisin aschur na dtástálacha rathúla le `--show-output`:

```console
$ cargo test -- --show-output
```

Nuair a rithimid na tástálacha i Liostú 11-10 arís leis an mbratach `--show-output`, déanaimid
féach an t-aschur seo a leanas:

```console
{{#include ../../listings/ch11-writing-automated-tests/output-only-01-show-output/output.txt}}
```

### Fothacar Trialacha a Reáchtáil de réir Ainm

Uaireanta, féadann sé go leor ama sraith tástála iomlán a rith. Má tá tú ag obair ar
cód i réimse ar leith, b'fhéidir gur mhaith leat a reáchtáil ach na tástálacha a bhaineann leis
an cód sin. Is féidir leat na tástálacha atá le déanamh a roghnú ach an t-ainm `cargo test` a chur
nó ainmneacha na dtrialacha nó na dtrialacha ar mhaith leat a rith mar argóint.

Chun a léiriú conas fo-thacar tástálacha a rith, cruthóimid trí thástáil ar dtús
ár bhfeidhm `add_two`, mar a thaispeántar i Liostú 11-11, agus roghnaigh na cinn le rith.

<Listing number="11-11" file-name="src/lib.rs" caption="Three tests with three different names">

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/listing-11-11/src/lib.rs}}
```

</Listing>

Má ritheann muid na tástálacha gan dul thar aon argóintí, mar a chonaic muid níos luaithe, go léir an
beidh tástálacha ar siúl ag an am céanna:

```console
{{#include ../../listings/ch11-writing-automated-tests/listing-11-11/output.txt}}
```

#### Trialacha Aonair a Rith

Is féidir linn ainm aon fheidhme tástála a chur ar aghaidh chuig `cargo test` chun an tástáil sin amháin a rith:

```console
{{#include ../../listings/ch11-writing-automated-tests/output-only-02-single-test/output.txt}}
```

Níor rith ach an triail leis an ainm `one_hundred`; níor mheaitseáil an dá thástáil eile
an t-ainm sin. Cuireann an t-aschur tástála in iúl dúinn go raibh níos mó tástálacha againn nár rith leo
ag taispeáint `2 filtered out`  ag an deireadh.

Ní féidir linn ainmneacha tástálacha iolracha a shonrú ar an mbealach seo; ach an chéad luach
a thugtar do `cargo test` úsáidfear é. Ach tá bealach ann chun tástálacha iolracha a rith.

#### Scagadh chun Ilthástálacha a Rith

Is féidir linn cuid d'ainm tástála a shonrú, agus aon tástáil a bhfuil a ainm ag teacht leis an luach sin
reáchtálfar. Mar shampla, toisc go bhfuil `add` in dhá cheann dár dtástálacha, is féidir linn
rith an dá cheann sin trí `cargo test add` a rith:

```console
{{#include ../../listings/ch11-writing-automated-tests/output-only-03-multiple-tests/output.txt}}
```

Rith an t-ordú seo gach tástáil le `add` san ainm agus scagadh amach an triail
darb ainm `one_hundred`. Tabhair faoi deara freisin go n-éiríonn an modúl ina dtaispeántar tástáil
chuid d’ainm na tástála, ionas gur féidir linn na tástálacha go léir a rith i modúl trí scagadh
ar ainm an mhodúil.

### Neamhaird a thabhairt ar Roinnt Trialacha Mura nIarratar Go Sonrach

Uaireanta is féidir le roinnt tástálacha sonracha a bheith an-am-íditheach a fhorghníomhú, mar sin leat
b'fhéidir gur mhaith leo iad a eisiamh le linn an chuid is mó de na `cargo test`. Seachas
liostú mar argóintí na tástálacha go léir ar mhaith leat a rith, is féidir leat an nóta a chur ina ionad sin
tástálacha am-ídeacha ag baint úsáide as an aitreabúid `ignore` chun iad a eisiamh, mar a thaispeántar
anseo:

<span class="filename">Filename: src/lib.rs</span>

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/no-listing-11-ignore-a-test/src/lib.rs:here}}
```

Tar éis `#[test]`, cuirimid an líne `#[ignore]` leis an tástáil ba mhaith linn a eisiamh.
Anois agus ár dtástálacha á reáchtáil againn, ritheann `it_works`, ach ní dhéanann `expensive_test`:

```console
{{#include ../../listings/ch11-writing-automated-tests/no-listing-11-ignore-a-test/output.txt}}
```

Tá an fheidhm `expensive_test` liostaithe mar `ignored`. Más mian linn a rith amháin
na tástálacha a ndearnadh neamhaird orthu, is féidir linn `cargo test -- --ignored` a úsáid:

```console
{{#include ../../listings/ch11-writing-automated-tests/output-only-04-running-ignored/output.txt}}
```

Trí na tástálacha a ritheann a rialú, is féidir leat a chinntiú go mbíonn do thorthaí `cargo test`
cuirfear ar ais go tapa é. Nuair a bhíonn tú ag pointe a bhfuil ciall agat seiceáil
torthaí na dtrialacha `ignored` agus tá am agat fanacht ar na torthaí,
is féidir leat `cargo test -- --ignored` a rith ina ionad sin. Más mian leat na tástálacha go léir a rith
cibé an ndéantar neamhaird orthu nó nach ndéantar, is féidir leat `cargo test -- --include-ignored` a rith.