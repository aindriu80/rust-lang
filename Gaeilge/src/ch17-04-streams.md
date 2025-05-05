## Sruthanna: Todhchaí i Seicheamh

<!-- Seancheannteidil. Ná bain iad nó d'fhéadfadh naisc briseadh. -->

<a id="streams"></a>

Go dtí seo sa chaibidil seo, táimid cloíte den chuid is mó le todhchaí aonair. Ba é an t-aon eisceacht mhór
a d'úsáideamar ná an cainéal asyncrónach. Cuimhnigh ar an gcaoi ar úsáideamar an glacadóir dár
chainéal asyncrónach níos luaithe sa chaibidil seo sa chuid [“Teachtaireacht
Ag Pasáil”][17-02-messages]<!-- neamhaird -->. Táirgeann an modh async `recv`
seicheamh míreanna le himeacht ama. Is sampla é seo de phatrún i bhfad níos
ginearálta ar a dtugtar _stream_.

Chonaiceamar seicheamh míreanna siar i gCaibidil 13, nuair a d'fhéachamar ar an tréith `Iterator`
sa chuid [An Tréith Iterator agus an Modh `next`][iterator-trait]<!-- neamhaird
-->, ach tá dhá dhifríocht idir atreoraitheoirí agus an glacadóir
cainéil asyncrónach. Is é an chéad difríocht ná am: bíonn athráiteoirí sioncrónach, agus
bíonn glacadóir an chainéil neamhshioncrónach. Is é an dara ceann an API. Agus muid ag obair
go díreach le `Iterator`, glaoimid ar a mhodh sioncrónach `next`. Leis an
sruth `trpl::Receiver` go háirithe, thugamar modh neamhshioncrónach `recv` air ina ionad. Seachas sin, mothaíonn na APIanna seo an-chosúil, agus ní comhtharlú é an chosúlacht sin. Tá sruth cosúil le foirm neamhshioncrónach athrá. Cé go
bhfuil an `trpl::Receiver` ag fanacht go sonrach le teachtaireachtaí a fháil, áfach, tá an
API srutha ginearálta i bhfad níos leithne: soláthraíonn sé an chéad mhír eile ar an
mbealach a dhéanann `Iterator`, ach go neamhshioncrónach.

Ciallaíonn an chosúlacht idir athráiteoirí agus sruthanna i Rust gur féidir linn
sruth a chruthú ó aon athráiteoir. Mar atá le hathráiteoir, is féidir linn oibriú le
sruth trí ghlaoch ar a mhodh `next` agus ansin fanacht leis an aschur, mar atá i Liostáil
17-30.

<Listing number="17-30" caption="Creating a stream from an iterator and printing its values" file-name="src/main.rs">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-30/src/main.rs:stream}}
```

</Listing>

Tosaímid le sraith uimhreacha, a thiontóimid ina n-athráthóir agus ansin glaoimid ar `map` chun na luachanna go léir a dhúbailt. Ansin tiontóimid an t-athráthóir ina shruth
ag baint úsáide as an bhfeidhm `trpl::stream_from_iter`. Ansin, lúbaimid thar na míreanna sa
sruth de réir mar a thagann siad leis an lúb `while let`.

Ar an drochuair, nuair a dhéanaimid iarracht an cód a rith, ní thiomsaíonn sé, ach ina ionad sin tuairiscíonn sé nach bhfuil aon mhodh `next` ar fáil:

<!-- manual-regeneration
cd listings/ch17-async-await/listing-17-30
cargo build
copy only the error output
-->

```console
error[E0599]: no method named `next` found for struct `Iter` in the current scope
  --> src/main.rs:10:40
   |
