## Snáitheanna a Úsáid chun Cód a Rith ag an Am Céanna

I bhformhór na gcóras oibriúcháin reatha, rithtear cód cláir atá curtha i gcrích i
_phróiseas_, agus bainisteoidh an córas oibriúcháin ilphróisis ag an am céanna.
Laistigh de chlár, is féidir leat codanna neamhspleácha a bheith agat a ritheann ag an am céanna.
Tugtar _snáitheanna_ ar na gnéithe a ritheann na codanna neamhspleácha seo. Mar
shampla, d'fhéadfadh ilshnáitheanna a bheith ag freastalaí gréasáin ionas go bhféadfadh sé freagairt do
níos mó ná iarratas amháin ag an am céanna.

Is féidir feabhas a chur ar fheidhmíocht tríd an ríomhaireacht i do chlár a roinnt ina ilshnáitheanna chun il
tascanna a rith ag an am céanna, ach cuireann sé castacht leis freisin.
Toisc gur féidir le snáitheanna rith ag an am céanna, níl aon ráthaíocht dhúchasach ann faoin
ord ina rithfidh codanna de do chód ar shnáitheanna éagsúla. Is féidir leis seo fadhbanna a chruthú, amhail:

- Coinníollacha rása, áit a bhfuil snáitheanna ag rochtain sonraí nó acmhainní in ord neamhréireach
- Deadlocks, áit a bhfuil dhá shnáithe ag fanacht lena chéile, rud a chuireann cosc ​​ar an dá shnáithe leanúint ar aghaidh
- Fabhtanna nach dtarlaíonn ach i gcásanna áirithe agus atá deacair a atáirgeadh agus a shocrú
go hiontaofa

Déanann Rust iarracht na héifeachtaí diúltacha a bhaineann le snáitheanna a úsáid a mhaolú, ach
tógann cláreagrú i gcomhthéacs ilsnáithe machnamh cúramach fós agus éilíonn sé
struchtúr cód atá difriúil ón gceann atá i gcláir a ritheann i snáithe aonair.

Cuireann teangacha cláreagraithe snáitheanna i bhfeidhm ar chúpla bealach difriúil, agus soláthraíonn go leor
córais oibriúcháin API ar féidir leis an teanga glaoch air chun snáitheanna nua a chruthú.
Úsáideann leabharlann chaighdeánach Rust samhail _1:1_ de chur i bhfeidhm snáithe, áit a
n-úsáideann clár snáithe córais oibriúcháin amháin in aghaidh gach snáithe teanga amháin. Tá
cliathbhoscaí ann a chuireann samhlacha eile snáithe i bhfeidhm a dhéanann comhbhabhtálacha difriúla leis an
tsamhail 1:1. (Soláthraíonn córas neamhshioncrónach Rust, a fheicfimid sa chéad chaibidil eile, cur chuige eile maidir le comhthráthacht chomh maith.)

### Snáithe Nua a Chruthú le `spawn`

Chun snáithe nua a chruthú, glaoimid ar an bhfeidhm `thread::spawn` agus cuirimid dúnadh (labhair muid faoi dhúnadh i gCaibidil 13) air ina bhfuil an cód is mian linn a rith sa snáithe nua. Priontálann an sampla i Liosta 16-1 téacs ó phríomh-
shnáithe agus téacs eile ó shnáithe nua:

<Listing number="16-1" file-name="src/main.rs" caption="Creating a new thread to print one thing while the main thread prints something else">

```rust
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-01/src/main.rs}}
```

</Listing>

Tabhair faoi deara nuair a chríochnaíonn príomhshnáithe cláir Rust, go ndúnfar síos na snáitheanna uile a cruthaíodh, cibé acu an bhfuil siad críochnaithe ag rith nó nach bhfuil. D’fhéadfadh an t-aschur ón gclár seo a bheith beagán difriúil gach uair, ach beidh cuma air cosúil leis an méid seo a leanas:

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the threads running differently rather than
changes in the compiler -->

