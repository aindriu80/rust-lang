## Sreabhadh Rialaithe

An cumas roinnt cód a rith ag brath ar cibé an bhfuil coinníoll `true` agus go
reáchtáil roinnt cód arís agus arís eile cé go bhfuil coinníoll `true` mar bhunchlocha tógála
i bhformhór na dteangacha ríomhchlárúcháin. Na constructs is coitianta a ligeann duit a rialú
is ionann sreabhadh forghníomhaithe an chóid Rust agus `if` nathanna agus lúba.

### `if` Nathanna

Ligeann slonn `if` duit do chód a chraobhscaoileadh ag brath ar choinníollacha. tu
cuir coinníoll ar fáil agus ansin luaigh, “Má shásaítear an coinníoll seo, rith an bloc seo
de chód. Mura gcomhlíontar an coinníoll, ná rith an bloc cód seo."

Cruthaigh tionscadal nua darb ainm _branches_ i d’eolaire _projects_ le fiosrú
an abairt `if`. Sa chomhad _src/main.rs_, cuir an méid seo a leanas isteach:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-26-if-true/src/main.rs}}
```

Tosaíonn gach nathanna `if` leis an eochairfhocal `if`, agus coinníoll ina dhiaidh sin. I
sa chás seo, seiceálann an riocht cibé an bhfuil nó nach bhfuil ag an `number` athróg
luach níos lú ná 5. Cuirimid an bloc cód a fhorghníomhú má tá an coinníoll
`true` díreach tar éis an riocht taobh istigh de lúibíní curly. Bloic cód
a bhaineann leis na coinníollacha i `if` tugtar _arms_ uaireanta ar na habairtí,
díreach cosúil leis na hairm sna habairtí `match` a phléamar sa [“Comparáid
an Buille faoi thuairim leis an Uimhir Rúnda”][comparing-the-guess-to-the-secret-number]<!--
neamhaird a dhéanamh ar --> alt de Chaibidil 2.

Roghnach, is féidir linn slonn `else` a chur san áireamh freisin, rud a roghnaigh muid a dhéanamh
anseo, chun bloc eile de chód a thabhairt don chlár le forghníomhú má tá an
riocht luacháil go `false`. Mura dtugann tú slonn `else` agus
is é an coinníoll `false`, ní dhéanfaidh an clár ach an bloc `if` a scipeáil agus bogadh ar aghaidh
go dtí an chéad phíosa eile de chód.

Bain triail as an gcód seo a rith; ba cheart duit an t-aschur seo a leanas a fheiceáil:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-26-if-true/output.txt}}
```

Déanaimid iarracht luach `number` a athrú go luach a dhéanann an riocht
`false` féachaint cad a tharlaíonn:

```rust,ignore
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-27-if-false/src/main.rs:here}}
```

Rith an clár arís, agus féach ar an aschur:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-27-if-false/output.txt}}
```

Is fiú a thabhairt faoi deara freisin go gcaithfidh an coinníoll sa chód seo _a bheith_ ina `bool`. Más rud é
ní `bool` é an coinníoll, gheobhaidh muid earráid. Mar shampla, bain triail as ag rith an
cód seo a leanas:

<span class="filename">Filename: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-28-if-condition-must-be-bool/src/main.rs}}
```

Measann an riocht `if` go luach `3` an uair seo, agus caitheann Rust an
earráid:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-28-if-condition-must-be-bool/output.txt}}
```

Léiríonn an earráid go raibh Rust ag súil le `bool` ach go bhfuair sé slánuimhir. Murab ionann agus
teangacha ar nós Ruby agus JavaScript, ní dhéanfaidh Rust iarracht go huathoibríoch é
cineálacha neamh-Boolean a thiontú go Boole. Caithfidh tú a bheith follasach agus a chur ar fáil i gcónaí
`if` le Boole mar a riocht. Más mian linn an bloc cód `if` a rith
ach amháin nuair nach bhfuil uimhir cothrom le `0`, mar shampla, is féidir linn an `if` a athrú
léiriú ar an méid seo a leanas:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-29-if-not-equal-0/src/main.rs}}
```

Má reáchtálann tú an cód seo, priontálfar `number was something other than zero`.

#### Láimhseáil Coinníollacha Il le `else if`

