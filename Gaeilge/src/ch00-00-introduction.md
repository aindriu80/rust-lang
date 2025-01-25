# Réamhrá

> Nóta: Is ionann an t-eagrán seo den leabhar agus [An Teanga Ríomhchláraithe
> Rust][nsprust] ar fáil i bhformáid chlóite agus ríomhleabhair ó [No Starch
> Press][nsp].

[nsprust]: https://nostarch.com/rust-programming-language-2nd-edition
[nsp]: https://nostarch.com/

Fáilte go dtí _The Rust Programming Language_, leabhar tosaigh faoi Rust.
Cuidíonn teanga ríomhchláraithe Rust leat bogearraí níos tapúla agus níos iontaofa a scríobh.
Is minic a bhíonn contrárthachtaí ag eirgeanamaíocht ardleibhéil agus rialú ísealleibhéil sa ríomhchlárú
dearadh teanga; Tugann Rust dúshlán don choinbhleacht sin. Trí chothromú cumhachtach
cumas teicniúil agus taithí iontach forbróra, tugann Rust an rogha duit
chun sonraí íseal-leibhéil a rialú (cosúil le húsáid chuimhne) gan aon stró
a bhaineann go traidisiúnta le rialú den sórt sin.

## Cé dó a bhfuil Rust

Tá Rust oiriúnach do go leor daoine ar chúiseanna éagsúla. Breathnaímid ar roinnt de
na grúpaí is tábhachtaí.

### Foirne Forbróirí

Is uirlis tháirgiúil é Rust chun comhoibriú i measc foirne móra de
forbróirí a bhfuil leibhéil éagsúla eolais ar ríomhchlárú córais acu. Cód leibhéal íseal
seans maith go bhfuil fabhtanna caolchúiseacha éagsúla ann, ar féidir iad a ghabháil i bhformhór na dteangacha eile
ach amháin trí thástáil fhairsing agus athbhreithniú cúramach cód ag taithí
fhorbróirí. I Rust, imríonn an tiomsaitheoir ról coimeádaí geata trí dhiúltú
cód a thiomsú leis na fabhtanna do-fheicthe seo, lena n-áirítear fabhtanna comhairgeadra. Trí oibriú
taobh leis an tiomsaitheoir, is féidir leis an bhfoireann a gcuid ama a chaitheamh ag díriú ar na cláir
loighic seachas dul ar thóir fabhtanna.

Tugann Rust uirlisí forbróra comhaimseartha chuig saol ríomhchláraithe na gcóras freisin:

- Déanann lasta, an bainisteoir spleáchais agus an uirlis tógála atá san áireamh, cur leis,
  spleáchais a thiomsú, agus a bhainistiú gan phian agus comhsheasmhach ar fud na Rust
  éiceachóras.
- Cinntíonn an uirlis formáidithe Rustfmt stíl códaithe chomhsheasmhach trasna
  fhorbróirí.
- Cumhachtaíonn an t-anailíseoir Rust Timpeallacht Chomhtháite Forbartha (IDE)
  comhtháthú chun cód a chomhlánú agus teachtaireachtaí earráide inlíne.

Trí úsáid a bhaint as na huirlisí seo agus uirlisí eile in éiceachóras Rust, is féidir le forbróirí a bheith
táirgiúil agus cód leibhéal córais á scríobh.

### Daltaí

Tá Rust ann do mhic léinn agus dóibh siúd ar spéis leo foghlaim faoi chórais
coincheapa. Ag baint úsáide as Rust, tá go leor daoine tar éis foghlaim faoi ábhair mar oibriú
forbairt córas. Tá an pobal an-fháilteach agus sásta freagra a thabhairt
ceisteanna daltaí. Trí iarrachtaí mar an leabhar seo, tá na foirne Rust ag iarraidh
coincheapa córais a dhéanamh níos inrochtana do níos mó daoine, go háirithe iad siúd nach bhfuil nua acu
ríomhchlárú.

### Cuideachtaí

