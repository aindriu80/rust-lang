## Saintréithe Teangacha Dírithe ar Réada

Níl aon chomhthuiscint sa phobal ríomhchlárúcháin faoi na gnéithe a chaithfidh a bheith ag
teanga le go measfaí gur teanga dhírithe ar réada í. Tá tionchar ag go leor
paraidímí ríomhchlárúcháin ar meirg, lena n-áirítear OOP; mar shampla, rinneamar iniúchadh ar na gnéithe
a tháinig ó ríomhchlárú feidhmiúil i gCaibidil 13. Is féidir a rá go bhfuil tréithe coitianta áirithe ag teangacha OOP, eadhon réada, ionchapslú, agus
oidhreacht. Féachfaimid ar a bhfuil i gceist le gach ceann de na tréithe sin agus an
tacaíonn
Rust leis.

### Tá Sonraí agus Iompar i Réada

Is catalóg de phatrúin dearaidh dírithe ar réada é an leabhar _Design Patterns: Elements of Reusable Object-Oriented Software_ le
Erich Gamma, Richard Helm, Ralph Johnson, agus John Vlissides (Addison-Wesley
Professional, 1994), ar a dtugtar _The Gang of Four_ go comhráiteach. Sainmhíníonn sé OOP ar an mbealach seo:

> Tá cláir dhírithe ar réada déanta suas de réada. Pacálann _object_ sonraí agus na nósanna imeachta a oibríonn ar na sonraí sin araon. De ghnáth, tugtar _methods_ nó _operations_ ar na nósanna imeachta.

Ag baint úsáide as an sainmhíniú seo, tá Rust dírithe ar réada: bíonn sonraí ag struchtúir agus enums,
agus soláthraíonn bloic `impl` modhanna ar struchtúir agus enums. Cé nach dtugtar _réada_ ar struchtúir agus
enums le modhanna, soláthraíonn siad an
fheidhmiúlacht chéanna, de réir sainmhíniú Gang of Four ar réada.

### Capsúlú a Cheileann Sonraí Cur i bhFeidhm

Gné eile a bhaineann go coitianta le OOP ná an coincheap _capsúlú_,
rud a chiallaíonn nach bhfuil sonraí cur i bhfeidhm réada inrochtana ag
cód a úsáideann an réada sin. Dá bhrí sin, is é an t-aon bhealach chun idirghníomhú le réad ná
trína API poiblí; níor cheart go mbeadh cód a úsáideann an réada in ann teacht isteach in
inmheánaigh an réada agus sonraí nó iompar a athrú go díreach. Cuireann sé seo ar chumas an
chláraitheora inmheánacha réada a athrú agus a athfhachtóireacht gan a bheith orthu
an cód a úsáideann an réad a athrú.

Phléamar conas an ionchapslú a rialú i gCaibidil 7: is féidir linn an eochairfhocal `pub` a úsáid chun a chinneadh cé na modúil, na cineálacha, na feidhmeanna agus na modhanna inár gcód
ba chóir a bheith poiblí, agus de réir réamhshocraithe bíonn gach rud eile príobháideach. Mar shampla, is féidir linn
struchtúr `AveragedCollection` a shainiú ina bhfuil réimse ina bhfuil veicteoir
de luachanna `i32`. Is féidir leis an struchtúr réimse a bheith aige freisin ina bhfuil meán na
luachanna sa veicteoir, rud a chiallaíonn nach gá an meán a ríomh
ar éileamh aon uair a bhíonn sé de dhíth ar aon duine. I bhfocail eile, déanfaidh `AveragedCollection`
an meán ríofa a thaisceadh dúinn. Tá sainmhíniú an
struchtúir `AveragedCollection` i Liostáil 18-1:

<Listing number="18-1" file-name="src/lib.rs" caption="An `AveragedCollection` struct that maintains a list of integers and the average of the items in the collection">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-01/src/lib.rs}}
```

</Listing>


Tá an struchtúr marcáilte mar `pub` ionas gur féidir le cód eile é a úsáid, ach fanann na réimsí laistigh den struchtúr príobháideach. Tá sé seo tábhachtach sa chás seo mar ba mhaith linn a chinntiú go ndéantar an meán a nuashonrú freisin aon uair a chuirtear luach leis an liosta nó a bhaintear den liosta. Déanaimid é seo trí mhodhanna `add`, `remove`, agus `average` a chur i bhfeidhm ar an struchtúr, mar a thaispeántar i Liostáil 18-2:

<Listing number="18-2" file-name="src/lib.rs" caption="Implementations of the public methods `add`, `remove`, and `average` on `AveragedCollection`">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-02/src/lib.rs:here}}
```

</Listing>

Is iad na modhanna poiblí `add`, `remove`, agus `average` na bealaí amháin chun rochtain a fháil ar shonraí nó iad a mhodhnú i gcás de `AveragedCollection`. Nuair a chuirtear mír le `list` ag baint úsáide as an modh `add` nó a bhaintear í ag baint úsáide as an modh `remove`, glaonn cur i bhfeidhm gach ceann acu ar an modh príobháideach `update_average` a láimhseálann
nuashonrú an réimse `average` chomh maith.

Fágaimid na réimsí `list` agus `average` príobháideach ionas nach bhfuil aon bhealach ann do chód seachtrach míreanna a chur leis an réimse `list` nó a bhaint de go díreach; ar shlí eile, d'fhéadfadh an réimse `meán` a bheith as sioncrón nuair a athraíonn an `liosta`. Tugann an modh `meán` an luach ar ais sa réimse `meán`, rud a ligeann don chód seachtrach an `meán` a léamh ach gan é a mhodhnú.

Toisc gur chuireamar sonraí cur i bhfeidhm an struchtúir `AveragedCollection` i bhfolach, is féidir linn gnéithe, amhail an struchtúr sonraí, a athrú go héasca sa todhchaí. Mar shampla, d'fhéadfaimis `HashSet<i32>` a úsáid in ionad
`Vec<i32>` don réimse `liosta`. Chomh fada agus a fhanann sínithe na modhanna poiblí `add`,
`remove`, agus `meán` mar a chéile, ní bheadh ​​​​gá le cód a úsáideann
`AveragedCollection` a athrú chun é a thiomsú. Dá ndéanfaimis `list` a phoibliú ina ionad sin, ní bheadh ​​sé seo amhlaidh go riachtanach: tá modhanna difriúla ag `HashSet<i32>` agus `Vec<i32>` chun míreanna a chur leis agus a bhaint, mar sin is dócha go mbeadh ar an gcód seachtrach
athrú dá mbeadh sé ag modhnú `list` go díreach.

Más gné riachtanach é an t-ionchapslú chun go measfaí teanga a bheith
dírithe ar réada, comhlíonann Rust an riachtanas sin. Cuireann an rogha `pub` nó
gan a úsáid le haghaidh codanna éagsúla den chód ar chumas sonraí cur i bhfeidhm a ionchapslú.

### Oidhreacht mar Chóras Cineál agus mar Chomhroinnt Cód

Is meicníocht í _Oidhreacht_ trína bhféadann réad eilimintí a oidhreacht ó
shainmhíniú réada eile, agus ar an gcaoi sin sonraí agus iompar an réada tuismitheora a fháil
gan ort iad a shainmhíniú arís.

Mura gcaithfidh oidhreacht a bheith ag teanga le bheith ina teanga dhírithe ar réada, ansin
ní teanga í Rust. Níl aon bhealach ann struchtúr a shainiú a oidhreachtaíonn réimsí agus cur i bhfeidhm modhanna an
struchtúir tuismitheora gan macra a úsáid.