Is féidir leat coinníollacha iolracha a úsáid trí `if` agus `else` a chur le chéile i `else if`
léiriú. Mar shampla:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-30-else-if/src/main.rs}}
```

Tá ceithre chosán féideartha ag an gclár seo ar féidir leis a ghlacadh. Tar éis é a rith, ba chóir duit
féach an t-aschur seo a leanas:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-30-else-if/output.txt}}
```

Nuair a fheidhmíonn an clár seo, seiceálann sé gach slonn `if` ar a seal agus ritheann sé
an chéad chorp a ndéanann an riocht meastóireacht air go `true`. Tabhair faoi deara go fiú
cé go bhfuil 6 inroinnte ar 2, ní fheicimid go bhfuil an  `number is divisible by 2`,
agus ní fheicimid nach bhfuil an `number is not divisible by 4, 3, or 2` téacs as an `else`
bloc. Sin toisc nach ndéanann Rust ach an bloc a fhorghníomhú don chéad `true`
riocht, agus nuair a fhaigheann sé ceann, ní seiceálann sé fiú an chuid eile.

Ag baint úsáide as an iomarca `else if` nathanna is féidir do chód tranglam, mar sin má tá níos mó agat
seachas ceann amháin, b'fhéidir gur mhaith leat do chód a athfhachtóiriú. Déanann Caibidil 6 cur síos ar chumhachtach
Tógáil branching Rust ar a dtugtar `match` do na cásanna seo.

#### Ag baint úsáide `if` i Ráiteas `let`

Toisc gur slonn é `if`, is féidir linn é a úsáid ar thaobh na láimhe deise de `let`
ráiteas chun an toradh a shannadh d’athróg, mar atá i Liostú 3-2.

<Listing number="3-2" file-name="src/main.rs" caption="Ag sannadh toradh slonn `if` d'athróg">

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/listing-03-02/src/main.rs}}
```

</Listing>

Beidh an athróg `number` ceangailte de réir luach a bheidh bunaithe ar thoradh an `if`
léiriú. Rith an cód seo chun a fheiceáil cad a tharlaíonn:

```console
{{#include ../../listings/ch03-common-programming-concepts/listing-03-02/output.txt}}
```

Cuimhnigh go bhfuil bloic de chód a mheas go dtí an slonn deiridh iontu, agus
is nathanna cainte iad uimhreacha leo féin freisin. Sa chás seo, luach an
iomlán `if` abairt ar an bloc cód a fhorghníomhú. Ciallaíonn sé seo an
ní mór luachanna a d'fhéadfadh a bheith ina dtorthaí ó gach géag den `if`
an cineál céanna; i Liosta 3-2, tá torthaí an lámh `if` agus an `else` araon
lámh bhí slánuimhreacha `i32`. Má tá na cineálacha mímheaitseála, mar atá sa mhéid seo a leanas
mar shampla, gheobhaidh muid earráid:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-31-arms-must-return-same-type/src/main.rs}}
```

Nuair a dhéanaimid iarracht an cód seo a thiomsú, gheobhaidh muid earráid. Na lámha `if` agus `else`
tá cineálacha luacha neamh-chomhoiriúnacha acu, agus léiríonn Rust go díreach cá háit le
aimsigh an fhadhb sa chlár:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-31-arms-must-return-same-type/output.txt}}
```

Déanann an slonn sa bhloc `if` luacháil go slánuimhir, agus an slonn i
déanann an bloc `else` luacháil go teaghrán. Ní oibreoidh sé seo mar ní mór athróga
bhfuil cineál amháin, agus ní mór Rust a fhios ag an am le chéile cén cineál an
Is éard atá in athróg `number`, go cinntitheach. Ós eol an cineál `number` ligeann an
tiomsaitheoir a fhíorú go bhfuil an cineál bailí i ngach áit a úsáidimid `number`. Ní bheadh Rust
in ann é sin a dhéanamh dá gcinnfí an cineál `number` ag am rite amháin; an
bheadh tiomsaitheoir níos casta agus dhéanfadh sé níos lú ráthaíochtaí faoin gcód
dá mbeadh air súil a choinneáil ar ilchineálacha hipitéiseach d’athróg ar bith.

### Athrá le Lúbanna

Is minic a bhíonn sé úsáideach bloc cód a rith níos mó ná uair amháin. Don tasc seo,
Soláthraíonn Rust roinnt _loops_, a rithfidh tríd an gcód taobh istigh den lúb
comhlacht go dtí deireadh agus ansin tosú láithreach ar ais ag an tús. Chun triail
le lúba, déanaimis tionscadal nua darb ainm _loops_.

Tá trí chineál lúb ag Rust: `loop`, `while` agus `for`. Déanaimis iarracht gach ceann acu.

#### Cód á athrá le `loop`

Insíonn an eochairfhocal `loop` do Rust bloc cód a fhorghníomhú arís agus arís eile
go deo nó go dtí go n-insíonn tú go sainráite é stopadh.

Mar shampla, athraigh an comhad _src/main.rs_ i do eolaire _loops_ chun breathnú
mar seo:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-32-loop/src/main.rs}}
```