Úsáideann na céadta cuideachtaí, idir bheag agus mhór, Rust i dtáirgeadh éagsúla
tascanna, lena n-áirítear uirlisí líne ordaithe, seirbhísí gréasáin, uirlisí DevOps, leabaithe
gléasanna, anailís fuaime agus físe agus traschódú, cryptocurrencies,
bithfhaisnéisíocht, innill chuardaigh, feidhmchláir Internet of Things, meaisín
foghlama, agus fiú codanna móra de bhrabhsálaí gréasáin Firefox.

### Forbróirí Foinse Oscailte

Tá Rust ann do dhaoine atá ag iarraidh teanga ríomhchláraithe Rust a thógáil, pobail,
uirlisí forbróra, agus leabharlanna. Ba bhreá linn go gcuirfeá leis an Rust
teanga.

### Daoine a bhfuil Luach acu ar Luas agus ar Chobhsaíocht

Tá Rust ann do dhaoine ar mian leo luas agus seasmhacht i dteanga. De réir luais, táimid
Ciallaíonn sé cé chomh tapa agus is féidir le cód Rust rith agus an luas a ligeann Rust duit
cláir a scríobh. Cinntíonn seiceálacha an tiomsaitheora Rust cobhsaíocht trí ghné
breiseanna agus athfhachtóirí. Tá sé seo i gcodarsnacht leis an gcód oidhreachta brittle i
teangacha gan na seiceálacha seo, ar minic go mbíonn eagla ar fhorbróirí iad a mhodhnú. Le
ag iarraidh astarraingtí nialasacha, gnéithe ardleibhéil a thiomsaíonn go
cód leibhéal níos ísle chomh tapa agus a scríobhtar an cód de láimh, déanann Rust a dhícheall a dhéanamh sábháilte
cód a bheith cód tapa chomh maith.

Tá súil ag an teanga Rust tacú le go leor úsáideoirí eile freisin; iad siúd atá luaite
níl anseo ach cuid de na páirtithe leasmhara is mó. Tríd is tríd, Rust is fearr
is é an uaillmhian deireadh a chur leis na comhbhabhtálacha a bhfuil glactha ag ríomhchláraitheoirí leo
blianta trí shábháilteacht _agus_ táirgiúlacht, luas _agus_ eirgeanamaíocht a sholáthar. Tabhair
Déan iarracht Rust agus féach an n-oibríonn a roghanna duit.

## Cé Leis an Leabhar Seo

Glacann an leabhar seo leis go bhfuil cód scríofa agat i dteanga ríomhchlárúcháin eile ach
ní dhéanann sé aon toimhde faoi cé acu. Rinneamar iarracht an t-ábhar a dhéanamh
inrochtana go ginearálta dóibh siúd ó raon leathan de chúlraí clár. muid
ná caith go leor ama ag caint faoi cad is ríomhchlárú _is_ nó conas smaoineamh
faoi. Más rud é go bhfuil tú nua go hiomlán le ríomhchlárú, b'fhearr duit freastal ar
ag léamh leabhar a sholáthraíonn réamhrá go sonrach ar ríomhchlárú.

## Conas an Leabhar Seo a Úsáid

Go ginearálta, glactar leis sa leabhar seo go bhfuil tú ag léamh in ord é ó thús deireadh
ar ais. Tógann caibidlí níos déanaí ar choincheapa i gcaibidlí níos luaithe, agus níos luaithe
b'fhéidir nach ndéanann caibidlí sonraí ar ábhar ar leith a mhionscrúdú ach go dtabharfaidh siad cuairt arís orthu
an topaic i gcaibidil níos déanaí.

Gheobhaidh tú dhá chineál caibidil sa leabhar seo: caibidlí coincheapa agus tionscadail
caibidlí. I gcaibidlí coincheapa, foghlaimeoidh tú faoi ghné de Rust. I dtionscadal
caibidlí, tógfaimid cláir bheaga le chéile

