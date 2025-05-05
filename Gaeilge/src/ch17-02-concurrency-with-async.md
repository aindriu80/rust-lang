## Comhthráthacht a Chur i bhFeidhm le hAs-Shioncrónach

<!-- Seancheannteidil. Ná bain iad nó d'fhéadfadh naisc briseadh. -->

<a id="concurrency-with-async"></a>

Sa chuid seo, cuirfimid as-shioncrónach i bhfeidhm ar chuid de na dúshláin chomhthráthachta céanna
a ndearnamar aghaidh orthu le snáitheanna i gcaibidil 16. Ós rud é gur labhair muid cheana féin faoi go leor de na
príomhsmaointe ansin, díreoimid sa chuid seo ar an difríocht idir
snáitheanna agus todhchaí.

I go leor cásanna, tá na APIanna le haghaidh oibriú le comhthráthacht ag baint úsáide as as-shioncrónach an-
chosúil leo siúd le haghaidh snáitheanna a úsáid. I gcásanna eile, bíonn siad sách
difriúil. Fiú nuair a bhíonn cuma_chosúil_ ar na APIanna idir snáitheanna agus as-shioncrónach, is minic a bhíonn iompar difriúil acu - agus bíonn tréithe feidhmíochta éagsúla acu beagnach i gcónaí.

<!-- Seancheannteidil. Ná bain iad nó d'fhéadfadh naisc briseadh. -->

<a id="counting"></a>

### Tasc Nua a Chruthú le `spawn_task`

Ba é an chéad oibríocht a ndearnamar i ngleic léi i [Snáithe Nua a Chruthú le
Spawn][thread-spawn]<!-- ignore --> ná comhaireamh suas ar dhá shnáithe ar leith.
Déanaimis an rud céanna ag baint úsáide as async. Soláthraíonn an cliath `trpl` feidhm `spawn_task`
atá an-chosúil leis an API `thread::spawn`, agus feidhm `sleep`
atá ina leagan async den API `thread::sleep`. Is féidir linn iad seo a úsáid le chéile
chun an sampla comhairimh a chur i bhfeidhm, mar a thaispeántar i Liostáil 17-6.

<Listing number="17-6" caption="Creating a new task to print one thing while the main task prints something else" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-06/src/main.rs:all}}
```

</Listing>

Mar phointe tosaigh, shocraíomar ár bhfeidhm `main` le `trpl::run` ionas gur féidir lenár bhfeidhm barrleibhéil a bheith neamhshioncrónach.

> Nóta: Ón bpointe seo ar aghaidh sa chaibidil, beidh an cód fillte céanna seo san áireamh i ngach sampla le `trpl::run` i `main`, mar sin is minic a scipeálfaimid é
> díreach mar a dhéanaimid le `main`. Ná déan dearmad é a chur san áireamh i do chód!

Ansin scríobhaimid dhá lúb laistigh den bhloc sin, agus glao `trpl::sleep` i ngach ceann acu,
a fhanann leathshoicind (500 milleasoicind) sula seoltar an chéad
teachtaireacht eile. Cuirimid lúb amháin i gcorp `trpl::spawn_task` agus an ceann eile i
lúb `for` barrleibhéil. Cuirimid `await` leis freisin tar éis na nglaonna `sleep`.

Iompraíonn an cód seo ar bhealach cosúil leis an gcur i bhfeidhm bunaithe ar shnáitheanna—lena n-áirítear an
fíric go bhféadfadh tú na teachtaireachtaí a fheiceáil in ord difriúil i do
chríochfort féin nuair a ritheann tú é:

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the threads running differently rather than
changes in the compiler -->

```text
hi number 1 from the second task!
hi number 1 from the first task!
hi number 2 from the first task!
hi number 2 from the second task!
hi number 3 from the first task!
hi number 3 from the second task!
hi number 4 from the first task!
hi number 4 from the second task!
hi number 5 from the first task!
```

Stopann an leagan seo a luaithe a chríochnaíonn an lúb `for` i gcorp an phríomhbhloic async, toisc go ndúnfar an tasc a ghintear le `spawn_task` nuair a chríochnaíonn an fheidhm `main`. Más mian leat go rithfidh sé an bealach ar fad go dtí go mbeidh an tasc críochnaithe, beidh ort láimhseáil join a úsáid chun fanacht go gcríochnófar an chéad tasc. Le
snáitheanna, d'úsáideamar an modh `join` chun "bac" a chur air go dtí go mbeadh an snáithe críochnaithe ag rith.
I Liosta 17-7, is féidir linn `await` a úsáid chun an rud céanna a dhéanamh, toisc gur todhchaí é an láimhseáil tasc féin. Is `Result` a chineál `Output`, mar sin díphacáilimid é freisin
tar éis fanacht leis.


<Listing number="17-7" caption="Using `await` with a join handle to run a task to completion" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-07/src/main.rs:handle}}
```

