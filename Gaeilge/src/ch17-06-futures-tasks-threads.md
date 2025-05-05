## Ag Cur Gach Rud le Chéile: Todhchaí, Tascanna, agus Snáitheanna

Mar a chonaiceamar i [Caibidil 16][ch16]<!-- neamhaird -->, cuireann snáitheanna cur chuige amháin ar fáil maidir le
comhthráthacht. Chonaiceamar cur chuige eile sa chaibidil seo: úsáid a bhaint as neamhshioncrónach le
todhchaí agus sruthanna. Más mian leat a fháil amach cathain is ceart modh a roghnú thar an gceann eile,
is é an freagra: braitheann sé! Agus i go leor cásanna, ní snáitheanna _nó_ neamhshioncrónach an rogha ach snáitheanna _agus_ neamhshioncrónach.

Tá samhlacha comhthráthachta bunaithe ar shnáitheanna á soláthar ag go leor córas oibriúcháin le
blianta fada anois, agus tacaíonn go leor teangacha ríomhchlárúcháin leo dá bharr. Mar sin féin,
níl na samhlacha seo gan a gcomhbhabhtálacha. Ar go leor córas oibriúcháin,
úsáideann siad go leor cuimhne do gach snáithe, agus tagann roinnt forchostais leo le haghaidh
tosú agus múchadh. Ní rogha iad snáitheanna ach amháin nuair a thacaíonn do
chóras oibriúcháin agus do chrua-earraí leo. Murab ionann agus ríomhairí deisce agus soghluaiste príomhshrutha, níl aon chóras oibriúcháin ag roinnt córas leabaithe ar chor ar bith, mar sin níl aon snáitheanna acu ach an oiread.

Soláthraíonn an tsamhail asyncrónach sraith chomhbhabhtálacha dhifriúil - agus comhlántach sa deireadh. Sa tsamhail asyncrónach, ní theastaíonn a snáitheanna féin ó oibríochtaí comhthráthacha. Ina áit sin, is féidir leo rith ar thascanna, mar a d'úsáideamar `trpl::spawn_task` chun
obair a thosú ó fheidhm shioncrónach sa chuid sruthanna. Tá tasc
cosúil le snáithe, ach in ionad é a bhainistiú ag an gcóras oibriúcháin, déantar é a
bhainistiú ag cód leibhéal na leabharlainne: an t-am rith.

Sa chuid roimhe seo, chonaiceamar gur féidir linn sruth a thógáil trí chainéal asyncrónach
a úsáid agus tasc asyncrónach a sceitheadh ​​​​a d'fhéadfaimis glaoch air ó chód sioncrónach. Is féidir linn
an rud céanna a dhéanamh le snáithe. I Liostáil 17-40, d'úsáideamar
`trpl::spawn_task` agus `trpl::sleep`. I Liosta 17-41, cuirimid na hAPIanna `thread::spawn` agus `thread::sleep` ón leabharlann chaighdeánach san fheidhm `get_intervals` ina n-áit.