léi, ag cur an méid atá foghlamtha agat i bhfeidhm
i bhfad. Is caibidlí tionscadail iad Caibidil 2, 12, agus 21; is caibidlí coincheapa an chuid eile.

Míníonn Caibidil 1 conas Rust a shuiteáil, conas "Dia duit, domhan!" clár,
agus conas Cargo, bainisteoir pacáiste Rust agus uirlis tógála a úsáid. Tá Caibidil 2 a
réamheolas praiticiúil ar chlár a scríobh i Rust, tar éis duit a
Cluiche buille faoi thuairim uimhreacha. Anseo clúdaímid coincheapa ar ardleibhéal, agus níos déanaí
soláthróidh caibidlí sonraí breise. Más mian leat do lámha a fháil salach
ar an bpointe boise, is é Caibidil 2 an áit chuige sin. Clúdaíonn Caibidil 3 gnéithe Rust
atá cosúil le teangacha cláir eile, agus i gCaibidil 4
beidh tú ag foghlaim faoi chóras úinéireachta Rust. Má tá tú thar a bheith cúramach
foghlaimeoir ar fearr leis gach mionsonra a fhoghlaim sula mbogann tú ar aghaidh go dtí an chéad cheann eile, tusa
b'fhéidir gur mhaith leat gan bacadh le Caibidil 2 agus dul díreach go dtí Caibidil 3, ag filleadh ar Caibidil
2 nuair is mian leat oibriú ar thionscadal ag cur na sonraí atá foghlamtha agat i bhfeidhm.

Caibideal 5 pléann sé struchtúir agus modhanna, agus clúdaíonn Caibideal 6 éumanna, abairtí `match`,
agus an tógáil sreafa rialaithe `if let`. Úsáidfidh tú struchtúir agus
éumanna chun cineálacha saincheaptha a chruthú i Rust.

I gCaibidil 7, foghlaimeoidh tú faoi chóras modúil Rust agus faoi rialacha príobháideachais
chun do chód agus a Chomhéadan Poiblí um Chlárú Feidhmchláir a eagrú
(API). Déantar plé i gCaibidil 8 ar roinnt struchtúir choiteanna maidir le bailiú sonraí a dhéanann an
Soláthraíonn leabharlann caighdeánach, mar shampla veicteoirí, teaghráin, agus léarscáileanna hash. Caibidil 9
déanann sé iniúchadh ar fhealsúnacht agus teicnící láimhseála earráidí Rust.

Dírítear i gCaibidil 10 ar chineálacha, tréithe agus saolréanna, a thugann an chumhacht duit
chun cód a bhaineann le cineálacha iolracha a shainiú. Baineann Caibidil 11 le tástáil,
rud atá riachtanach fiú le ráthaíochtaí sábháilteachta Rust chun do chláir a chinntiú
Tá an loighic ceart. I gCaibidil 12, tógfaimid ár gcur i bhfeidhm féin ar fho-thacar
feidhmiúlacht ón uirlis líne ordaithe `grep` a chuardaíonn téacs
laistigh de chomhaid. Chun seo, bainfimid úsáid as go leor de na coincheapa a phléamar sa
caibidlí roimhe seo.

I gCaibidil 13 déantar iniúchadh ar dhúnadh agus iterators: gnéithe Rust a thagann as
teangacha ríomhchlárúcháin feidhme. I gCaibidil 14, scrúdóimid lasta níos mó
doimhneacht agus labhair faoi na cleachtais is fearr chun do leabharlanna a roinnt le daoine eile.
Pléann Caibidil 15 leideanna cliste a sholáthraíonn an leabharlann chaighdeánach agus an
tréithe a chuireann ar chumas a bhfeidhmiúlachta.

I gCaibidil 16, siúlfaimid trí mhúnlaí éagsúla de ríomhchlárú comhthráthach agus
labhairt faoi conas a chuidíonn Rust leat ríomhchlárú i snáitheanna iolracha gan eagla. I
Caibidil 17, cuirfimid leis sin trí iniúchadh a dhéanamh ar async Rust agus ag fanacht le comhréir agus
an tsamhail concurrency éadrom a thacaíonn siad.