10 |         while let Some(value) = stream.next().await {
   |                                        ^^^^
   |
   = note: the full type name has been written to 'file:///projects/async_await/target/debug/deps/async_await-9de943556a6001b8.long-type-1281356139287206597.txt'
   = note: consider using `--verbose` to print the full type name to the console
   = help: items from traits can only be used if the trait is in scope
help: the following traits which provide `next` are implemented but not in scope; perhaps you want to import one of them
   |
1  + use crate::trpl::StreamExt;
   |
1  + use futures_util::stream::stream::StreamExt;
   |
1  + use std::iter::Iterator;
   |
1  + use std::str::pattern::Searcher;
   |
help: there is a method `try_next` with a similar name
   |
10 |         while let Some(value) = stream.try_next().await {
   |                                        ~~~~~~~~
```

Mar a mhíníonn an t-aschur seo, is é an chúis atá leis an earráid tiomsaitheora ná go bhfuil an tréith cheart sa raon feidhme ag teastáil uainn chun an modh `next` a úsáid. Agus ár bplé
go dtí seo san áireamh, d'fhéadfá a bheith ag súil go réasúnta gurb é `Stream` an tréith sin, ach is é `StreamExt` atá ann i ndáiríre. Giorrúchán do _extension_, is patrún coitianta é `Ext` i
bphobal Rust chun tréith amháin a shíneadh le tréith eile.

Mínímid na tréithe `Stream` agus `StreamExt` beagán níos mine ag
deireadh na caibidle, ach faoi láthair níl le fios agat ach go sainmhíníonn an tréith `Stream`
comhéadan ísealleibhéil a chomhcheanglaíonn na tréithe `Iterator` agus
`Future` go héifeachtach. Soláthraíonn `StreamExt` sraith APIanna ardleibhéil ar bharr
`Stream`, lena n-áirítear an modh `next` chomh maith le modhanna fóntais eile cosúil
leis na cinn a sholáthraíonn an tréith `Iterator`. Níl `Stream` agus `StreamExt`
mar chuid de leabharlann chaighdeánach Rust fós, ach úsáideann formhór na gcliathbhoscaí éiceachórais an sainmhíniú céanna.

Is é an réiteach ar an earráid tiomsaitheora ná ráiteas `use` a chur leis le haghaidh `trpl::StreamExt`,
mar atá i Liostáil 17-31.

<Listing number="17-31" caption="Successfully using an iterator as the basis for a stream" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-31/src/main.rs:all}}
```

</Listing>

Agus na píosaí sin go léir curtha le chéile, oibríonn an cód seo mar is mian linn! Ina theannta sin, anois go bhfuil `StreamExt` againn, is féidir linn a chuid modhanna fóntais go léir a úsáid, díreach mar a dhéantar le hathraitheoirí. Mar shampla, i Liosta 17-32, úsáidimid an modh `filter` chun gach rud a scagadh amach ach amháin iolraithe de thrí agus cúig.

<Listing number="17-32" caption="Filtering a stream with the `StreamExt::filter` method" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-32/src/main.rs:all}}
```

</Listing>

Ar ndóigh, níl sé seo an-suimiúil, ós rud é go bhféadfaimis an rud céanna a dhéanamh le hathráiteoirí gnáth agus gan aon neamhshioncrónú ar chor ar bith. Féachfaimid ar a
is féidir linn a dhéanamh atá _uathúil_ do shruthanna.

### Sruthanna a Chumadh

Léirítear go leor coincheap go nádúrtha mar shruthanna: míreanna ag teacht ar fáil i
scuaine, píosaí sonraí á dtarraingt de réir a chéile ón gcóras comhad nuair a bhíonn an
tacar sonraí iomlán ró-mhór do thacar sonraí an ríomhaire, nó sonraí ag teacht thar an
líonra le himeacht ama. Ós rud é gur todhchaí iad sruthanna, is féidir linn iad a úsáid le haon
chineál eile todhchaí agus iad a chomhcheangal ar bhealaí suimiúla. Mar shampla, is féidir linn imeachtaí a bhaisc
chun an iomarca glaonna líonra a sheachaint, sosanna ama a shocrú ar sheichimh
oibríochtaí fada, nó imeachtaí comhéadain úsáideora a thógadh chun obair
gan ghá a sheachaint.

Tosaímis trí shruth beag teachtaireachtaí a thógáil mar ionadaí do shruth
sonraí a d'fhéadfaimis a fheiceáil ó WebSocket nó ó phrótacal cumarsáide fíor-ama eile, mar a thaispeántar i Liostáil 17-33.

<Listing number="17-33" caption="Using the `rx` receiver as a `ReceiverStream`" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-33/src/main.rs:all}}
```

</Listing>

Ar dtús, cruthaímid feidhm ar a dtugtar `get_messages` a thugann `impl Stream<Item
= String>` ar ais. Chun é a chur i bhfeidhm, cruthaímid cainéal neamhshioncrónach, lúbaimid thar na chéad 10 litir den aibítir Béarla, agus seolaimid iad trasna an chainéil.

