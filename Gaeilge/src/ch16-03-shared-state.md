## Comhthráthacht Comhroinnte

Is bealach breá é teachtaireachtaí a sheoladh chun comhthráthacht a láimhseáil, ach ní hé an t-aon cheann amháin é. Modh eile a bheadh ​​ann ná go mbeadh rochtain ag ilshnáitheanna ar na sonraí comhroinnte céanna. Smaoinigh ar an gcuid seo den mana ó dhoiciméadú teanga Go
arís: "ná déan cumarsáid trí chuimhne a roinnt."

Cén chuma a bheadh ​​ar chumarsáid trí chuimhne a roinnt? Ina theannta sin, cén fáth a
dtabharfadh díograiseoirí teachtaireachtaí rabhadh gan comhroinnt cuimhne a úsáid?

Ar bhealach, tá bealaí in aon teanga ríomhchlárúcháin cosúil le húinéireacht aonair,
mar nuair a aistríonn tú luach síos cainéal, níor cheart duit an luach sin a úsáid a thuilleadh. Tá comhthráthacht chuimhne comhroinnte cosúil le húinéireacht iolrach: is féidir le ilshnáitheanna
rochtain a fháil ar an suíomh cuimhne céanna ag an am céanna. Mar a chonaic tú i gCaibidil 15,
áit ar chuir pointeoirí cliste úinéireacht iolrach ar fáil, is féidir le húinéireacht iolrach
castacht a chur leis toisc go gcaithfear na húinéirí éagsúla seo a bhainistiú. Cuidíonn córas cineáil Rust
agus rialacha úinéireachta go mór leis an mbainistíocht seo a fháil i gceart. Mar shampla, féachaimis ar mhútéacsanna, ceann de na bunghnéithe comhthráthachta is coitianta
le haghaidh cuimhne comhroinnte.

### Úsáid Mutexanna chun Rochtain ar Shonraí a Cheadú ó Shnáithe Amháin ag an Am

Is giorrúchán é _Mutex_ do _eisiamh frithpháirteach_, mar atá, ní cheadaíonn mutex ach do
shnáithe amháin rochtain a fháil ar shonraí áirithe ag aon am ar leith. Chun rochtain a fháil ar na sonraí i
mutex, ní mór do shnáithe a chur in iúl ar dtús go bhfuil rochtain uaidh trí iarraidh _glas_ an
mutex a fháil. Is struchtúr sonraí é an glas atá mar chuid den mutex a
choinníonn súil ar cé a bhfuil rochtain eisiach aige ar na sonraí faoi láthair. Dá bhrí sin, déantar cur síos ar an
mutex mar _chosaint_ na sonraí atá aige tríd an gcóras glasála.

Tá cáil ar Mutexanna as a bheith deacair a úsáid mar caithfidh tú
dhá riail a mheabhrú:

- Ní mór duit iarracht a dhéanamh an glas a fháil sula n-úsáideann tú na sonraí.
- Nuair a bheidh tú críochnaithe leis na sonraí a chosnaíonn an mutex, ní mór duit na sonraí a dhíghlasáil
ionas gur féidir le snáitheanna eile an glas a fháil.

Mar mheafar fíorshaoil ​​do mutex, samhlaigh plé painéil ag
comhdháil le micreafón amháin. Sula bhféadann painéalaí labhairt, caithfidh siad a iarraidh nó comhartha a thabhairt gur mian leo an micreafón a úsáid. Nuair a fhaigheann siad an micreafón, is féidir leo labhairt chomh fada agus is mian leo agus ansin an micreafón a thabhairt don chéad phainéalaí eile a iarrann labhairt. Má dhéanann painéalaí dearmad an micreafón a thabhairt dóibh nuair a bhíonn siad críochnaithe leis, ní bheidh aon duine eile in ann labhairt. Mura n-oibríonn bainistíocht an mhicreafóin chomhroinnte, ní oibreoidh an painéal mar a bhí beartaithe!

Is féidir go mbeadh sé thar a bheith deacair bainistíocht mutex a dhéanamh i gceart, agus sin an fáth go bhfuil an oiread sin daoine díograiseach faoi chainéil. Mar sin féin, a bhuíochas le córas cineáil agus rialacha úinéireachta Rust, ní féidir leat dul i ngleic le glasáil agus díghlasáil.

#### API `Mutex<T>`

Mar shampla de conas mutex a úsáid, déanaimis tosú trí mutex a úsáid i gcomhthéacs aon-snáithe, mar a thaispeántar i Liostáil 16-12:

<Listing number="16-12" file-name="src/main.rs" caption="Exploring the API of `Mutex<T>` in a single-threaded context for simplicity">