Agus an clár seo á rith againn, feicfidh muid `again!` á phriontáil arís agus arís eile
go dtí go stopfaimid an clár de láimh. Tacaíonn an chuid is mó de na críochfoirt leis an aicearra méarchláir
<kbd>ctrl</kbd> - <kbd>c</kbd> chun cur isteach ar ríomhchlár atá i bhfostú go leanúnach
lúb. Bain triail as:

<!-- athghiniúint de láimh
liostaí cd/ch03-common-programming-concepts/gan-liostú-32-lúb
rith lasta
CTRL-C
-->

```console
$ cargo run
   Compiling loops v0.1.0 (file:///projects/loops)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.08s
     Running `target/debug/loops`
again!
again!
again!
again!
^Cagain!
```

Léiríonn an tsiombail `^C` an áit ar bhrúigh tú <kbd>ctrl</kbd> - <kbd>c</kbd>. tu
b'fhéidir nó b'fhéidir nach bhfeicfidh sé an focal `again!` i gcló tar éis an `^C`, ag brath ar an áit
bhí an cód sa lúb nuair a fuair sé an comhartha idirbhriste.

Go fortunately, soláthraíonn Rust bealach freisin chun briseadh amach as lúb ag baint úsáide as cód. tu
Is féidir leis an eochairfhocal `break` a chur laistigh den lúb chun a insint don chlár cathain a stopfaidh sé
an lúb a fhorghníomhú. Thabhairt chun cuimhne go ndearna muid é seo sa chluiche buille faoi thuairim sa
[“Ag Scoir Tar éis Buille Cheart”][quitting-after-a-correct-guess]<!-- déan neamhaird
--> alt de Chaibidil 2 a fhágáil ar an gclár nuair a bhuaigh an t-úsáideoir an cluiche trí
an uimhir cheart a thomhas.

Bhaineamar úsáid freisin as `continue` sa chluiche buille faoi thuairim, rud a insíonn an clár i lúb
chun dul thar aon chód atá fágtha san atriall seo den lúb agus téigh go dtí an
an chéad atriall eile.

#### Luachanna Ag Filleadh ó Lúbanna

Ceann de na húsáidí a bhaineann le `loop` is ea triail eile a bhaint as oibríocht a bhfuil a fhios agat go bhféadfadh go dteipfeadh uirthi, mar sin
le seiceáil an bhfuil a phost críochnaithe ag snáithe. Seans go mbeidh ort pas a fháil freisin
toradh na hoibríochta sin amach as an lúb go dtí an chuid eile de do chód. A dhéanamh
seo, is féidir leat an luach a theastaíonn uait a chur ar ais tar éis an slonn `break` tú
úsáid chun an lúb a stopadh; cuirfear an luach sin ar ais as an lúb ionas gur féidir leat
bain úsáid as, mar a thaispeántar anseo:

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-33-return-value-from-loop/src/main.rs}}
```

Roimh an lúb, dearbhaímid athróg darb ainm `counter` agus cuirimid tús leis
`0`. Ansin dearbhaímid athróg darb ainm `result` chun an luach a tugadh ar ais uaidh a choinneáil
an lúb. Ar gach atriall den lúb, cuirimid `1` leis an athróg `counter`,
agus ansin seiceáil an bhfuil an `counter` cothrom le `10`. Nuair a bhíonn sé, úsáidimid an
eochairfhocal `break` leis an luach `counter * 2`. Tar éis an lúb, úsáidimid a
leathstad chun deireadh a chur leis an ráiteas a sannann an luach do `result`. Ar deireadh, táimid
priontáil an luach i `result`, atá sa chás seo `20`.

Is féidir leat `return` ón taobh istigh de lúb freisin. Cé nach n-imíonn `break` ach as an sruth
lúb, fágann `return` an fheidhm reatha i gcónaí.

#### Lipéid Lúb le Díréimniú Idir lúbanna Il

Má tá lúba laistigh de lúba agat, beidh feidhm ag `break` agus `continue` ar aghaidh chuig an gceann is faide istigh
lúb ar an bpointe sin. Is féidir leat _loop label_ a shonrú go roghnach ar lúb a
is féidir leat a úsáid ansin le `break` nó `continue` chun a shonrú go bhfuil na heochairfhocail
cuir i bhfeidhm ar an lúb lipéadaithe in ionad na lúb is faide istigh. Ní mór tús a chur le lipéid lúb
le ceanglófar amháin. Seo sampla le dhá lúb neadaithe:

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-32-5-loop-labels/src/main.rs}}
```