Úsáidimid cineál nua freisin: `ReceiverStream`, a athraíonn an glacadóir `rx` ón `trpl::channel` go `Stream` le modh `next`. Ar ais i `main`, úsáidimid lúb `while let` chun na teachtaireachtaí go léir ón sruth a phriontáil.

Nuair a ritheann muid an cód seo, faighimid na torthaí go díreach a mbeimid ag súil leo:

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the threads running differently rather than
changes in the compiler -->

```text
Message: 'a'
Message: 'b'
Message: 'c'
Message: 'd'
Message: 'e'
Message: 'f'
Message: 'g'
Message: 'h'
Message: 'i'
Message: 'j'
```

Arís, d’fhéadfaimis é seo a dhéanamh leis an ngnáth-API `Receiver` nó fiú leis an ngnáth-API `Iterator`, áfach, mar sin cuirfimid gné leis a éilíonn sruthanna: ag cur teorainn ama leis a bhaineann le gach mír sa sruth, agus moill ar na míreanna a astaíonn muid, mar a thaispeántar i Liostáil 17-34.

<Listing number="17-34" caption="Using the `StreamExt::timeout` method to set a time limit on the items in a stream" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-34/src/main.rs:timeout}}
```

</Listing>

We start by adding a timeout to the stream with the `timeout` method, which
comes from the `StreamExt` trait. Then we update the body of the `while let`
loop, because the stream now returns a `Result`. The `Ok` variant indicates a
message arrived in time; the `Err` variant indicates that the timeout elapsed
before any message arrived. We `match` on that result and either print the
message when we receive it successfully or print a notice about the timeout.
Finally, notice that we pin the messages after applying the timeout to them,
because the timeout helper produces a stream that needs to be pinned to be
polled.

However, because there are no delays between messages, this timeout does not
change the behavior of the program. Let’s add a variable delay to the messages
we send, as shown in Listing 17-35.

<Listing number="17-35" caption="Sending messages through `tx` with an async delay without making `get_messages` an async function" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-35/src/main.rs:messages}}
```

</Listing>

I `get_messages`, úsáidimid an modh athrá `enumerate` leis an eagar `messages` ionas gur féidir linn innéacs gach míre atá á sheoladh againn a fháil mar aon leis an
mír féin. Ansin cuirimid moill 100 milleasoicind i bhfeidhm ar mhíreanna cothrom-innéacs agus moill 300 milleasoicind ar mhíreanna corr-innéacs chun na moilleanna éagsúla a d'fhéadfaimis a fheiceáil ó shruth teachtaireachtaí sa saol réadúil a insamhladh. Ós rud é go bhfuil ár n-am scoir
do 200 milleasoicind, ba cheart go mbeadh tionchar aige seo ar leath na dteachtaireachtaí.

Chun codladh idir theachtaireachtaí sa fheidhm `get_messages` gan bac a chur,
ní mór dúinn async a úsáid. Mar sin féin, ní féidir linn `get_messages` féin a dhéanamh ina fheidhm async,
mar ansin chuirfimis `Future<Output = Stream<Item = String>>` ar ais in ionad `Stream<Item = String>>`. Bheadh ​​ar an nglaoiteoir fanacht
le `get_messages` féin chun rochtain a fháil ar an sruth. Ach cuimhnigh: tarlaíonn gach rud i
dtodhchaí ar leith go líneach; tarlaíonn comhthráthacht idir todhchaí. Dá mbeadh fanacht
le `get_messages` ann, bheadh ​​air na teachtaireachtaí go léir a sheoladh, lena n-áirítear an mhoill codlata
idir gach teachtaireacht, sula bhfillfí an sruth glacadóra. Mar thoradh air sin,
bheadh ​​an t-am scoir gan úsáid. Ní bheadh ​​aon mhoilleanna sa sruth féin;
tharlódh siad go léir sula mbeadh an sruth ar fáil fiú.

Ina áit sin, fágaimid `get_messages` mar fheidhm rialta a thugann sruth ar ais,
agus cruthaímid tasc chun na glaonna `sleep` neamhshioncrónacha a láimhseáil.