</Listing>

Ritheann an leagan nuashonraithe seo go dtí go gcríochnaíonn _an dá_ lúb.

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the threads running differently rather than
changes in the compiler -->

```text
hi number 1 from the second task!
hi number 1 from the first task!
hi number 2 from the first task!
hi number 2 from the second task!
hi number 3 from the first task!
hi number 3 from the second task!
hi number 4 from the first task!
hi number 4 from the second task!
hi number 5 from the first task!
hi number 6 from the first task!
hi number 7 from the first task!
hi number 8 from the first task!
hi number 9 from the first task!
```

Go dtí seo, is cosúil go dtugann async agus snáitheanna na torthaí bunúsacha céanna dúinn, ach le comhréir dhifriúil: ag baint úsáide as `await` in ionad glaoch ar `join` ar an láimhseáil join, agus ag fanacht leis na glaonna `sleep`.

Is é an difríocht is mó ná nach raibh orainn snáithe córais oibriúcháin eile a chruthú chun seo a dhéanamh. Déanta na fírinne, ní gá dúinn fiú tasc a chruthú anseo. Toisc go
mbíonn bloic async ag tiomsú chuig todhchaí gan ainm, is féidir linn gach lúb a chur i mbloc async agus an t-am rith a chur orthu araon go dtí go mbeidh siad críochnaithe ag baint úsáide as an bhfeidhm `trpl::join`.

Sa chuid [Ag fanacht le gach snáithe a chríochnú ag baint úsáide as Láimhseálacha `join`][join-handles]<!-- ignore -->, thaispeánamar conas an modh `join` a úsáid ar an gcineál `JoinHandle` a fhilleann nuair a ghlaonn tú ar `std::thread::spawn`. Tá an fheidhm `trpl::join` cosúil, ach le haghaidh todhchaí. Nuair a thugann tú dhá thodhchaí dó,
táirgeann sé todhchaí nua aonair a bhfuil a aschur ina tuple ina bhfuil aschur
gach todhchaí a chuir tú isteach a luaithe a bheidh siad _an dá_ gcríochnaithe. Dá bhrí sin, i Liosta 17-8,
úsáidimid `trpl::join` chun fanacht go mbeidh `fut1` agus `fut2` críochnaithe. _Ní_ fhanfaimid
le `fut1` agus `fut2` ach ina ionad sin leis an todhchaí nua a tháirgeann `trpl::join`. Déanaimid neamhaird den
aschur, mar níl ann ach tuple ina bhfuil dhá luach aonaid.