I gCaibidil 18 féachtar ar conas a chuirtear nathanna cainte Rust i gcomparáid le ríomhchlárú atá dírithe ar oibiachtaí
prionsabail a bhféadfadh cur amach a bheith agat orthu.

Is tagairt í Caibidil 19 do phatrúin agus meaitseáil patrún, atá cumhachtach
bealaí chun smaointe a chur in iúl ar fud na gclár Rust. I gCaibidil 20 tá a
smorgasbord ard-ábhair spéise, lena n-áirítear Rust neamhshábháilte, macraí, agus
níos mó faoi shaolréanna, tréithe, cineálacha, feidhmeanna agus dúnta.

I gCaibidil 21, cuirfimid tionscadal i gcrích ina gcuirfimid leibhéal íseal i bhfeidhm
freastalaí gréasáin ilshnáithe!

Ar deireadh, tá eolas úsáideach faoin teanga in aguisíní áirithe a
níos mó formáid tagartha. Clúdaíonn Aguisín A eochairfhocail Rust, Aguisín B
clúdaíonn sé oibreoirí agus siombailí Rust, clúdaíonn Aguisín C tréithe in-díorthaithe
a sholáthraíonn an leabharlann chaighdeánach, clúdaíonn Aguisín D roinnt forbairtí úsáideacha
uirlisí, agus míníonn Aguisín E eagráin Rust. In Aguisín F, is féidir leat a fháil
aistriúcháin ar an leabhar, agus in Aguisín G clúdóidh muid conas a dhéantar Rust agus
cad é Rust oíche.

Níl aon bhealach mícheart leis an leabhar seo a léamh: más mian leat dul ar aghaidh, téigh chuige!
Seans go mbeidh ort léim siar chuig caibidlí níos luaithe má bhíonn taithí agat ar aon cheann díobh
mearbhall. Ach déan cibé rud a oibríonn duit.

<span id="ferris"></span>

Cuid thábhachtach den phróiseas foghlama Rust is ea foghlaim conas léamh an
teachtaireachtaí earráide a thaispeánann an tiomsaitheoir: treoróidh siad seo tú i dtreo an chóid oibre.
Mar sin, cuirfimid go leor samplaí ar fáil nach dtiomsóidh mar aon leis an earráid
teachtaireacht a thaispeánfaidh an tiomsaitheoir duit i ngach cás. Bíodh a fhios sin má théann tú isteach
agus sampla randamach a rith, ní fhéadfaidh sé a thiomsú! Bí cinnte go léann tú an
téacs mórthimpeall féachaint an bhfuil sé i gceist an sampla a bhfuil tú ag iarraidh a rith a rith
earráid. Cabhróidh Ferris leat freisin idirdhealú a dhéanamh ar chód nach bhfuil i gceist a bheith ag obair:

| Ferris                                                                                                              | Brí                                                   |
| ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| <img src="img/ferris/does_not_compile.svg" class="ferris-explain" alt="Ferris le comhartha ceiste"/>                | Ní thiomsaíonn an cód seo!                            |
| <img src="img/ferris/panics.svg" class="ferris-explain" alt="Ferris ag caitheamh a lámha"/>                         | Caoileann an cód seo!                                 |
| <img src="img/ferris/not_desired_behavior.svg" class="ferris-explain" alt="Ferris le crúb amháin suas, shrugging"/> | Ní tháirgeann an cód seo an t-iompar atá ag teastáil. |

I bhformhór na gcásanna, beidh muid tú a threorú chuig an leagan ceart d'aon chód sin ní thiomsaíonn.

## Cód Foinse

Is féidir na comhaid foinse óna gineadh an leabhar seo a fháil ar
[GitHub][leabhar].

[leabhar]: https://github.com/rust-lang/book/tree/main/src