```rust
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-12/src/main.rs}}
```

</Listing>

Mar is amhlaidh le go leor cineálacha, cruthaímid `Mutex<T>` ag baint úsáide as an bhfeidhm ghaolmhar `new`.
Chun rochtain a fháil ar na sonraí taobh istigh den mutex, úsáidimid an modh `lock` chun an
glas a fháil. Cuirfidh an glao seo bac ar an snáithe reatha ionas nach féidir leis aon obair a dhéanamh go dtí
go mbeidh sé inár seal an glas a bheith againn.

Theipfeadh ar an nglao ar `lock` dá mbeadh scaoll ar snáithe eile a bhfuil an glas aige. Sa
chás sin, ní bheadh ​​​​aon duine in ann an glas a fháil riamh, mar sin roghnaigh muid `unwrap` agus an snáithe seo a bheith i scaoll má bhímid sa chás sin.

Tar éis dúinn an glas a fháil, is féidir linn an luach fillte, ar a dtugtar `num` sa
chás seo, a láimhseáil mar thagairt inathraithe do na sonraí taobh istigh. Cinntíonn an córas cineáil
go bhfaighimid glas sula n-úsáidimid an luach i `m`. Is é `Mutex<i32>` cineál `m`, ní `i32`, mar sin _ní mór_ dúinn glaoch ar `lock` chun go mbeimid in ann an luach `i32` a úsáid. Ní féidir linn dearmad a dhéanamh; ní ligfidh an córas cineáil dúinn rochtain a fháil ar an `i32` istigh
ar shlí eile.

Mar a d'fhéadfá a cheapadh, is pointeoir cliste é `Mutex<T>`. Níos cruinne, tugann an glao
chun `glasáil` _ar ais_ pointeoir cliste ar a dtugtar `MutexGuard`, fillte i
`LockResult` a láimhseáil muid leis an nglao chun `unwrap`. Cuireann an pointeoir cliste `MutexGuard` `Deref` i bhfeidhm chun pointeáil ar ár sonraí istigh; tá cur i bhfeidhm `Drop` ag an bpointeoir cliste freisin
a scaoileann an glas go huathoibríoch nuair a théann
`MutexGuard` lasmuigh den raon feidhme, rud a tharlaíonn ag deireadh an raon feidhme istigh. Mar thoradh air sin, níl an baol ann go ndéanaimid dearmad an glas a scaoileadh agus bac a chur ar an mutex
ó bheith á úsáid ag snáitheanna eile, toisc go dtarlaíonn an scaoileadh glas
go huathoibríoch.

Tar éis an glas a scaoileadh, is féidir linn an luach mutex a phriontáil agus a fheiceáil gur éirigh linn an `i32` istigh a athrú go 6.

#### `Mutex<T>` a roinnt idir snáitheanna iolracha

Anois, déanaimis iarracht luach a roinnt idir snáitheanna iolracha ag baint úsáide as `Mutex<T>`.
Déanfaimid 10 snáithe a chasadh suas agus méadóimid luach cuntair faoi 1, ionas
go dtéann an cuntar ó 0 go 10. Beidh earráid tiomsaitheora sa chéad sampla eile i Liosta 16-13, agus úsáidfimid an earráid sin chun níos mó a fhoghlaim faoi úsáid `Mutex<T>` agus conas a chabhraíonn Rust linn é a úsáid i gceart.