> Nóta: Oibríonn glaoch ar `spawn_task` ar an mbealach seo toisc go bhfuil ár
> ham rithe socraithe againn cheana féin; mura mbeadh, chuirfeadh sé scaoll faoi deara. Roghnaíonn cur i bhfeidhm eile
> comhbhabhtálacha difriúla: d'fhéadfadh siad am rithe nua a chruthú agus an scaoll a sheachaint ach
> críochnóidh siad le beagán forchostais bhreise, nó d'fhéadfadh sé nach soláthróidh siad bealach
> neamhspleách chun tascanna a chruthú gan tagairt d'am rithe. Bí cinnte go bhfuil a fhios agat
> cén chomhréiteach atá roghnaithe ag do rith-am agus scríobh do chód dá réir!

Anois tá toradh i bhfad níos suimiúla ag ár gcód. Idir gach péire eile
teachtaireachta, earráid `Problem: Elapsed(())`.

<!-- manual-regeneration
cd listings/ch17-async-await/listing-17-35
cargo run
copy only the program output, *not* the compiler output
-->

```text
Message: 'a'
Problem: Elapsed(())
Message: 'b'
Message: 'c'
Problem: Elapsed(())
Message: 'd'
Message: 'e'
Problem: Elapsed(())
Message: 'f'
Message: 'g'
Problem: Elapsed(())
Message: 'h'
Message: 'i'
Problem: Elapsed(())
Message: 'j'
```

Ní chuireann an t-am scoir cosc ​​ar na teachtaireachtaí teacht sa deireadh. Faighimid fós
na teachtaireachtaí bunaidh go léir, mar go bhfuil ár gcainéal _gan teorainn_: is féidir leis an oiread
teachtaireachtaí agus is féidir linn a fheistiú sa chuimhne a shealbhú. Mura dtagann an teachtaireacht roimh an
am scoir, cuirfidh ár láimhseálaí srutha san áireamh é sin, ach nuair a dhéanann sé suirbhé ar an sruth
arís, d'fhéadfadh an teachtaireacht a bheith tagtha anois.

Is féidir leat iompar difriúil a fháil más gá trí chineálacha eile cainéal nó
cineálacha eile sruthanna a úsáid go ginearálta. Féachfaimid ar cheann acu sin i gcleachtas trí
shruth eatraimh ama a chomhcheangal leis an sruth teachtaireachtaí seo.

### Sruthanna a Chumasc

Ar dtús, cruthaímis sruth eile, a scaoilfidh mír gach milleasoicind má
ligimid dó rith go díreach. Ar mhaithe le simplíocht, is féidir linn an fheidhm `sleep` a úsáid chun
teachtaireacht a sheoladh ar mhoill agus í a chomhcheangal leis an gcur chuige céanna a d'úsáideamar i
`get_messages` chun sruth a chruthú ó chainéal. Is é an difríocht ná go seolfaimid ar ais an comhaireamh eatraimh atá caite an uair seo, mar sin beidh an cineál tuairisceáin `impl Stream<Item = u32>`, agus is féidir linn glaoch ar an bhfeidhm `get_intervals` (féach Liostáil 17-36).

<Listing number="17-36" caption="Creating a stream with a counter that will be emitted once every millisecond" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-36/src/main.rs:intervals}}
```

</Listing>

Tosaímid trí `count` a shainiú sa tasc. (D'fhéadfaimis é a shainiú lasmuigh den
tasc freisin, ach is soiléire raon feidhme aon athróg ar leith a theorannú.) Ansin
cruthaímid lúb gan teorainn. Codlaíonn gach athrá den lúb go haisioncrónach ar feadh
milleasoicind amháin, méadaíonn sé an comhaireamh, agus ansin seolann sé thar an gcainéal é.
Toisc go bhfuil sé seo go léir fillte sa tasc a chruthaigh `spawn_task`, glanfar suas é go léir - lena n-áirítear an lúb gan teorainn - mar aon leis an am rith.

Tá an cineál seo lúb gan teorainn, nach gcríochnaíonn ach amháin nuair a dhéantar an t-am rith iomlán a stróiceadh, sách coitianta i meirge asyncrónach: ní mór do go leor clár leanúint ar aghaidh ag rith
go neamhchinnte. Le haisioncrónach, ní chuireann sé seo bac ar aon rud eile, fad is atá
pointe feithimh amháin ar a laghad i ngach athrá tríd an lúb.

Anois, ar ais i mbloc asyncrónach ár bpríomhfheidhme, is féidir linn iarracht a dhéanamh na sruthanna
`messages` agus `intervals` a chumasc, mar a thaispeántar i Liostáil 17-37.

<Listing number="17-37" caption="Attempting to merge the `messages` and `intervals` streams" file-name="src/main.rs">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-37/src/main.rs:main}}
```