<Listing number="17-8" caption="Using `trpl::join` to await two anonymous futures" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-08/src/main.rs:join}}
```

</Listing>

Nuair a ritheann muid é seo, feicimid an dá thodhchaí ag rith go dtí an críoch:

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the threads running differently rather than
changes in the compiler -->

```text
hi number 1 from the first task!
hi number 1 from the second task!
hi number 2 from the first task!
hi number 2 from the second task!
hi number 3 from the first task!
hi number 3 from the second task!
hi number 4 from the first task!
hi number 4 from the second task!
hi number 5 from the first task!
hi number 6 from the first task!
hi number 7 from the first task!
hi number 8 from the first task!
hi number 9 from the first task!
```

Anois, feicfidh tú an t-ord céanna gach uair, rud atá an-difriúil ón méid a chonaiceamar le snáitheanna. Tá sé sin amhlaidh toisc go bhfuil an fheidhm `trpl::join` _fair_,
rud a chiallaíonn go seiceálann sí gach todhchaí chomh minic céanna, ag malartú eatarthu, agus nach ligeann sí do cheann amháin dul chun tosaigh riamh má tá an ceann eile réidh. Le snáitheanna, cinneann an córas oibriúcháin cén snáithe atá le seiceáil agus cé chomh fada is ceart dó rith. Le async Rust, cinneann an
am rith cén tasc atá le seiceáil. (Go praiticiúil, bíonn na sonraí casta
toisc go bhféadfadh am rith async snáitheanna córais oibriúcháin a úsáid faoin gcochall mar
chuid den chaoi a mbainistíonn sé comhthráthacht, mar sin is féidir go mbeadh níos mó oibre ann cothroime a ráthú
do am rith - ach is féidir fós!) Ní gá d'amanna rith cothroime a ráthú
d'aon oibríocht ar leith, agus is minic a thairgeann siad APIanna éagsúla chun ligean duit
a roghnú cibé acu is mian leat cothroime nó nach ea.

Bain triail as cuid de na hathruithe seo ar fanacht leis na todhchaí agus féach cad a dhéanann siad:

- Bain an bloc async as timpeall ar cheachtar lúb nó an dá cheann. - Fan le gach bloc neamhshioncrónach díreach tar éis é a shainiú.
- Fill an chéad lúb amháin i mbloc neamhshioncrónach, agus fan leis an todhchaí a eascraíonn as tar éis chorp an dara lúb.

Mar dhúshlán breise, féach an féidir leat a dhéanamh amach cad a bheidh an t-aschur i
ngach cás _sula_ ritheann tú an cód!

### Ag Comhaireamh Suas ar Dhá Thasc ag Úsáid Aistriú Teachtaireachtaí

Beidh roinnt sonraí idir todhchaíochtaí eolach freisin: úsáidfimid teachtaireachtaí aistriú
arís, ach an uair seo le leaganacha neamhshioncrónacha de na cineálacha agus na feidhmeanna. Glacfaimid
cosán beagán difriúil ná mar a rinneamar i [Ag Úsáid Aistriú Teachtaireachtaí chun Sonraí a Aistriú
Idir Snáitheanna][message-passing-threads]<!-- neamhaird --> chun cuid de na
príomhdhifríochtaí idir comhthráthacht bunaithe ar shnáitheanna agus todhchaíochtaí bunaithe a léiriú. I
Liostú 17-9, tosóimid le bloc neamhshioncrónach amháin—_gan_ tasc ar leithligh a chruthú mar a chruthaíomar snáithe ar leithligh.

<Listing number="17-9" caption="Creating an async channel and assigning the two halves to `tx` and `rx`" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-09/src/main.rs:channel}}
```

</Listing>

Anseo, úsáidimid `trpl::channel`, leagan neamhshioncrónach den API il-tháirgeora, aon-tomhaltóra a d'úsáideamar le snáitheanna siar i gCaibidil 16. Níl ach beagán difríochta idir an leagan neamhshioncrónach den API agus an leagan snáithe-bhunaithe: úsáideann sé `rx` glacadóir inathraithe seachas glacadóir dochloíte, agus cruthaíonn a mhodh `recv` todhchaí a gcaithfimid fanacht leis seachas an luach a tháirgeadh go díreach. Anois
is féidir linn teachtaireachtaí a sheoladh ón seoltóir chuig an nglacadóir. Tabhair faoi deara nach gá dúinn
snáithe ar leithligh nó fiú tasc a chruthú; níl le déanamh againn ach fanacht leis an nglao `rx.recv`.

Blocálann an modh sioncrónach `Receiver::recv` i `std::mpsc::channel` go dtí
go bhfaigheann sé teachtaireacht. Ní dhéanann an modh `trpl::Receiver::recv`, toisc go bhfuil sé neamhshioncrónach. In ionad blocáil, tugann sé an rialú ar ais don am rith go dtí go
bhfaightear teachtaireacht nó go ndúnann taobh seolta an chainéil. I gcodarsnacht leis sin, ní fhanfaimid leis an nglao `send`, mar ní chuireann sé bac air. Ní gá dó, mar níl teorainn leis an gcainéal a bhfuilimid á sheoladh isteach ann.

> Nóta: Ós rud é go ritheann an cód async seo go léir i mbloc async i nglao `trpl::run`
>, is féidir le gach rud laistigh de bhlocáil a sheachaint. Mar sin féin, cuirfidh an cód _lasmuigh_ de
> bac ar an bhfeidhm `run` atá ag filleadh. Sin pointe iomlán na feidhme
> `trpl::run`: ligeann sé duit _a roghnú_ cá háit le blocáil ar shraith áirithe de chód async,
> agus dá bhrí sin cá háit le haistriú idir cód sioncrónaithe agus async. I bhformhór na rith-amanna async,
> tugtar `block_on` ar `run` ar an gcúis seo go díreach.