<Listing number="16-13" file-name="src/main.rs" caption="Ten threads each increment a counter guarded by a `Mutex<T>`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-13/src/main.rs}}
```

</Listing>

Cruthaímid athróg `counter` chun `i32` a choinneáil taobh istigh de `Mutex<T>`, mar a rinneamar i Liostáil 16-12. Ansin, cruthaímid 10 snáithe trí athrá a dhéanamh thar raon uimhreacha. Úsáidimid `thread::spawn` agus tugann muid an dúnadh céanna do na snáitheanna go léir: ceann a bhogann an t-counter isteach sa snáithe, a fhaigheann glas ar an `Mutex<T>` trí ghlaoch ar an modh `lock`, agus ansin cuireann sé 1 leis an luach sa mutex. Nuair a chríochnaíonn snáithe a dhúnadh, rachaidh `num` as raon feidhme agus scaoilfidh sé an
glas ionas gur féidir le snáithe eile é a fháil.

Sa phríomhshnáithe, bailímid na láimhseálacha join go léir. Ansin, mar a rinneamar i Liostáil 16-2, glaoimid `join` ar gach láimhseáil chun a chinntiú go gcríochnaíonn na snáitheanna go léir. Ag an bpointe sin, gheobhaidh an príomhshnáithe an glas agus priontálfaidh sé toradh an chláir seo.

Thugamar le fios nach ndéanfadh an sampla seo a thiomsú. Anois, déanaimis a fháil amach cén fáth!

```console
{{#include ../../listings/ch16-fearless-concurrency/listing-16-13/output.txt}}
```


Deir an teachtaireacht earráide gur aistríodh luach an `counter` san athrá roimhe seo den lúb. Tá Rust ag insint dúinn nach féidir linn úinéireacht `counter` a bhogadh isteach i snáitheanna iolracha. Déanaimis an earráid tiomsaitheora a shocrú le modh ilúinéireachta a phléamar i gCaibidil 15.

#### Ilúinéireacht le Snáitheanna Iolracha

I gCaibidil 15, thugamar luach ilúinéirí trí úsáid a bhaint as an pointeoir cliste `Rc<T>` chun luach comhaireamh tagartha a chruthú. Déanaimis an rud céanna anseo agus feicfimid cad a tharlaíonn. Fillfimid an `Mutex<T>` i `Rc<T>` i Liostáil 16-14 agus clónálfaimid an `Rc<T>` sula mbogfaimid úinéireacht chuig an snáithe.

<Listing number="16-14" file-name="src/main.rs" caption="Attempting to use `Rc<T>` to allow multiple threads to own the `Mutex<T>`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-14/src/main.rs}}
```

</Listing>

Arís eile, déanaimid tiomsú agus faighimid... earráidí difriúla! Tá an tiomsaitheoir ag múineadh go leor dúinn.

```console
{{#include ../../listings/ch16-fearless-concurrency/listing-16-14/output.txt}}
```

Ó, tá an teachtaireacht earráide sin an-fhoclach! Seo an chuid thábhachtach le díriú air:
`` `Rc<Mutex<i32>>` cannot be sent between threads safely  ``. Tá an tiomsaitheoir ag
insint dúinn an chúis freisin: `` the trait `Send` is not implemented for
`Rc<Mutex<i32>>` ``. Labhróimid faoi `Send` sa chéad chuid eile: is ceann de
na tréithe é a chinntíonn go bhfuil na cineálacha a úsáidimid le snáitheanna ceaptha lena n-úsáid i
gcásanna comhthráthacha.

Ar an drochuair, níl `Rc<T>` sábháilte a roinnt trasna snáitheanna. Nuair a bhainistíonn `Rc<T>`
an comhaireamh tagartha, cuireann sé leis an gcomhaireamh do gach glao chuig `clone` agus
baineann sé ón gcomhaireamh nuair a scaoiltear gach clón. Ach ní úsáideann sé aon
bhunphrionsabail chomhthráthacha chun a chinntiú nach féidir le snáithe eile
cur isteach ar athruithe ar an gcomhaireamh. D’fhéadfadh sé seo a bheith ina chúis le comhaireamh mícheart—fabhtanna caolchúiseacha a
d’fhéadfadh sceitheanna cuimhne nó luach a chailleadh sula mbeidh muid críochnaithe
leis. Is cineál atá díreach cosúil le `Rc<T>` atá de dhíth orainn ach ceann a dhéanann athruithe
ar an gcomhaireamh tagartha ar bhealach atá sábháilte ó thaobh snáithe de.

#### Comhaireamh Tagartha Adamhach le `Arc<T>`

Ar ámharaí an tsaoil, is cineál cosúil le `Rc<T>` é `Arc<T>` atá sábháilte le húsáid i
gcásanna comhthráthacha. Seasann an _a_ do _atomic_, rud a chiallaíonn gur cineál _adamhach
comhairimh_ tagartha é. Is cineál breise comhthráthachta
bunaidh iad adamhach nach gclúdóimid go mion anseo: féach ar an doiciméadú
leabharlainne caighdeánach le haghaidh [`std::sync::atomic`][atomic]<!-- neamhaird --> le haghaidh tuilleadh
sonraí. Ag an bpointe seo, níl le déanamh agat ach a fhios a bheith agat go n-oibríonn adamhach cosúil le cineálacha
bunaidh ach go bhfuil siad sábháilte a roinnt trasna snáitheanna.

B’fhéidir go mbeadh iontas ort ansin cén fáth nach bhfuil gach cineál primitive adamhach agus cén fáth nach gcuirtear cineálacha caighdeánacha leabharlainne i bhfeidhm chun `Arc<T>` a úsáid de réir réamhshocraithe. Is é an chúis atá leis sin ná go dtagann pionós feidhmíochta le sábháilteacht snáithe nach mian leat a íoc ach nuair a
bhíonn gá agat leis i ndáiríre. Má tá tú ag déanamh oibríochtaí ar luachanna laistigh de
shnáithe amháin, is féidir le do chód rith níos tapúla mura gá dó na
ráthaíochtaí a sholáthraíonn adamhach a fhorfheidhmiú.

Fillfimid ar ár sampla: Tá an API céanna ag `Arc<T>` agus `Rc<T>`, mar sin socraímid
ár gclár tríd an líne `use`, an glao go `new`, agus an glao go
`clone` a athrú. Tiomsóidh agus rithfidh an cód i Liosta 16-15 sa deireadh:

<Listing number="16-15" file-name="src/main.rs" caption="Using an `Arc<T>` to wrap the `Mutex<T>` to be able to share ownership across multiple threads">

```rust
{{#rustdoc_include ../../listings/ch16-fearless-concurrency/listing-16-15/src/main.rs}}
```

</Listing>

Priontálfaidh an cód seo an méid seo a leanas:

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the threads running differently rather than
changes in the compiler -->

```text
Result: 10
```

Rinneamar é! Chomhaireamhamar ó 0 go 10, rud nach mbeadh an-suntasach b'fhéidir, ach mhúin sé go leor dúinn faoi `Mutex<T>` agus sábháilteacht snáitheanna. D'fhéadfá struchtúr an chláir seo a úsáid freisin chun oibríochtaí níos casta a dhéanamh ná díreach cuntar a mhéadú. Ag baint úsáide as an straitéis seo, is féidir leat ríomh a roinnt ina chodanna neamhspleácha, na codanna sin a roinnt thar shnáitheanna, agus ansin `Mutex<T>` a úsáid chun go ndéanfaidh gach
snáithe an toradh deiridh a nuashonrú lena chuid.

Tabhair faoi deara, má tá tú ag déanamh oibríochtaí uimhriúla simplí, go bhfuil cineálacha níos simplí ann
ná cineálacha `Mutex<T>` arna soláthar ag an modúl [`std::sync::atomic` den
leabharlann chaighdeánach][atomic]<!-- ignore -->. Soláthraíonn na cineálacha seo rochtain shábháilte, chomhuaineach,
adamhach ar chineálacha primitive. Roghnaíomar `Mutex<T>` a úsáid le cineál primitive
don sampla seo ionas go bhféadfaimis díriú ar an gcaoi a n-oibríonn `Mutex<T>`.

### Cosúlachtaí idir `RefCell<T>`/`Rc<T>` agus `Mutex<T>`/`Arc<T>`

B’fhéidir gur thug tú faoi deara nach féidir an `counter` a athrú ach go bhféadfaimis tagairt inathraithe a fháil don luach atá istigh ann; ciallaíonn sé seo go soláthraíonn `Mutex<T>` inathraitheacht inmheánach, mar a dhéanann an teaghlach `Cell`. Ar an gcaoi chéanna a d’úsáideamar `RefCell<T>` i
gCaibidil 15 chun ligean dúinn ábhar a athrú laistigh de `Rc<T>`, úsáidimid `Mutex<T>` chun ábhar a athrú laistigh de `Arc<T>`.

Sonra eile le tabhairt faoi deara ná nach féidir le Rust tú a chosaint ó gach cineál earráide loighce
nuair a úsáideann tú `Mutex<T>`. Cuimhnigh i gCaibidil 15 gur tháinig an baol timthriallta tagartha a chruthú le húsáid `Rc<T>`, áit a dtagraíonn dhá luach `Rc<T>` dá chéile, rud a fhágann sceitheanna cuimhne. Ar an gcaoi chéanna, tá an baol ann go gcruthófar _deadlocks_ le `Mutex<T>`. Tarlaíonn siad seo nuair a bhíonn ar oibríocht dhá acmhainn a ghlasáil
agus nuair a bhíonn ceann de na glais faighte ag dhá shnáithe, rud a fhágann go bhfanann siad
le chéile go deo. Más spéis leat deadlocks, déan iarracht clár Rust a chruthú
a bhfuil deadlock ann; ansin déan taighde ar straitéisí maolaithe deadlock do
mutexes in aon teanga agus déan iarracht iad a chur i bhfeidhm i Rust. Cuireann
an doiciméadú caighdeánach leabharlainne API do `Mutex<T>` agus `MutexGuard`
eolas úsáideach ar fáil.

Cuirfimid clabhsúr ar an gcaibidil seo trí labhairt faoi na tréithe `Send` agus `Sync` agus
conas is féidir linn iad a úsáid le cineálacha saincheaptha.

[atomic]: ../std/sync/atomic/index.html