<Listing number="17-41" caption="Using the `std::thread` APIs instead of the async `trpl` APIs for the `get_intervals` function" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-41/src/main.rs:threads}}
```

</Listing>

Má ritheann tú an cód seo, tá an t-aschur mar an gcéanna le haschur Liosta 17-40. Agus
tabhair faoi deara cé chomh beag is atá na hathruithe anseo ó pheirspictíocht an chóid ghlaoigh. Ina theannta sin, cé gur ghin ceann dár bhfeidhmeanna tasc neamhshioncrónach ar an am rith agus
gur ghin an ceann eile snáithe OS, níor chuir na difríochtaí isteach ar na sruthanna a lean as.

In ainneoin a gcosúlachtaí, iompraíonn an dá chur chuige seo go han-difriúil,
cé go mb’fhéidir go mbeadh sé deacair orainn é a thomhas sa sampla an-simplí seo. D’fhéadfaimis
na milliúin tascanna neamhshioncrónacha a ghiniúint ar aon ríomhaire pearsanta nua-aimseartha. Dá ndéanfaimis iarracht
é sin a dhéanamh le snáitheanna, rithfeadh an chuimhne asainn go litriúil!

Mar sin féin, tá cúis ann go bhfuil na APIanna seo chomh cosúil sin. Feidhmíonn snáitheanna mar theorainn
do shraitheanna d’oibríochtaí sioncrónacha; is féidir comhthráthacht a bheith ann _idir_ snáitheanna.
Feidhmíonn tascanna mar theorainn do shraitheanna d’oibríochtaí _neamhshioncrónacha_; is féidir comhthráthacht a bheith ann
idir_ agus _laistigh_ de thascanna, toisc gur féidir le tasc aistriú idir
todhchaí ina chorp. Ar deireadh, is iad todhchaíochtaí an t-aonad comhthráthachta is mine de chuid Rust, agus féadfaidh gach todhchaí crann de thodhchaí eile a léiriú. Bainistíonn an t-am rithe—go sonrach, a fhorghníomhaitheoir—tascanna, agus bainistíonn tascanna todhchaíochtaí. Sa chomhthéacs sin, tá tascanna cosúil le snáitheanna éadroma, bainistithe ag am rithe le
cumas breise a thagann ó bheith á mbainistiú ag am rithe seachas ag an
gcóras oibriúcháin.

Ní chiallaíonn sé seo go bhfuil tascanna neamhshioncrónacha i gcónaí níos fearr ná snáitheanna (nó a mhalairt). Is samhail ríomhchlárúcháin níos simplí é comhthráthacht le snáitheanna ar bhealaí áirithe
ná comhthráthacht le `async`. Is féidir gur neart nó laige é sin. Tá snáitheanna
rud beag "tine agus dearmad"; níl aon choibhéis dhúchasach acu le todhchaí, mar sin ritheann siad go dtí go mbeidh siad críochnaithe gan cur isteach orthu ach amháin ag an
gcóras oibriúcháin féin. Is é sin le rá, níl aon tacaíocht ionsuite acu do _comthráthacht intratask_ ar an mbealach a dhéanann todhchaíochtaí. Níl aon mheicníochtaí ag snáitheanna i Rust le haghaidh
cealaithe ach an oiread—ábhar nár phléamar go sonrach sa chaibidil seo ach a
tugtar le fios leis an bhfíric gur glanadh a staid i gceart aon uair a chríochnaíomar todhchaí.

Déanann na teorainneacha seo níos deacra snáitheanna a chumadh ná todhchaí freisin. Tá sé i bhfad
níos deacra, mar shampla, snáitheanna a úsáid chun cúntóirí a thógáil ar nós na
modhanna `timeout` agus `throttle` a thógamar níos luaithe sa chaibidil seo. Ciallaíonn an fhíric go bhfuil
struchtúir sonraí níos saibhre i dtodhchaí gur féidir iad a chumadh le chéile níos
nádúrtha, mar a chonaiceamar.

Tugann tascanna, mar sin, _smacht_ breise_ dúinn ar thodhchaí, rud a ligeann dúinn a roghnú
cá háit agus conas iad a ghrúpáil. Agus is cosúil go n-oibríonn snáitheanna agus tascanna go minic
go han-mhaith le chéile, toisc gur féidir tascanna (ar a laghad i roinnt amanna reatha) a bhogadh
idir snáitheanna. Déanta na fírinne, faoin gcochall, tá an t-am reatha atá
á úsáid againn—lena n-áirítear na feidhmeanna `spawn_blocking` agus `spawn_task`—ilshnáitheáilte
de réir réamhshocraithe! Úsáideann go leor rith-amanna cur chuige ar a dtugtar _goid oibre_ chun
tascanna a bhogadh go trédhearcach idir snáitheanna, bunaithe ar an gcaoi a bhfuil na snáitheanna
á n-úsáid faoi láthair, chun feidhmíocht fhoriomlán an chórais a fheabhsú. Éilíonn an
cur chuige sin snáitheanna _agus_ tascanna i ndáiríre, agus dá bhrí sin todhchaí.

Nuair atá tú ag smaoineamh ar an modh le húsáid cathain, smaoinigh ar na rialacha seo:

- Más _an-chomhthreomhar_ an obair, amhail próiseáil a dhéanamh ar ghrúpa sonraí ina bhféadfar gach cuid a phróiseáil ar leithligh, is rogha níos fearr iad snáitheanna.
- Más _an-chomhthráthach_ an obair, amhail láimhseáil teachtaireachtaí ó ghrúpa foinsí éagsúla a d'fhéadfadh teacht isteach ag eatraimh éagsúla nó rátaí éagsúla,
is rogha níos fearr é neamhshioncrónach.

Agus má theastaíonn comhthreomharacht agus comhthráthacht uait, ní gá duit rogha a dhéanamh
idir snáitheanna agus neamhshioncrónach. Is féidir leat iad a úsáid le chéile go saor, ag ligean do gach duine
an ról is fearr a imirt. Mar shampla, taispeánann Liostáil 17-42 sampla sách coitianta
den chineál seo meascáin i gcód Rust an tsaoil réadaigh.

<Listing number="17-42" caption="Sending messages with blocking code in a thread and awaiting the messages in an async block" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-42/src/main.rs:all}}
```