Tabhair faoi deara dhá rud faoin sampla seo. Ar dtús, tiocfaidh an teachtaireacht láithreach.

Ar an dara dul síos, cé go n-úsáidimid todhchaí anseo, níl aon chomhthráthacht ann fós. Tarlaíonn gach rud
sa liostú in ord, díreach mar a dhéanfadh sé mura mbeadh aon todhchaí
i gceist.

Déanaimis aghaidh ar an gcéad chuid trí shraith teachtaireachtaí a sheoladh agus codladh eatarthu, mar a thaispeántar i Liostáil 17-10.

<!-- We cannot test this one because it never stops! -->

<Listing number="17-10" caption="Sending and receiving multiple messages over the async channel and sleeping with an `await` between each message" file-name="src/main.rs">

```rust,ignore
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-10/src/main.rs:many-messages}}
```

</Listing>

Chomh maith leis na teachtaireachtaí a sheoladh, ní mór dúinn iad a fháil. Sa chás seo,
toisc go bhfuil a fhios againn cé mhéad teachtaireacht atá ag teacht isteach, d'fhéadfaimis é sin a dhéanamh de láimh trí
ghlaoch ar `rx.recv().await` ceithre huaire. Sa saol réadúil, áfach, de ghnáth beidh muid ag fanacht ar líon _anaithnid_ teachtaireachtaí, mar sin ní mór dúinn fanacht
go dtí go gcinnfimid nach bhfuil a thuilleadh teachtaireachtaí ann.

I Liosta 16-10, d'úsáideamar lúb `for` chun na míreanna go léir a fuarthas ó
chainéal sioncrónach a phróiseáil. Níl bealach ag Rust fós chun lúb `for` a scríobh thar shraith
_asinchrónach_ míreanna, áfach, mar sin ní mór dúinn lúb nach bhfacamar roimhe seo a úsáid: an lúb coinníollach `while let`. Seo an leagan lúb den
thógáil `if let` a chonaiceamar siar sa chuid [Sreabhadh Rialaithe Gonta le `if
let` agus `let else`][if-let]<!-- neamhaird a dhéanamh -->. Leanfaidh an lúb ag feidhmiú chomh fada agus a leanann an patrún a shonraítear de bheith ag teacht leis an luach.

Ginfidh an glao `rx.recv` todhchaí, agus fanfaimid air. Cuirfidh an t-am rith sos ar an todhchaí go dtí go mbeidh sé réidh. Nuair a thiocfaidh teachtaireacht, réiteoidh an todhchaí go
`Some(message)` an oiread uaireanta agus a thagann teachtaireacht. Nuair a dhúnann an cainéal,
beag beann ar cibé an bhfuil _aon_ teachtaireachtaí tagtha, réiteoidh an todhchaí go `None` ina ionad sin chun a léiriú nach bhfuil aon luachanna eile ann agus dá bhrí sin ba chóir dúinn
stop a chur leis an vótaíocht—is é sin, stop a chur leis an bhfanacht.

Tarraingíonn an lúb `while let` seo go léir le chéile. Más é `Some(message)` toradh an ghlao ar
`rx.recv().await`, faighimid rochtain ar an teachtaireacht agus is féidir linn
í a úsáid i gcorp an lúibe, díreach mar a d'fhéadfaimis le `if let`. Más é
`None` an toradh, críochnaíonn an lúb. Gach uair a chríochnaíonn an lúb, buaileann sé an pointe fanachta
arís, mar sin cuireann an t-am rith sos air arís go dtí go dtagann teachtaireacht eile.

Seolann agus faigheann an cód na teachtaireachtaí go léir go rathúil anois. Ar an drochuair,
tá cúpla fadhb ann fós. Ar an gcéad dul síos, ní thagann na teachtaireachtaí
ag eatraimh leathshoicind. Tagann siad go léir ag an am céanna, 2 (2,000 milleasoicind) tar éis
dúinn an clár a thosú. Ar an dara dul síos, ní scoireann an clár seo riamh! Ina áit sin,
fanann sé go deo le haghaidh teachtaireachtaí nua. Beidh ort é a dhúnadh síos ag baint úsáide as <span
class="keystroke">ctrl-c</span>.

