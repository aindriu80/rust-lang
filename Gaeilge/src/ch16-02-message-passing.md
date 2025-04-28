## Úsáid a bhaint as Tarchur Teachtaireachtaí chun Sonraí a Aistriú idir Snáitheanna

Cur chuige atá ag éirí níos coitianta chun comhthráthacht shábháilte a chinntiú ná _tarchur_teachtaireachta_, áit a ndéanann snáitheanna nó gníomhaithe cumarsáid trí theachtaireachtaí ina bhfuil sonraí a sheoladh chuig a chéile. Seo an smaoineamh i mana ó [dhoiciméadacht teanga Go](https://golang.org/doc/effective_go.html#concurrency):
“Ná déan cumarsáid trí chuimhne a roinnt; ina ionad sin, roinn cuimhne trí chumarsáid.”

Chun comhthráthacht seolta teachtaireachtaí a bhaint amach, soláthraíonn leabharlann chaighdeánach Rust
cur i bhfeidhm de _chainéil_. Is coincheap clársceidealaithe ginearálta é cainéal trína
seoltar sonraí ó shnáithe amháin go snáithe eile.

Is féidir leat cainéal i gclársceidealú a shamhlú mar chainéal treorach uisce, amhail sruthán nó abhainn. Má chuireann tú rud éigin cosúil le lacha rubair
isteach in abhainn, rachaidh sé síos an abhainn go dtí deireadh an uiscebhealaigh.

Tá dhá leath ag cainéal: tarchuradóir agus glacadóir. Is é leath an tarchuradóra
an suíomh suas an abhainn ina gcuireann tú lachain rubair san abhainn, agus is é
leath an ghlacadóra an áit a gcríochnaíonn an lacha rubair síos an abhainn. Glaonn cuid amháin de do
chód modhanna ar an tarchuradóir leis na sonraí is mian leat a sheoladh, agus
seiceálann cuid eile an taobh glacadóra le haghaidh teachtaireachtaí atá ag teacht isteach. Deirtear go bhfuil cainéal
_dúnta_ má scaoiltear leath an tarchuradóra nó an ghlacadóra.

Anseo, oibreoimid suas go dtí clár a bhfuil snáithe amháin ann chun luachanna a ghiniúint agus
iad a sheoladh síos cainéal, agus snáithe eile a gheobhaidh na luachanna agus
a phriontálfaidh amach iad. Seolfaimid luachanna simplí idir snáitheanna ag baint úsáide as cainéal
chun an ghné a léiriú. Nuair a bheidh tú eolach ar an teicníc, d'fhéadfá
cainéil a úsáid le haghaidh aon snáitheanna a gcaithfidh cumarsáid a dhéanamh eatarthu, mar shampla
córas comhrá nó córas ina ndéanann go leor snáitheanna codanna de ríomh
agus na codanna a sheoladh chuig snáithe amháin a chomhiomlánaíonn na torthaí.

Ar dtús, i Liostáil 16-6, cruthóimid cainéal ach ní dhéanaimid aon rud leis. Tabhair faoi deara nach ndéanfar é seo a thiomsú go fóill mar ní féidir le Rust a rá cén cineál luachanna is mian linn a sheoladh thar an gcainéal.

<span class="filename">Filename: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-06/src/main.rs}}
```

<span class="caption">Listing 16-6: Creating a channel and assigning the two
halves to `tx` and `rx`</span>

Cruthaímid cainéal nua ag baint úsáide as an bhfeidhm `mpsc::channel`; seasann `mpsc` do
_multiple producer, single consumer_. Go hachomair, ciallaíonn an chaoi a gcuireann leabharlann chaighdeánach Rust
cainéil i bhfeidhm gur féidir le cainéal il-chríocha _seolta_ a bheith aige a
tháirgeann luachanna ach gan ach críoch _faighte_ amháin a ídíonn na luachanna sin. Samhlaigh
il-shruthanna ag sileadh le chéile in aon abhainn mhór amháin: críochnóidh gach rud a sheoltar síos aon cheann de na
sruthanna in aon abhainn amháin ag an deireadh. Tosaímid le
táirgeoir
amháin faoi láthair, ach cuirfimid il-tháirgeoirí leis nuair a bheidh an sampla seo
ag obair againn.

Tugann an fheidhm `mpsc::channel` tuple ar ais, agus is é an chéad eilimint de an
chríoch seolta—an tarchuradóir—agus is é an dara heilimint an críoch glactha—an
glacadóir. Úsáidtear na giorrúcháin `tx` agus `rx` go traidisiúnta i go leor réimsí
do _transmitter_ agus _receiver_ faoi seach, mar sin ainmnímid ár n-athróga mar sin
chun gach críoch a léiriú. Táimid ag úsáid ráiteas `let` le patrún a scriosann na tuplaí; pléifimid úsáid patrún i ráitis `let` agus dístruchtúrú i gCaibidil 19. Faoi láthair, bíodh a fhios agat gur cur chuige áisiúil é ráiteas `let` a úsáid ar an mbealach seo chun píosaí an tupla a eastóscadh a fhilleann `mpsc::channel`.

Bogfaimid an taobh tarchuir isteach i snáithe sceite agus lig dúinn teaghrán amháin a sheoladh ionas go mbeidh an snáithe sceite ag cumarsáid leis an bpríomhshnáithe, mar a thaispeántar i
Liostú 16-7. Tá sé seo cosúil le lacha rubair a chur san abhainn suas an abhainn nó
teachtaireacht comhrá a sheoladh ó shnáithe amháin go snáithe eile.

<Listing number="16-7" file-name="src/main.rs" caption="Moving `tx` to a spawned thread and sending “hi”">

```rust
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-07/src/main.rs}}
```

</Listing>

Arís, táimid ag úsáid `thread::spawn` chun snáithe nua a chruthú agus ansin ag úsáid `move`
chun `tx` a bhogadh isteach sa dúnadh ionas go mbeidh `tx` ag an snáithe sceite. Caithfidh an snáithe sceite
an tarchuradóir a bheith aige chun teachtaireachtaí a sheoladh tríd an
chainéal. Tá modh `send` ag an tarchuradóir a ghlacann an luach is mian linn a
sheoladh. Tugann an modh `send` cineál `Result<T, E>` ar ais, mar sin má tá an glacadóir
scaoilte cheana féin agus mura bhfuil áit ar bith ann chun luach a sheoladh, cuirfidh an oibríocht seolta
earráid ar ais. Sa sampla seo, táimid ag glaoch ar `unwrap` chun scaoll a chur i gcás
earráide. Ach in fheidhmchlár fíor, láimhseálfaimis é i gceart: fill ar
Chaibidil 9 chun athbhreithniú a dhéanamh ar straitéisí maidir le láimhseáil earráide i gceart.

I Liostáil 16-8, gheobhaimid an luach ón nglacadóir sa phríomhshnáithe. Tá sé seo
cosúil leis an lacha rubair a aisghabháil ón uisce ag deireadh na habhann nó
teachtaireacht comhrá a fháil.

<Listing number="16-8" file-name="src/main.rs" caption="Receiving the value “hi” in the main thread and printing it">

```rust
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-08/src/main.rs}}
```

</Listing>

Tá dhá mhodh úsáideacha ag an nglacadóir: `recv` agus `try_recv`. Táimid ag baint úsáide as `recv`,
giorrúchán do _receive_, a chuirfidh bac ar fhorghníomhú an phríomhshnáithe agus a fhanfaidh
go dtí go seolfar luach síos an cainéal. Nuair a sheolfar luach, cuirfidh `recv`
ar ais é i `Result<T, E>`. Nuair a dhúnann an tarchuradóir, cuirfidh `recv`
earráid ar ais chun comhartha nach mbeidh aon luachanna eile ag teacht.

Ní chuireann an modh `try_recv` bac, ach ina ionad sin cuirfidh sé `Result<T, E>` ar ais
láithreach: luach `Ok` ina bhfuil teachtaireacht má tá ceann ar fáil agus luach `Err`
mura bhfuil aon teachtaireachtaí ann an uair seo. Tá úsáid `try_recv` úsáideach
má tá obair eile le déanamh ag an snáithe seo agus muid ag fanacht le teachtaireachtaí: d'fhéadfaimis
lúb a scríobh
a ghlaonn ar `try_recv` ó am go ham, a láimhseálann teachtaireacht má tá ceann ar fáil,
agus a dhéanann obair eile ar feadh tamaill bhig go dtí go ndéantar seiceáil
arís.

D'úsáideamar `recv` sa sampla seo ar mhaithe le simplíocht; níl aon obair eile againn don phríomhshnáithe le déanamh seachas fanacht le teachtaireachtaí, mar sin is cuí an príomhshnáithe a bhlocáil.

Nuair a ritheann muid an cód i Liosta 16-8, feicfimid an luach priontáilte ón bpríomhshnáithe:

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the threads running differently rather than
changes in the compiler -->

```text
Got: hi
```

Foirfe!

### Cainéil agus Aistriú Úinéireachta

Tá ról ríthábhachtach ag na rialacha úinéireachta i seoladh teachtaireachtaí mar go gcabhraíonn siad leat
cód sábháilte, comhuaineach a scríobh. Is é an buntáiste a bhaineann le smaoineamh ar úinéireacht ar fud do chláir Rust ná earráidí a chosc i gcláreagrú comhuaineach. Déanaimis
turgnamh chun a thaispeáint conas a oibríonn bealaí agus úinéireacht le chéile chun
fadhbanna a chosc: déanfaimid iarracht luach `val` a úsáid sa snáithe sceite _tar éis_ dúinn
é a sheoladh síos an cainéal. Bain triail as an gcód i Liostáil 16-9 a thiomsú chun a fheiceáil cén fáth
nach gceadaítear an cód seo:

<Listing number="16-9" file-name="src/main.rs" caption="Attempting to use `val` after we’ve sent it down the channel">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-09/src/main.rs}}
```