```text
hi number 1 from the main thread!
hi number 1 from the spawned thread!
hi number 2 from the main thread!
hi number 2 from the spawned thread!
hi number 3 from the main thread!
hi number 3 from the spawned thread!
hi number 4 from the main thread!
hi number 4 from the spawned thread!
hi number 5 from the spawned thread!
```

Cuireann na glaonna chuig `thread::sleep` iallach ar shnáithe a fhorghníomhú a stopadh ar feadh tréimhse ghearr,
rud a ligeann do shnáithe difriúil rith. Is dócha go nglacfaidh na snáitheanna
sealanna, ach níl aon ráthaíocht ann go ndéanfaidh siad amhlaidh: braitheann sé ar an gcaoi a sceidealaíonn do chóras oibriúcháin na snáitheanna. Sa rith seo, priontáladh an príomhshnáithe ar dtús, cé go
bhfuil an ráiteas priontála ón snáithe sceite le feiceáil ar dtús sa chód. Agus cé gur inis muid don snáithe sceite priontáil go dtí go mbeidh `i` 9, níor shroich sé ach 5
sular dhún an príomhshnáithe síos.

Má ritheann tú an cód seo agus mura bhfeiceann tú ach aschur ón bpríomhshnáithe, nó mura bhfeiceann tú aon
fhorluí, déan iarracht na huimhreacha sna raonta a mhéadú chun níos mó deiseanna a chruthú
don chóras oibriúcháin aistriú idir na snáitheanna.

### Ag Fanacht go gCríochnóidh Gach Snáithe ag Úsáid Láimhseálacha `join`

Ní hamháin go stopann an cód i Liostáil 16-1 an snáithe sceite roimh am an chuid is mó den
am mar gheall ar dheireadh an phríomhshnáithe, ach toisc nach bhfuil aon ráthaíocht ann maidir leis an
ord ina ritheann snáitheanna, ní féidir linn a ráthú go mbeidh an snáithe sceite
ag rith ar chor ar bith!

Is féidir linn an fhadhb a bhaineann leis an snáithe sceite gan a bheith ag rith nó ag críochnú roimh am a réiteach
trí luach fillte `thread::spawn` a shábháil in athróg. Is é `JoinHandle` cineál fillte `thread::spawn`. Is luach úinéireachta é `JoinHandle` a fhanfaidh, nuair a
ghlaoimid ar an modh `join` air, go gcríochnóidh a shnáithe. Taispeánann Liostáil 16-2
conas `JoinHandle` an tsnáithe a chruthaíomar i Liostáil 16-1 a úsáid agus
glaoch ar `join` chun a chinntiú go gcríochnaíonn an snáithe sceite sula scoireann `main`:

<Listing number="16-2" file-name="src/main.rs" caption="Saving a `JoinHandle` from `thread::spawn` to guarantee the thread is run to completion">

```rust
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-02/src/main.rs}}
```

</Listing>

Má ghlaonn tú ar `join` ar an láimhseáil, cuirtear bac ar an snáithe atá ag rith faoi láthair go dtí go gcríochnaíonn an
snáithe a léirítear leis an láimhseáil. Má _bhacann_ tú_snáithe,
cé go
gcuirtear cosc ​​ar an snáithe obair a dhéanamh nó imeacht. Ós rud é gur chuireamar an glao
chun `join` i ndiaidh lúb `for` an phríomhshnáithe, ba cheart go
gcuirfí aschur cosúil leis seo ar fáil trí Liosta 16-2 a rith:

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the threads running differently rather than
changes in the compiler -->

```text
hi number 1 from the main thread!
hi number 2 from the main thread!
hi number 1 from the spawned thread!
hi number 3 from the main thread!
hi number 2 from the spawned thread!
hi number 4 from the main thread!
hi number 3 from the spawned thread!
hi number 4 from the spawned thread!
hi number 5 from the spawned thread!
hi number 6 from the spawned thread!
hi number 7 from the spawned thread!
hi number 8 from the spawned thread!
hi number 9 from the spawned thread!
```

Leanann an dá shnáithe ar aghaidh ag malartú, ach fanann an príomhshnáithe mar gheall ar an nglao ar `handle.join()` agus ní chríochnaíonn sé go dtí go mbeidh an snáithe sceite críochnaithe.