Tosaímis trí scrúdú a dhéanamh ar an gcúis a dtagann na teachtaireachtaí isteach go léir ag an am céanna tar éis an
mhoill iomláin, seachas teacht isteach le moilleanna idir gach ceann. Laistigh de bhloc neamhshioncrónach ar leith,
is é an t-ord ina bhfeictear eochairfhocail `await` sa chód an t-ord ina ndéantar iad a fhorghníomhú nuair a ritheann an clár.

Níl ach bloc neamhshioncrónach amháin i Liosta 17-10, mar sin ritheann gach rud ann
go líneach. Níl aon chomhthráthacht ann fós. Tarlaíonn na glaonna `tx.send` go léir,
idircheangailte leis na glaonna `trpl::sleep` go léir agus a gcuid pointí await
gaolmhara. Ansin amháin a théann an lúb `while let` trí aon cheann de na pointí `await`
ar na glaonna `recv`.

Chun an t-iompar atá uainn a fháil, áit a dtarlaíonn an mhoill codlata idir gach teachtaireacht,
ní mór dúinn na hoibríochtaí `tx` agus `rx` a chur ina mbloic neamhshioncrónacha féin, mar a thaispeántar
i Liosta 17-11. Ansin is féidir leis an rith-am gach ceann acu a fhorghníomhú ar leithligh ag baint úsáide as
`trpl::join`, díreach mar atá sa sampla comhairimh. Arís eile, fanfaimid ar thoradh
glaoch ar `trpl::join`, ní ar na todhchaí aonair. Dá bhfanfaimis ar na
todhchaí aonair in ord, chríochnóimis ar ais i sreabhadh seicheamhach - díreach an rud atáimid ag iarraidh _gan_ a dhéanamh.

<!-- We cannot test this one because it never stops! -->

<Listing number="17-11" caption="Separating `send` and `recv` into their own `async` blocks and awaiting the futures for those blocks" file-name="src/main.rs">

```rust,ignore
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-11/src/main.rs:futures}}
```

</Listing>

Leis an gcód nuashonraithe i Liosta 17-11, priontáiltear na teachtaireachtaí ag eatraimh 500 milleasoicind, seachas iad go léir ar luas lasrach tar éis 2 shoicind.

Ní scoireann an clár riamh, áfach, mar gheall ar an gcaoi a n-idirghníomhaíonn lúb `while let` le `trpl::join`:

- Ní chríochnaíonn an todhchaí a fhilleann ó `trpl::join` ach amháin nuair a bhíonn _both_ futures a tugadh dó críochnaithe.

- Críochnaíonn an todhchaí `tx` nuair a chríochnaíonn sé ina chodladh tar éis an teachtaireacht dheireanach a sheoladh i `vals`.

- Ní chríochnóidh an todhchaí `rx` go dtí go gcríochnóidh lúb `while let`.

- Ní chríochnóidh lúb `while let` go dtí go dtáirgtear `None` ag fanacht le `rx.recv`.

- Ní fhilleann fanacht le `rx.recv` `None` ach amháin nuair a bheidh ceann eile an chainéil dúnta.

- Ní dhúnfaidh an cainéal ach amháin má ghlaonn muid `rx.close` nó nuair a scaoiltear taobh an tseoltóra,
`tx`.
- Ní ghlaonn muid ar `rx.close` áit ar bith, agus ní scaoilfear `tx` go dtí go mbeidh an bloc neamhshioncrónach is forimeallaí a chuirtear ar aghaidh chuig `trpl::run` críochnaithe.
- Ní féidir leis an mbloc críochnú mar go bhfuil sé blocáilte nuair a bheidh `trpl::join` críochnaithe, rud a thugann ar ais go barr an liosta seo sinn.

D’fhéadfaimis `rx` a dhúnadh de láimh trí ghlaoch ar `rx.close` áit éigin, ach níl mórán ciall leis sin. Dá stopfaí tar éis líon treallach teachtaireachtaí a láimhseáil,
dhéanfadh sé sin an clár a dhúnadh síos, ach d’fhéadfaimis teachtaireachtaí a chailleadh. Teastaíonn bealach eile uainn
chun a chinntiú go scaoilfear `tx` _roimh_ dheireadh na feidhme.

