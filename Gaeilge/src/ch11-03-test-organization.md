## Eagraíocht Tástála

Mar a luadh ag tús na caibidle, is disciplín casta í an tástáil, agus
úsáideann daoine éagsúla téarmaíocht agus eagrú difriúil. An pobal Rust
smaoiníonn sé ar thástálacha i dtéarmaí dhá phríomhchatagóir: tástálacha aonaid agus comhtháthú
tástálacha. Tá _Unit tests_ beag agus níos dírithe, ag tástáil modúl amháin ina aonar
ag an am, agus is féidir comhéadain phríobháideacha a thástáil. Tá _Trialacha Comhtháthaithe_ ar fad
taobh amuigh de do leabharlann agus bain úsáid as do chód ar an mbealach céanna le haon sheachtrach eile
cód, ag baint úsáide as an comhéadan poiblí amháin agus d'fhéadfadh a fheidhmiú iolrach
modúil in aghaidh na tástála.

Scríobh an dá chineál tástálacha tábhachtach chun a chinntiú go bhfuil na píosaí de do
leabharlann ag déanamh a bhfuil tú ag súil leo a dhéanamh, ar leithligh agus le chéile.

### Trialacha Aonaid

Is é cuspóir na dtástálacha aonaid gach aonad cód a thástáil ar leithligh ón
an chuid eile den chód chun a chur in iúl go tapa cá bhfuil agus nach bhfuil an cód ag obair
ag súil. Cuirfidh tú tástálacha aonaid san eolaire _src_ i ngach comhad leis an
cód atá á thástáil acu. Is é an gnás ná modúl darb ainm `tests` a chruthú
i ngach comhad chun na feidhmeanna tástála a chuimsiú agus an modúl a anótáil le
`cfg(test)`.

#### Modúl na dTrialacha agus `#[cfg(test)]`

Insíonn an nóta `#[cfg(test)]` ar an modúl `tests` do Rust a thiomsú agus
ní ritheann an cód tástála ach amháin nuair a ritheann tú `cargo test`, ní nuair a ritheann tú `cargo
build`. Sábhálann sé seo am tiomsaithe nuair nach bhfuil uait ach an leabharlann a thógáil agus
sábhálann sé spás sa déantúsán tiomsaithe dá bharr toisc nach bhfuil na tástálacha
san áireamh. Feicfidh tú é sin toisc go dtéann trialacha comhtháthaithe ar bhealach eile
eolaire, níl an nóta `#[cfg(test)]` ag teastáil uathu. Mar sin féin, mar gheall ar aonad
téann na tástálacha sna comhaid chéanna leis an gcód, úsáidfidh tú `#[cfg(test)]` le sonrú
nár cheart iad a áireamh sa toradh tiomsaithe.

Thabhairt chun cuimhne nuair a ghineamar an tionscadal nua `adder` sa chéad chuid de
sa chaibidil seo, ghin lasta an cód seo dúinn:

<span class="filename">Filename: src/lib.rs</span>

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/listing-11-01/src/lib.rs}}
```

Ar an modúl `tests` a ghintear go huathoibríoch, seasann an aitreabúid `cfg`
_configuration_ agus insíonn sé do Rust nár cheart ach an mhír seo a leanas a chur san áireamh
tugadh rogha cumraíochta áirithe. Sa chás seo, is é an rogha cumraíochta
`test`, a sholáthraíonn Rust chun tástálacha a thiomsú agus a rith. Trí úsáid a bhaint as an
tréith `cfg`, ní thiomsaíonn lasta ár gcód tástála ach amháin má rithimid na tástálacha go gníomhach
le `cargo test`. Áirítear leis seo aon fheidhmeanna cúntóra a d’fhéadfadh a bheith laistigh de seo
modúl, chomh maith leis na feidhmeanna atá anótáilte le `#[test]`.

#### Feidhmeanna Príobháideacha a Thástáil

Tá díospóireacht ar siúl laistigh den phobal tástála faoi cé acu príobháideach nó nach ea
ba cheart feidhmeanna a thástáil go díreach, agus déanann teangacha eile deacrachtaí nó
dodhéanta feidhmeanna príobháideacha a thástáil. Beag beann ar a thástáil idé-eolaíocht tú
cloí leis, ceadaíonn rialacha príobháideachais Rust duit feidhmeanna príobháideacha a thástáil.
Smaoinigh ar an gcód i Liostú 11-12 leis an bhfeidhm phríobháideach `internal_adder`.