</Listing>

Tosaímid trí chainéal neamhshioncrónach a chruthú, agus ansin sceithimid snáithe a ghlacann úinéireacht ar thaobh an tseoltóra den chainéal. Laistigh den snáithe, seolaimid na huimhreacha 1 go 10, ag codladh ar feadh soicind idir gach ceann. Ar deireadh, rithimid todhchaí a cruthaíodh le bloc neamhshioncrónach a ritheadh ​​chuig `trpl::run` díreach mar atá déanta againn ar fud na caibidle. Sa todhchaí sin, fanfaimid leis na teachtaireachtaí sin, díreach mar atá sna samplaí eile de sheoladh teachtaireachtaí a chonaiceamar.

Chun filleadh ar an gcás a d’oscail muid an chaibidil leis, samhlaigh sraith tascanna ionchódaithe físe a rith ag baint úsáide as snáithe tiomnaithe (toisc go bhfuil ionchódú físe
ceangailte le ríomhaireacht) ach ag cur in iúl don Chomhéadan Úsáideora go ndéantar na hoibríochtaí sin le cainéal neamhshioncrónach. Tá samplaí gan áireamh de na cineálacha teaglaim seo i gcásanna úsáide fíorshaoil.

## Achoimre

Ní hé seo an uair dheireanach a fheicfidh tú comhthráthacht sa leabhar seo. Cuirfidh an tionscadal i
[Caibidil 21][ch21] na coincheapa seo i bhfeidhm i gcás níos réadúla
ná na samplaí níos simplí a phléitear anseo agus déanfaidh sé comparáid níos dírí idir réiteach fadhbanna agus snáitheáil i gcoinne tascanna.

Is cuma cén cur chuige seo a roghnaíonn tú, tugann Rust na huirlisí duit a theastaíonn uait chun cód sábháilte, tapa, comhuaineach a scríobh
—bíodh sé le haghaidh freastalaí gréasáin ard-tréchur nó córas oibriúcháin leabaithe.

Ansin, labhróimid faoi bhealaí idiomatacha chun fadhbanna a shamhaltú agus réitigh a struchtúrú
de réir mar a fhásann do chláir Rust. Ina theannta sin, pléifimid conas a bhaineann idiomacha Rust
leis na cinn a d'fhéadfá a bheith eolach orthu ó chláreagrú dírithe ar réada.

[ch16]: http://localhost:3000/ch16-00-concurrency.html
[combining-futures]: ch17-03-more-futures.html#building-our-own-async-abstractions
[streams]: ch17-04-streams.html#composing-streams
[ch21]: ch21-00-final-project-a-web-server.html