</Listing>

Anseo, déanaimid iarracht `val` a phriontáil tar éis dúinn é a sheoladh síos an cainéal trí `tx.send`.
Bheadh ​​sé ina dhroch-smaoineamh é seo a cheadú: nuair a bheidh an luach seolta chuig snáithe eile, d'fhéadfadh an snáithe sin é a mhodhnú nó a ligean ar lár sula ndéanaimid iarracht an luach a úsáid
arís. D'fhéadfadh sé go mbeadh earráidí nó
torthaí gan choinne mar thoradh ar mhodhnuithe an snáithe eile mar gheall ar shonraí neamhréireach nó neamhbheith ann. Mar sin féin, tugann Rust
earráid dúinn má dhéanaimid iarracht an cód i Liostáil 16-9 a thiomsú:

```console
{{#include ../../listings/ch16-fearless-concurrency/listing-16-09/output.txt}}
```

Tá earráid ama tiomsaithe mar thoradh ar ár mbotún comhthráthachta. Glacann an fheidhm `send` úinéireacht ar a paraiméadar, agus nuair a bhogtar an luach, glacann an glacadóir úinéireacht air. Cuireann sé seo cosc ​​orainn an luach a úsáid arís de thaisme tar éis é a sheoladh; seiceálann an córas úinéireachta go bhfuil gach rud ceart go leor.