</Listing>

Tosaímid trí ghlaoch ar `get_intervals`. Ansin, déanaimid na sruthanna `messages` agus `intervals` a chumasc leis an modh `merge`, a chomhcheanglaíonn ilshruthanna
i sruth amháin a tháirgeann míreanna ó aon cheann de na sruthanna foinse a luaithe
a bhíonn na míreanna ar fáil, gan aon ordú ar leith a fhorchur. Ar deireadh, déanaimid lúb thar an sruth comhcheangailte sin in ionad thar `messages`.

Ag an bpointe seo, ní gá `messages` ná `intervals` a phionáil ná a athrú,
toisc go gcomhcheanglófar an dá cheann sa sruth `merged` aonair. Mar sin féin, ní
thiomsaíonn an glao seo chun `merge`! (Ní dhéanann an glao `next` sa lúb `while
let` ach an oiread, ach fillfimid ar sin.) Tá sé seo amhlaidh toisc go bhfuil
cineálacha difriúla ag an dá shruth. Tá an cineál `Timeout<impl Stream<Item =
String>>` ag an sruth `messages`, áit a bhfuil `Timeout` an cineál a chuireann `Stream` i bhfeidhm le haghaidh glao `timeout`. Tá an cineál `impl Stream<Item = u32>` ag an sruth `intervals`. Chun an dá shruth seo a chumasc, ní mór dúinn ceann acu a chlaochlú chun go n-oireann sé don cheann eile. Déanfaimid
athoibriú ar an sruth eatraimh, mar go bhfuil teachtaireachtaí cheana féin san fhormáid bhunúsach atá uainn agus caithfidh sé earráidí ama scoir a láimhseáil (féach Liostáil 17-38).

<!-- We cannot directly test this one, because it never stops. -->

<Listing number="17-38" caption="Aligning the type of the the `intervals` stream with the type of the `messages` stream" file-name="src/main.rs">

```rust,ignore
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-38/src/main.rs:main}}
```

</Listing>

Ar dtús, is féidir linn an modh cúnta `map` a úsáid chun na `intervals` a chlaochlú go
teaghrán. Ar an dara dul síos, ní mór dúinn an `Timeout` ó `messages` a mheaitseáil. Ós rud é nach bhfuilimid
i ndáiríre _ag iarraidh_ teorainn ama do `intervals`, áfach, is féidir linn teorainn ama a chruthú
atá níos faide ná na tréimhsí eile atá á n-úsáid againn. Anseo, cruthaímid
tréimhse ama 10 soicind le `Duration::from_secs(10)`. Ar deireadh, ní mór dúinn
`stream` a dhéanamh inathraithe, ionas gur féidir le glaonna `next` an lúb `while let` athrá
tríd an sruth, agus é a phionáil ionas go mbeidh sé sábháilte é sin a dhéanamh. Tugann sé sin _beagnach_
sinn go dtí an áit a gcaithfimid a bheith. Seiceálann gach cineál. Má ritheann tú é seo, áfach,
beidh dhá fhadhb ann. Ar dtús, ní stopfaidh sé choíche! Beidh ort é a stopadh le
<span class="keystroke">ctrl-c</span>. Ar an dara dul síos, beidh na teachtaireachtaí ón aibítir Béarla curtha i measc na dteachtaireachtaí uile maidir le comhaireamh eatraimh:

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the tasks running differently rather than
changes in the compiler -->

```text
--snip--
Interval: 38
Interval: 39
Interval: 40
Message: 'a'
Interval: 41
Interval: 42
Interval: 43
--snip--
```

Taispeánann liostú 17-39 bealach amháin chun an dá fhadhb dheireanacha seo a réiteach.