Mar sin féin, má tá tú cleachtaithe le hoidhreacht a bheith i do bhosca uirlisí cláir, is féidir leat
réitigh eile i Rust a úsáid, ag brath ar do chúis le teacht ar
oidhreacht sa chéad áit.

Roghnófá oidhreacht ar dhá phríomhchúis. Ceann amháin ná athúsáid cód:
is féidir leat iompar ar leith a chur i bhfeidhm do chineál amháin, agus cuireann oidhreacht ar do chumas
an cur i bhfeidhm sin a athúsáid do chineál difriúil. Is féidir leat é seo a dhéanamh ar bhealach teoranta i gcód Rust ag baint úsáide as cur i bhfeidhm modhanna tréithe réamhshocraithe, a chonaic tú i
Liostáil 10-14 nuair a chuireamar cur i bhfeidhm réamhshocraithe den mhodh `summarize` leis an tréith `Summary`. Bheadh ​​an modh `summarize` ar fáil ar aon chineál a chuireann an tréith `Summary` i bhfeidhm gan aon chód breise. Tá sé seo
cosúil le rang tuismitheora a bhfuil cur i bhfeidhm modha aige agus rang linbh oidhreachta a bhfuil cur i bhfeidhm an mhodha aige freisin. Is féidir linn
cur i bhfeidhm réamhshocraithe an mhodha `summarize` a shárú freisin nuair a
chuirimid an tréith `Summary` i bhfeidhm, atá cosúil le rang linbh a sháraíonn
cur i bhfeidhm modha a oidhreachtaíodh ó rang tuismitheora.

Baineann an chúis eile le hoidhreacht a úsáid leis an gcóras cineáil: chun
cineál linbh a chumasú a úsáid sna háiteanna céanna leis an gcineál tuismitheora. Tugtar _polamorfacht_ air seo freisin, rud a chiallaíonn gur féidir leat ilréad a chur in ionad
a chéile ag am rith má roinneann siad tréithe áirithe.

> ### Polamorfacht
>
> Do go leor daoine, is comhchiallach le hoidhreacht an focal polamorfacht. Ach is
> coincheap níos ginearálta é i ndáiríre a thagraíonn do chód ar féidir leis oibriú le sonraí
> de chineálacha éagsúla. Maidir le hoidhreacht, is fo-aicmí iad na cineálacha sin de ghnáth.
>
> Ina áit sin, úsáideann Rust cineálacha chun teibí a dhéanamh thar chineálacha éagsúla féideartha agus
> teorainneacha tréithe chun srianta a fhorchur ar a gcaithfidh na cineálacha sin a sholáthar. Tugtar _polamorfacht pharaiméadrach teoranta_ air seo uaireanta.

Tá oidhreacht imithe as fabhar le déanaí mar réiteach dearaidh ríomhchlárúcháin
i go leor teangacha ríomhchlárúcháin toisc go mbíonn baol ann go minic go roinnfear níos mó cóid
ná mar is gá. Níor cheart go roinnfeadh fo-aicmí tréithe uile a
ranga tuismitheora i gcónaí ach déanfaidh siad amhlaidh le hoidhreacht. Is féidir leis seo dearadh cláir a dhéanamh
níos lú solúbtha. Tugann sé seo isteach an fhéidearthacht freisin modhanna a ghlaoch ar
fho-aicmí nach bhfuil ciall leo nó a chruthaíonn earráidí toisc nach mbaineann na modhanna
leis an bhfo-aicme. Ina theannta sin, ní cheadóidh roinnt teangacha ach oidhreacht aonair (rud a chiallaíonn nach féidir le fo-aicme ach oidhreacht a fháil ó aon aicme amháin), rud a chuireann srian breise ar sholúbthacht dhearadh cláir.

Ar na cúiseanna seo, glacann Rust cur chuige difriúil maidir le húsáid a bhaint as réada tréithe in ionad oidhreachta. Féachfaimid ar an gcaoi a gcuireann réada tréithe polamorfacht ar chumas i Rust.