### Illuachanna a Sheoladh agus an Glacadóir a Fheiceáil ag Fanacht

Tiomsaíodh agus rith an cód i Liostáil 16-8, ach níor léirigh sé go soiléir dúinn go raibh dhá shnáithe ar leith ag caint lena chéile thar an gcainéal. I Liostáil 16-10 rinneamar roinnt modhnuithe a chruthóidh go bhfuil an cód i Liostáil 16-8 ag rith ag an am céanna: seolfaidh an snáithe sceite teachtaireachtaí iolracha anois agus sosfaidh sé ar feadh soicind idir gach teachtaireacht.

<Listing number="16-10" file-name="src/main.rs" caption="Sending multiple messages and pausing between each">

```rust,noplayground
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-10/src/main.rs}}
```

</Listing>

An uair seo, tá veicteoir teaghrán ag an snáithe sceite ar mhaith linn a sheoladh chuig an bpríomhshnáithe. Déanaimid athrá orthu, ag seoladh gach ceann ina aonar, agus sos a chur idir gach ceann trí ghlaoch ar an bhfeidhm `thread::sleep` le luach `Duration` de
1 soicind.

Sa phríomhshnáithe, nílimid ag glaoch ar an bhfeidhm `recv` go sainráite a thuilleadh:
ina áit sin, táimid ag déileáil le `rx` mar athrá. Maidir le gach luach a fhaightear, táimid á
phriontáil. Nuair a dhúnfar an cainéal, críochnóidh an athrá.