<Listing number="17-39" caption="Using `throttle` and `take` to manage the merged streams" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-39/src/main.rs:throttle}}
```

</Listing>

Ar dtús, úsáidimid an modh `throttling` ar an sruth `intervals` ionas nach gcuirfidh sé ró-ualach ar an sruth `messages`. Is bealach é _Throttling_ chun an ráta a theorannú ag
a nglaofar ar fheidhm—nó, sa chás seo, cé chomh minic a dhéanfar an sruth a
phoibliú. Ba chóir go ndéanfadh uair amháin gach 100 milleasoicind, mar sin cé chomh minic
a thagann ár dteachtaireachtaí.

Chun líon na míreanna a nglacfaimid ó shruth a theorannú, cuirimid an modh `take` i bhfeidhm ar an sruth `merged`, mar ba mhaith linn an t-aschur deiridh a theorannú, ní hamháin sruth amháin nó an sruth eile.

Anois nuair a ritheann muid an clár, stopann sé tar éis 20 mír a tharraingt ón sruth,
agus ní chuireann na eatraimh ró-ualach ar na teachtaireachtaí. Ní fhaighimid `Interval:
100` ná `Interval: 200` nó mar sin de ach an oiread, ach ina ionad sin faighimid `Interval: 1`, `Interval: 2`,
agus mar sin de—cé go bhfuil sruth foinse againn ar féidir leis imeacht a tháirgeadh gach
mileasoicind. Sin toisc go dtáirgeann an glao `throttle` sruth nua a fhilleann
an sruth bunaidh ionas nach ndéantar poll ar an sruth bunaidh ach ag an ráta
scóip, ní ag a ráta "dúchasach" féin. Níl bunch teachtaireachtaí eatraimh neamhláimhseáilte againn
atá á roghnú againn neamhaird a dhéanamh orthu. Ina áit sin, ní tháirgimid na teachtaireachtaí eatraimh sin riamh sa chéad áit! Seo an "leisciúlacht" dúchasach de thodhchaí Rust
ag obair arís, rud a ligeann dúinn ár dtréithe feidhmíochta a roghnú.

<!-- manual-regeneration
cd listings/ch17-async-await/listing-17-39
cargo run
copy and paste only the program output
-->

```text
Interval: 1
Message: 'a'
Interval: 2
Interval: 3
Problem: Elapsed(())
Interval: 4
Message: 'b'
Interval: 5
Message: 'c'
Interval: 6
Interval: 7
Problem: Elapsed(())
Interval: 8
Message: 'd'
Interval: 9
Message: 'e'
Interval: 10
Interval: 11
Problem: Elapsed(())
Interval: 12
```

Tá rud amháin eile ann a chaithfimid a láimhseáil: earráidí! Leis an dá shruth seo atá bunaithe ar chainéal, d'fhéadfadh na glaonna `send` teip nuair a dhúnann an taobh eile den
chainéal—agus níl ansin ach ceist faoin gcaoi a ndéanann an t-am rith na todhchaí a fhorghníomhú
a dhéanann suas an sruth. Go dtí seo, níor thugamar aird ar an bhféidearthacht seo trí ghlaoch ar
`unwrap`, ach in aip dea-iompartha, ba cheart dúinn an earráid a láimhseáil go sainráite, ar a laghad tríd an lúb a chríochnú ionas nach ndéanaimid iarracht aon teachtaireachtaí eile a sheoladh. Taispeánann liostú
17-40 straitéis earráide simplí: priontáil an cheist agus ansin `break` ó na
lúba.

<Listing number="17-40" caption="Handling errors and shutting down the loops">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-40/src/main.rs:errors}}
```

</Listing>

Mar is gnách, beidh an bealach ceart chun déileáil le hearráid seolta teachtaireachta éagsúil; déan cinnte go bhfuil straitéis agat.

Anois go bhfuil go leor neamhshioncrónacha feicthe againn i gcleachtas, déanaimis céim siar agus déanaimis tochailt isteach i roinnt de na sonraí faoi conas a úsáideann `Future`, `Stream`, agus na príomhthréithe eile a úsáideann Rust chun neamhshioncrón a chur ag obair.

[17-02-messages]: ch17-02-concurrency-with-async.html#message-passing
[iterator-trait]: ch13-02-iterators.html#the-iterator-trait-and-the-next-method	