<Listing number="11-12" file-name="src/lib.rs" caption="Testing a private function">

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/listing-11-12/src/lib.rs}}
```

</Listing>

Tabhair faoi deara nach bhfuil an fheidhm `internal_adder` marcáilte mar `pub`. Tá tástálacha díreach
Cód meirge, agus níl sa mhodúl `tests` ach modúl eile. Mar a phléamar i
na [“Cosáin chun Tagairt a Dhéanamh do Mhír i gCrann an Mhodúil”][paths]<!-- déan neamhaird de -->
alt, is féidir le míreanna i modúil leanaí na míreanna i modúil a sinsear a úsáid. I
leis an triail seo, tugaimid gach ceann de na míreanna tuismitheora modúl `tests` isteach sa scóip le
`use super::*`, agus ansin is féidir `internal_adder` a ghlaoch ar an tástáil. Mura gceapann tú
ba cheart feidhmeanna príobháideacha a thástáil, níl aon rud i Rust a chuirfidh iallach
leat é sin a dhéanamh.

### Trialacha Comhtháthaithe

I Rust, tá tástálacha lánpháirtithe go hiomlán lasmuigh de do leabharlann. Úsáideann siad do
leabharlann ar an mbealach céanna a bheadh ​​aon chód eile, rud a chiallaíonn nach féidir leo ach glaoch
feidhmeanna atá mar chuid de API poiblí do leabharlainne. Is é an cuspóir a thástáil
cibé an n-oibríonn go leor codanna de do leabharlann le chéile i gceart. Aonaid de chód a
d'fhéadfadh fadhbanna a bheith ag obair i gceart ina n-aonar agus iad comhtháite, mar sin déan tástáil
tá clúdach an chóid chomhtháite tábhachtach freisin. Chun comhtháthú a chruthú
tástálacha, beidh eolaire _tests_ uait ar dtús.

#### Eolaire na _tests_

Cruthaímid eolaire _tests_ ag an leibhéal is airde dár eolaire tionscadail, an chéad cheann eile
go _src_. Tá a fhios ag lasta comhaid tástála comhtháthaithe a chuardach san eolaire seo. muid
ansin is féidir leis an oiread comhaid tástála agus is mian linn a dhéanamh, agus tiomsóidh lasta gach ceann de na
comhaid mar chliabhán aonair.

Déanaimis tástáil chomhtháthaithe. Leis an gcód i Liostú 11-12 fós sa
_src/lib.rs_, déan eolaire _tests_, agus cruthaigh comhad nua darb ainm
_tests/integration_test.rs_. Ba cheart go mbeadh cuma mar seo ar do struchtúr eolaire:

```text
adder
├── Cargo.lock
├── Cargo.toml
├── src
│   └── lib.rs
└── tests
    └── integration_test.rs
```

Cuir isteach an cód i Liostú 11-13 sa chomhad _tests/integration_test.rs_.

<Listing number="11-13" file-name="tests/integration_test.rs" caption="An integration test of a function in the `adder` crate">

```rust,ignore
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/listing-11-13/tests/integration_test.rs}}
```

</Listing>

Is cliathbhosca ar leith é gach comhad san eolaire _tests_, mar sin ní mór dúinn ár gcuid
leabharlann isteach i raon feidhme gach cliathbhosca tástála. Ar an ábhar sin cuirimid `use
adder::add_two;` ag barr an chóid, rud nach raibh ag teastáil uainn sna trialacha aonaid.

Ní gá dúinn aon chód a anótáil in _tests/integration_test.rs_ le
`#[cfg(test)]`. Déileálann lasta go speisialta leis an eolaire _tests_ agus tiomsaíonn sé comhaid
san eolaire seo amháin nuair a rithimid `cargo test`. Rith 'tástáil lasta' anois:

```console
{{#include ../../listings/ch11-writing-automated-tests/listing-11-13/output.txt}}
```

Áirítear ar na trí chuid den aschur na tástálacha aonaid, an tástáil chomhtháthaithe, agus
na tástálacha doc. Tabhair faoi deara má theipeann ar aon tástáil i roinn, na hailt seo a leanas
ní bheidh a rith. Mar shampla, má theipeann ar thástáil aonaid, ní bheidh aon aschur ann
le haghaidh tástálacha comhtháthaithe agus doc toisc nach reáchtálfar na tástálacha sin ach amháin más aonad iad uile
tástálacha ag dul thar.