Faoi láthair, ní fhaigheann an bloc neamhshioncrónach ina seolaimid na teachtaireachtaí ach `tx` ar iasacht mar
nach bhfuil úinéireacht ag teastáil chun teachtaireacht a sheoladh, ach dá bhféadfaimis `tx` a bhogadh isteach sa
bhloc neamhshioncrónach sin, scaoilfí é nuair a bheidh an bloc sin críochnaithe. Sa chuid Caibidil 13
[Tagairtí a Ghabháil nó Úinéireacht a Bhogadh][capture-or-move]<!-- neamhaird a dhéanamh -->, d'fhoghlaim tú
conas an eochairfhocal `move` a úsáid le dúnadh, agus, mar a pléadh sa
chuid Caibidil 16 [Dúnadh `move` a Úsáid le Snáitheanna][move-threads]<!-- neamhaird a dhéanamh
-->, is minic a bhíonn orainn sonraí a bhogadh isteach i ndúnadh agus muid ag obair le snáitheanna.

Baineann an dinimic bhunúsach chéanna le bloic async, mar sin oibríonn an eochairfhocal `move` le
bloic async díreach mar a dhéanann sé le dúnadh.

I Liosta 17-12, athraímid an bloc a úsáidtear chun teachtaireachtaí a sheoladh ó `async` go
`async move`. Nuair a ritheann muid an _leagan_ seo den chód, múchtar é go galánta
tar éis an teachtaireacht dheireanach a sheoladh agus a fháil.

<Listing number="17-12" caption="A  revision of the code from Listing 17-11 that correctly shuts down when complete" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-12/src/main.rs:with-move}}
```

</Listing>

Is cainéal il-tháirgeoirí é an cainéal neamhshioncrónach seo freisin, mar sin is féidir linn glaoch ar `clone` ar `tx` más mian linn teachtaireachtaí a sheoladh ó thodhchaí iolracha, mar a thaispeántar i Liostáil 17-13.

<Listing number="17-13" caption="Using multiple producers with async blocks" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-13/src/main.rs:here}}
```

</Listing>

Ar dtús, clónálaimid `tx`, ag cruthú `tx1` lasmuigh den chéad bhloc asyncrónach. Bogaimid `tx1` isteach sa bhloc sin díreach mar a rinneamar roimhe seo le `tx`. Ansin, níos déanaí, bogaimid an `tx` bunaidh isteach i mbloc asyncrónach _new_, áit a seolaimid níos mó teachtaireachtaí ar
mhoill beagán níos moille. Tarlaíonn sé go gcuirimid an bloc asyncrónach nua seo i ndiaidh an bhloic asyncrónaigh
chun teachtaireachtaí a fháil, ach d'fhéadfadh sé dul roimhe chomh maith céanna. Is é an eochair
an t-ord ina bhfuiltear ag fanacht leis na todhchaí, ní an áit ina gcruthaítear iad.

Ní mór don dá bhloc asyncrónach chun teachtaireachtaí a sheoladh a bheith ina mblocanna `bogadh async` ionas
go gcaillfear `tx` agus `tx1` araon nuair a chríochnaíonn na bloic sin. Seachas sin, críochnóimid ar ais san lúb gan teorainn céanna inar thosaíomar. Ar deireadh, athraímid ó `trpl::join` go `trpl::join3` chun an todhchaí bhreise a láimhseáil.

Anois feicimid na teachtaireachtaí go léir ó na todhchaí seolta araon, agus toisc go n-úsáideann na todhchaí seolta moilleanna beagán difriúla tar éis seolta, faightear na teachtaireachtaí ag na eatraimh éagsúla sin freisin.

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the threads running differently rather than
changes in the compiler -->

```text
received 'hi'
received 'more'
received 'from'
received 'the'
received 'messages'
received 'future'
received 'for'
received 'you'
```

Is tús maith é seo, ach níl ann ach dornán todhchaí: dhá cheann le `join`, nó trí cinn le `join3`. Feicfimid conas a d'fhéadfaimis oibriú le níos mó todhchaí.

[thread-spawn]: ch16-01-threads.html#creating-a-new-thread-with-spawn
[join-handles]: ch16-01-threads.html#waiting-for-all-threads-to-finish-using-join-handles
[message-passing-threads]: ch16-02-message-passing.html
[if-let]: ch06-03-if-let.html
[capture-or-move]: ch13-01-closures.html#capturing-references-or-moving-ownership
[move-threads]: ch16-01-threads.html#using-move-closures-with-threads