Nuair a bhíonn an cód i Liosta 16-10 á rith, ba cheart duit an t-aschur seo a leanas a fheiceáil
le sos 1 soicind idir gach líne:

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the threads running differently rather than
changes in the compiler -->

```text
Got: hi
Got: from
Got: the
Got: thread
```

Ós rud é nach bhfuil aon chód againn a chuireann sos nó moill ar an lúb `for` sa
phríomhshnáithe, is féidir linn a rá go bhfuil an príomhshnáithe ag fanacht le luachanna a fháil ón
snáithe a cruthaíodh.

### Il-Tháirgeoirí a Chruthú tríd an Tarchuradóir a Chlónáil

Níos luaithe luaigh muid gur acrainm é `mpsc` do _il-tháirgeoir,
aon tomhaltóir_. Cuirimis `mpsc` in úsáid agus leathnaímis an cód i Liostáil 16-10
chun il-shnáitheanna a chruthú a sheolann luachanna chuig an nglacadóir céanna. Is féidir linn é sin a dhéanamh
trí an tarchuradóir a chlónáil, mar a thaispeántar i Liostáil 16-11:

<Listing number="16-11" file-name="src/main.rs" caption="Sending multiple messages from multiple producers">

```rust,noplayground
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-11/src/main.rs:here}}
```

</Listing>


An uair seo, sula gcruthaímid an chéad snáithe sceite, glaoimid ar `clone` ar an
tarchuradóir. Tabharfaidh sé seo tarchuradóir nua dúinn is féidir linn a chur ar aghaidh chuig an gcéad
snáithe sceite. Cuirimid an tarchuradóir bunaidh ar aghaidh chuig an dara snáithe sceite.
Tugann sé seo dhá shnáithe dúinn, agus gach ceann acu ag seoladh teachtaireachtaí difriúla chuig an nglacadóir amháin.

Nuair a ritheann tú an cód, ba chóir go mbeadh cuma mar seo ar d’aschur:

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the threads running differently rather than
changes in the compiler -->

```text
Got: hi
Got: more
Got: from
Got: messages
Got: for
Got: the
Got: thread
Got: you
```

B’fhéidir go bhfeicfeá na luachanna in ord difriúil, ag brath ar do chóras. Seo é
an rud a fhágann go bhfuil comhthráthacht suimiúil agus deacair araon. Má dhéanann tú turgnamh le
`thread::sleep`, ag tabhairt luachanna éagsúla dó sna snáitheanna éagsúla, beidh gach rith
níos neamhchinntitheach agus cruthófar aschur difriúil gach uair.

Anois agus muid tar éis breathnú ar an gcaoi a n-oibríonn bealaí, féachaimis ar mhodh difriúil
comthráthachta.