Tá an lipéad `'counting_up`' ar an lúb seachtrach, agus comhairfidh sé suas ó 0 go 2.
Comhaireamh an lúb istigh gan lipéad síos ó 10 go 9. An chéad `break` sin
Ní shonraítear lipéad scoirfidh sé den lúb inmheánach amháin. An `break
'counting_up;` scoirfidh ráiteas an lúb seachtrach. Priontálann an cód seo:

```console
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-32-5-loop-labels/output.txt}}
```

#### Lúb Choinníollach le `while`

Is minic go gcaithfidh clár riocht laistigh de lúb a mheas. Cé go bhfuil an
Tá an coinníoll `true`, ritheann an lúb. Nuair a scoireann an riocht de bheith `true`, beidh an
Glaonn an clár `break`, ag stopadh an lúb. Is féidir iompar a chur i bhfeidhm
mar seo ag baint úsáide as meascán de `loop`, `if`, `else`, agus `break`; d'fhéadfadh tú
bain triail as sin anois i gclár, más mian leat. Mar sin féin, tá an patrún seo chomh coitianta
go bhfuil tógáil teanga ionsuite ag Rust dó, ar a dtugtar lúb `while`. I
Ag liostú 3-3, bainimid úsáid as `while` chun an clár a lúbadh trí huaire, ag comhaireamh síos gach ceann acu
am, agus ansin, tar éis an lúb, a phriontáil teachtaireacht agus scoir.

<Listing number="3-3" file-name="src/main.rs" caption="Úsáid lúb `while` chun cód a rith agus coinníoll fós fíor">

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/listing-03-03/src/main.rs}}
```

</Listing>

Cuireann an tógáil seo deireadh le go leor neadaithe a bheadh riachtanach dá mbainfeá úsáid as
`loop`, `if`, `else`, agus `break`, agus tá sé níos soiléire. Cé go coinníoll
meastóireacht go `true`, ritheann an cód; ar shlí eile, scoireann sé an lúb.

#### Ag dul trí Bhailiúchán le `for`

Is féidir leat an tógáil `while` a úsáid freisin chun na heilimintí de a
bhailiú, mar shampla eagar. Mar shampla, priontaí an lúb i Liostú 3-4 an ceann
eilimint san eagar `a`.

<Listing number="3-4" file-name="src/main.rs" caption="Ag dul trí gach eilimint de bhailiúchán ag úsáid lúb `while`">

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/listing-03-04/src/main.rs}}
```

</Listing>

Anseo, déantar an cód a chomhaireamh trí na heilimintí san eagar. Tosaíonn sé ag innéacs
`0`, agus lúbann sé ansin go dtí go sroicheann sé an t-innéacs deiridh san eagar (is é sin,
nuair nach bhfuil `index < 5` a thuilleadh `true`). Má ritheann tú an cód seo, déanfar gach
eilimint san eagar:

```console
{{#include ../../listings/ch03-common-programming-concepts/listing-03-04/output.txt}}
```