Ach féachfaimid cad a tharlaíonn nuair a bhogaimid `handle.join()` ina ionad sin roimh an
lúb `for` i `main`, mar seo:

<Listing file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/no-listing-01-join-too-early/src/main.rs}}
```

</Listing>

Fanfaidh an príomhshnáithe go mbeidh an snáithe sceite críochnaithe agus ansin rithfidh sé a lúb `for`, mar sin ní bheidh an t-aschur idirnasctha a thuilleadh, mar a thaispeántar anseo:

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the threads running differently rather than
changes in the compiler -->

```text
hi number 1 from the spawned thread!
hi number 2 from the spawned thread!
hi number 3 from the spawned thread!
hi number 4 from the spawned thread!
hi number 5 from the spawned thread!
hi number 6 from the spawned thread!
hi number 7 from the spawned thread!
hi number 8 from the spawned thread!
hi number 9 from the spawned thread!
hi number 1 from the main thread!
hi number 2 from the main thread!
hi number 3 from the main thread!
hi number 4 from the main thread!
```

Is féidir le sonraí beaga, amhail an áit a nglaotar ar `join`, tionchar a imirt ar cibé an ritheann do
shnáitheanna ag an am céanna nó nach ritheann.

### Úsáid Dúnta `move` le Snáitheanna

Is minic a úsáidfimid an eochairfhocal `move` le dúnta a chuirtear chuig `thread::spawn` mar go nglacfaidh an dúnadh úinéireacht ar na luachanna a úsáideann sé ón
timpeallacht ansin, rud a aistríonn úinéireacht na luachanna sin ó shnáithe amháin go
snáithe eile. Sa chuid [“Tagairtí a Ghabháil nó Úinéireacht a Bhogadh”][capture]<!-- ignore
--> de Chaibidil 13, phléamar `move` i gcomhthéacs dúnta. Anois,
díreoidh muid níos mó ar an idirghníomhaíocht idir `move` agus `thread::spawn`.

Tabhair faoi deara i Liostáil 16-1 nach nglacann an dúnadh a chuireann muid chuig `thread::spawn` aon
argóintí: nílimid ag úsáid aon sonraí ón bpríomhshnáithe i gcód an tsnáithe
a cruthaíodh. Chun sonraí ón bpríomhshnáithe a úsáid sa snáithe a cruthaíodh, ní mór do dhúnadh an tsnáithe a cruthaíodh na luachanna atá de dhíth air a ghabháil. Taispeánann liostú 16-3 iarracht veicteoir a chruthú sa phríomhshnáithe agus é a úsáid sa snáithe a cruthaíodh. Mar sin féin, ní oibreoidh sé seo go fóill, mar a fheicfidh tú i gceann nóiméid.

<Listing number="16-3" file-name="src/main.rs" caption="Attempting to use a vector created by the main thread in another thread">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-03/src/main.rs}}
```

</Listing>

Úsáideann an dúnadh `v`, mar sin gabhfaidh sé `v` agus déanfaidh sé cuid de thimpeallacht an dúnta de. Ós rud é go ritheann `thread::spawn` an dúnadh seo i snáithe nua, ba cheart go mbeimid in ann rochtain a fháil ar `v` laistigh den snáithe nua sin. Ach nuair a thiomsóimid an sampla seo, faighimid an earráid seo a leanas:

```console
{{#include ../../listings/ch16-fearless-concurrency/listing-16-03/output.txt}}
```
Tugann Rust _infers_ le fios conas `v` a ghabháil, agus toisc nach bhfuil gá ach le tagairt do `v` ag `println!`, déanann an dúnadh iarracht `v` a fháil ar iasacht. Mar sin féin, tá fadhb ann: ní féidir le Rust
a rá cé chomh fada a rithfidh an snáithe sceite, mar sin níl a fhios aige an mbeidh an tagairt
do `v` bailí i gcónaí.

Soláthraíonn Liostáil 16-4 cás a bhfuil seans níos mó ann go mbeidh tagairt ann do `v`
nach mbeidh bailí:

<Listing number="16-4" file-name="src/main.rs" caption="A thread with a closure that attempts to capture a reference to `v` from a main thread that drops `v`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-04/src/main.rs}}
```

</Listing>

Dá mbeadh cead ag Rust an cód seo a rith, tá seans ann go gcuirfí an snáithe sceite sa chúlra láithreach gan é a rith ar chor ar bith. Tá tagairt do `v` istigh sa snáithe sceite, ach scaoileann an príomhsnáithe `v` láithreach, ag baint úsáide as an bhfeidhm `drop` a phléamar i gCaibidil 15. Ansin, nuair a thosaíonn an
snáithe sceite ag rith, níl `v` bailí a thuilleadh, mar sin tá tagairt dó
neamhbhailí freisin. Ó ní hea!

Chun an earráid tiomsaitheora i Liostáil 16-3 a shocrú, is féidir linn comhairle na teachtaireachta earráide a úsáid:

<!-- manual-regeneration
after automatic regeneration, look at listings/ch16-fearless-concurrency/listing-16-03/output.txt and copy the relevant part
-->

```text
help: to force the closure to take ownership of `v` (and any other referenced variables), use the `move` keyword
  |
6 |     let handle = thread::spawn(move || {
  |                                ++++
```

Trí an eochairfhocal `move` a chur leis roimh an dúnadh, cuirimid iallach ar an dúnadh úinéireacht a ghlacadh ar na luachanna atá á n-úsáid aige seachas ligean do Rust a thabhairt i gcrích gur cheart dó na luachanna a fháil ar iasacht. Tiomsófar agus rithfidh an modhnú ar Liostáil 16-3 a thaispeántar i Liostáil
16-5 mar atá beartaithe againn:

<Listing number="16-5" file-name="src/main.rs" caption="Using the `move` keyword to force a closure to take ownership of the values it uses">

```rust
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-05/src/main.rs}}
```

</Listing>

B’fhéidir go mbeadh fonn orainn an rud céanna a thriail chun an cód i Liostáil 16-4 a shocrú áit a raibh an príomhshnáithe ar a dtugtar `drop` trí dhúnadh `move` a úsáid. Mar sin féin, ní oibreoidh an socrú seo mar go bhfuil an rud atá Liostáil 16-4 ag iarraidh a dhéanamh dícheadaithe ar chúis
dhifriúil. Dá gcuirfimis `move` leis an dúnadh, bhogfaimis `v` isteach i dtimpeallacht an
dhúnta, agus ní fhéadfaimis glaoch ar `drop` air sa phríomhshnáithe a thuilleadh. Gheobhaimis an earráid tiomsaitheora seo ina ionad:

```console
{{#include ../../listings/ch16-fearless-concurrency/output-only-01-move-drop/output.txt}}
```

Tá rialacha úinéireachta Rust tar éis sinn a shábháil arís! Fuaireamar earráid ón gcód i
Liostú 16-3 toisc go raibh Rust coimeádach agus nach raibh sé ach ag iasacht `v` don
snáithe, rud a chiallaigh go bhféadfadh an príomhshnáithe tagairt an
tsnáithe a cruthaíodh a chur ar neamhní go teoiriciúil. Trí a rá le Rust úinéireacht `v` a bhogadh chuig an
snáithe a cruthaíodh, táimid ag ráthú do Rust nach n-úsáidfidh an príomhshnáithe `v` a thuilleadh. Má
athraímid Liostú 16-4 ar an mbealach céanna, táimid ag sárú na
rialacha úinéireachta nuair a dhéanaimid iarracht `v` a úsáid sa phríomhshnáithe. Sáraíonn an eochairfhocal `move`
réamhshocrú coimeádach Rust maidir le hiasacht; ní ligeann sé dúinn na
rialacha úinéireachta a shárú.

Le tuiscint bhunúsach ar shnáitheanna agus ar API an tsnáithe, féachaimis ar a
is féidir linn a _dhéanamh_ le snáitheanna.

[capture]: ch13-01-closures.html#capturing-references-or-moving-ownership