Tá an chéad chuid do na tástálacha aonaid mar a chéile agus a chonaiceamar: líne amháin
do gach triail aonaid (ceann amháin darb ainm `internal` a chuireamar leis i Liostú 11-12) agus
ansin líne achomair do na tástálacha aonaid.

Tosaíonn an chuid tástálacha comhtháthú leis an líne `Running
tests/integration_test.rs`. Ansin, tá líne le haghaidh gach feidhm tástála i
an tástáil chomhtháthaithe sin agus líne achoimre ar thorthaí an chomhtháthaithe
tástáil díreach sula dtosaíonn an rannán `Doc-tests adder`.

Tá a chuid féin ag gach comhad tástála comhtháthaithe, mar sin má chuirimid níos mó comhad leis an
_tests_ eolaire, beidh níos mó rannóg tástála comhtháthaithe.

Is féidir linn feidhm tástála comhtháthaithe ar leith a rith fós tríd an tástáil a shonrú
ainm na feidhme mar argóint le `cargo test`. Na tástálacha go léir a reáchtáil i a
comhad tástála comhtháthaithe ar leith, bain úsáid as an argóint `--test` ar `cargo test`
agus ainm an chomhaid ina dhiaidh:

```console
{{#include ../../listings/ch11-writing-automated-tests/output-only-05-single-integration/output.txt}}
```

Ní ritheann an t-ordú seo ach na tástálacha sa chomhad _tests/integration_test.rs_.

#### Fomodúil i dTrialacha Comhtháthaithe

De réir mar a chuireann tú níos mó tástálacha comhtháthaithe leis, b'fhéidir gur mhaith leat níos mó comhad a dhéanamh sa
_tests_ eolaire chun cabhrú leo iad a eagrú; mar shampla, is féidir leat an tástáil a ghrúpáil
feidhmeanna ag an bhfeidhmiúlacht atá á thástáil acu. Mar a luadh cheana, gach comhad
san eolaire _tests_ atá tiomsaithe mar chliabhán ar leith dá cuid féin, rud atá úsáideach
chun scóip ar leith a chruthú chun aithris níos mine a dhéanamh ar an mbealach a bheidh úsáideoirí deiridh
ag baint úsáide as do chliabhán. Mar sin féin, ciallaíonn sé seo nach ndéanann comhaid san eolaire _tests_
déan an t-iompar céanna le comhaid in _src_ a dhéanamh, mar a d'fhoghlaim tú i gCaibidil 7
maidir le conas cód a dheighilt i modúil agus comhaid.

Tá iompar éagsúil comhad eolaire _tests_ níos suntasaí nuair a bhíonn tú
sraith feidhmeanna cúntóra a bheith acu le húsáid i gcomhaid tástála comhtháthaithe iolracha agus
déanann tú iarracht na céimeanna a leanúint sa [“Modúil a Scaradh ina Modúil Éagsúla
Comhaid”][separating-modules-into-files]<!-- neamhaird --> alt de Chaibidil 7 go
sliocht iad i modúl coiteann. Mar shampla, má chruthaímid _tests/common.rs_
agus feidhm darb ainm `setup` a chur ann, is féidir linn roinnt cód a chur le `setup` sin
ba mhaith linn glaoch ó fheidhmeanna tástála iolracha i gcomhaid tástála iolracha:

<span class="filename">Filename: tests/common.rs</span>

```rust,noplayground
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/no-listing-12-shared-test-code-problem/tests/common.rs}}
```

Nuair a bheidh na tástálacha á reáchtáil againn arís, feicfidh muid alt nua san aschur tástála don
_common.rs_, cé nach bhfuil feidhmeanna tástála ar bith sa chomhad seo ná
ar thugamar an fheidhm `setup` ó áit ar bith:

```console
{{#include ../../listings/ch11-writing-automated-tests/no-listing-12-shared-test-code-problem/output.txt}}
```

Nuair a bhíonn `common` le feiceáil i dtorthaí na dtrialacha agus `running 0 tests` ar taispeáint do
ní hé an rud a bhí uainn. Theastaigh uainn ach roinnt cód a roinnt leis an gceann eile
comhaid tástála comhtháthú. Chun ‘coitianta’ a sheachaint san aschur tástála,
in ionad _tests/common.rs_ a chruthú, cruthóimid _tests/common/mod.rs_. Tá an
Breathnaíonn an eolaire tionscadail mar seo anois:

```text
├── Cargo.lock
├── Cargo.toml
├── src
│   └── lib.rs
└── tests
    ├── common
    │   └── mod.rs
    └── integration_test.rs
```