Tá na cúig luach eagair ar fad le feiceáil sa teirminéal, mar a bhíothas ag súil leis. Cé go bhfuil `index`
Beidh teacht ar luach `5` ag pointe éigin, stopann an lúb forghníomhaitheach roimh iarraidh
an séú luach a fháil ón eagar.

Mar sin féin, tá an cur chuige seo seans maith go hearráidí; d’fhéadfaimis scaoll a chur ar an gclár dá mba rud é
tá an luach innéacs nó an riocht tástála mícheart. Mar shampla, má d'athraigh tú an
sainmhíniú ar an eagar `a` a bheith ceithre eilimint ach dearmad a thabhairt cothrom le dáta an
coinníoll go `while index < 4`, bheadh an cód scaoll. Tá sé mall freisin, mar gheall ar
cuireann an tiomsaitheoir cód ama rite leis chun an tseiceáil choinníollach a dhéanamh an bhfuil an
tá an t-innéacs laistigh de theorainneacha an eagar ar gach atriall tríd an lúb.

Mar rogha eile níos gonta, is féidir leat lúb `for` a úsáid agus cód éigin a fhorghníomhú
do gach earra i mbailiúchán. Breathnaíonn lúb `for` cosúil leis an gcód i Liostú 3-5.

<Listing number="3-5" file-name="src/main.rs" caption="Ag lúbadh trí gach eilimint de bhailiúchán ag baint úsáide as lúb `for`">

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/listing-03-05/src/main.rs}}
```

</Listing>

Agus an cód seo á rith againn, feicfidh muid an t-aschur céanna agus atá i Liostú 3-4. Tuilleadh
rud is tábhachtaí, táimid tar éis sábháilteacht an chóid a mhéadú anois agus deireadh a chur le
seans fabhtanna a d'fhéadfadh a bheith mar thoradh ar dhul níos faide ná deireadh na sraithe nó nach bhfuil
ag dul fada go leor agus roinnt míreanna ar iarraidh.

Ag baint úsáide as an lúb `for`, ní bheadh ort cuimhneamh ar aon chód eile a athrú más rud é
d'athraigh tú líon na luachanna san eagar, mar a dhéanfá leis an modh
a úsáidtear i Liosta 3-4.

Mar gheall ar shábháilteacht agus beacht na lúb `for` is iad an lúb is coitianta a úsáidtear
Tógáil i Rust. Fiú i gcásanna inar mian leat a rith roinnt cód a
líon áirithe uaireanta, mar atá sa sampla comhaireamh síos a d'úsáid lúb `while`
i Liosta 3-3, d'úsáidfeadh formhór na Rustaceans lúb `for`. An bealach chun é sin a dhéanamh
úsáid a bhaint as `Range`, a sholáthraíonn an leabharlann chaighdeánach, a ghineann
gach uimhir in ord ag tosú ó uimhir amháin agus ag críochnú roimh uimhir eile
uimhir.

Seo an chuma a bheadh ar an gcomhaireamh síos ag baint úsáide as lúb `for` agus modh eile
níor labhair muid faoi go fóill, `rev`, chun an raon a aisiompú:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-34-for-range/src/main.rs}}
```

Tá an cód seo beagán níos deise, nach ea?

## Achoimre

Rinne tú é! Ba chaibidil shuntasach í seo: d’fhoghlaim tú faoi athróga, scálach
agus cineálacha sonraí cumaisc, feidhmeanna, tuairimí, nathanna `if`, agus lúba! Chuig
cleachtadh leis na coincheapa a phléitear sa chaibidil seo, bain triail as cláir a thógáil chun
déan an méid seo a leanas:

- Tiontaigh teochtaí idir Fahrenheit agus Celsius.
- Gin an *n*ú uimhir Fibonacci.
- Priontáil na liricí don charúl Nollag “The Twelve Day of Christmas,”
 ag baint leasa as an athrá san amhrán.

Nuair a bheidh tú réidh le bogadh ar aghaidh, labhróimid faoi choincheap i Rust nach _ní dhéanann_
atá ann go coitianta i dteangacha ríomhchlárúcháin eile: úinéireacht.

[comparing-the-guess-to-the-secret-number]: ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number
[quitting-after-a-correct-guess]: ch02-00-guessing-game-tutorial.html#quitting-after-a-correct-guess