Is é seo an coinbhinsiún ainmniúcháin níos sine a thuigeann Rust freisin go bhfuil muid
luaite sa ["Cosáin Chomhaid Malartacha"][alt-paths]<!-- neamhaird --> de
Caibidil 7. Agus an comhad á ainmniú ar an mbealach seo, insíonn sé do Rust gan caitheamh leis an modúl `common`
mar chomhad tástála comhtháthaithe. Nuair a bhogaimid an cód feidhme `setup` isteach
_tests/common/mod.rs_ agus scrios an comhad _tests/common.rs_, an chuid sa
ní bheidh aschur tástála le feiceáil a thuilleadh. Comhaid i bhfochomhadlanna na _tástálacha_
ní dhéantar an t-eolaire a thiomsú mar chliabháin ar leith nó tá codanna sa tástáil
aschur.

Tar éis dúinn _tests/common/mod.rs_ a chruthú, is féidir linn é a úsáid ó aon cheann de na
comhaid tástála comhtháthú mar mhodúl. Seo sampla de ‘socrú’ a ghlaoch
feidhm ón tástáil `it_adds_two` in _tests/integration_test.rs_:

<span class="filename">Filename: tests/integration_test.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch11-writing-automated-tests/no-listing-13-fix-shared-test-code-problem/tests/integration_test.rs}}
```

Tabhair faoi deara go bhfuil an dearbhú `mod common;` mar an gcéanna le dearbhú an mhodúil
léirigh muid i Liosta 7-21. Ansin, sa fheidhm tástála, is féidir linn glaoch ar an
`common::setup()`  feidhm.

#### Trialacha Comhtháthaithe le haghaidh cliathbhoscaí Dénártha

Más cliathbhosca dénártha ár dtionscadal nach bhfuil ann ach comhad _src/main.rs_ agus
nach bhfuil comhad _src/lib.rs_, ní féidir linn tástálacha comhtháthú a chruthú sa
_tests_ eolaire agus tabhair na feidhmeanna atá sainithe sa chomhad _src/main.rs_ isteach
scóip le ráiteas `use`. Ní nochtann ach cliathbhoscaí leabharlainne feidhmeanna nach bhfuil eile acu
is féidir cliathbhoscaí a úsáid; cliathbhoscaí dénártha tá sé i gceist a reáchtáil ina n-aonar.

Tá sé seo ar cheann de na cúiseanna go bhfuil tionscadail meirge a sholáthraíonn dénártha a
straightforward _src/main.rs_ comhad a ghlaonn an loighic a chónaíonn sa
_src/lib.rs_ comhad. Ag baint úsáide as an struchtúr sin, tástálacha comhtháthú _can_ tástáil an
cliathbhosca leabharlainne le `use` chun an fheidhmiúlacht thábhachtach a chur ar fáil. Má tá an
oibríonn feidhmiúlacht thábhachtach, an méid beag cód sa _src/main.rs_
oibreoidh an comhad freisin, agus ní gá an méid beag cód sin a thástáil.

## Achoimre

Soláthraíonn gnéithe tástála Rust bealach chun a shonrú conas ba cheart don chód feidhmiú
a chinntiú go leanann sé ag obair mar a bhfuil súil agat, fiú agus tú ag déanamh athruithe. Tástálacha aonaid
codanna éagsúla de leabharlann a fheidhmiú ar leithligh agus is féidir tástáil phríobháideach
sonraí cur chun feidhme. Seiceálann tástálacha comhtháthaithe go bhfuil go leor codanna den leabharlann
oibriú le chéile i gceart, agus úsáideann siad API poiblí na leabharlainne chun an cód a thástáil
ar an mbealach céanna a úsáidfidh cód seachtrach é. Cé go bhfuil córas cineál Rust agus
Cuidíonn rialacha úinéireachta le roinnt cineálacha fabht a chosc, tá tástálacha fós tábhachtach
laghdaigh fabhtanna loighce a bhaineann leis an gcaoi a bhfuiltear ag súil go n-iompróidh do chód.

Déanaimis an t-eolas a d'fhoghlaim tú sa chaibidil seo agus roimhe seo a chomhcheangal
caibidlí a bheith ag obair ar thionscadal!

[paths]: ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html
[separating-modules-into-files]: ch07-05-separating-modules-into-different-files.html
[alt-paths]: ch07-05-separating-modules-into-different-files.html#alternate-file-paths

