## Modúil a Shainmhíniú chun Scóip agus Príobháideacht a Rialú

Sa chuid seo, labhróimid faoi mhodúil agus faoi chodanna eile den chóras modúl,
is é sin _paths_, a ligeann duit míreanna a ainmniú; an eochairfhocal `use` a thugann a
cosán isteach sa raon feidhme; agus an eochairfhocal `pub` chun míreanna a dhéanamh poiblí. Déanfaimid plé freisin
an eochairfhocal `as`, pacáistí seachtracha, agus an t-oibreoir glob.

### Modúil Bileog Cheat

Sula n-aimsímid sonraí na modúl agus na gcosán, cuirimid scéal tapa ar fáil anseo
tagairt don chaoi a n-oibríonn modúil, cosáin, an eochairfhocal `use`, agus an eochairfhocal `pub`
sa tiomsaitheoir, agus conas a eagraíonn formhór na bhforbróirí a gcód. Beimid ag dul
trí shamplaí de gach ceann de na rialacha seo ar fud na caibidle seo, ach tá sé seo a
áit iontach chun tagairt a dhéanamh dó mar mheabhrúchán ar an gcaoi a n-oibríonn modúil.

- **Tosaigh ó fhréamh an gcliathbhosca**: Agus cliathbhosca á thiomsú, an tiomsaitheoir ar dtús
 Breathnaíonn i bhfréamhchomhad an chliathbhosca (de ghnáth _src/lib.rs_ le haghaidh cliathbhosca leabharlainne nó
 _src/main.rs_ le haghaidh cliathbhosca dénártha) le cód a thiomsú.
- **Modúil á ndearbhú**: Sa fhréamhchomhad cliathbhosca, is féidir leat modúil nua a dhearbhú;
 a rá go ndearbhaíonn tú modúl “gairdín” le `mod garden;`. Breathnóidh an tiomsaitheoir
 do chód an mhodúil sna háiteanna seo:
 - Inlíne, laistigh de lúibíní curly a thagann in ionad an leathstad tar éis `mod
 garden`
 - Sa chomhad _src/garden.rs_
 - Sa chomhad _src/garden/mod.rs_
- **Fomodúil á ndearbhú**: In aon chomhad seachas fréamh an chliabháin, is féidir leat
 fomhodúil a dhearbhú. Mar shampla, b'fhéidir go ndearbhóidh tú `mod vegetables;` i
 _src/gairdín.rs_. Lorgóidh an tiomsaitheoir cód an fhomhodúil laistigh de na
 eolaire ainmnithe don mhodúl tuismitheora sna háiteanna seo:
 - Inlíne, díreach ag leanúint `mod vegetables`, laistigh de lúibíní curly ina ionad
 den leathstad
 - Sa chomhad _src/garden/vegetables.rs_
 - Sa chomhad _src/garden/vegetables/mod.rs_
- **Cosáin chun cód a chur i modúil**: Nuair a bheidh modúl mar chuid de do chliabhán, is féidir leat
 déan tagairt don chód sa mhodúl sin ó áit ar bith eile sa chliabhán céanna sin, chomh fada
 mar a cheadaíonn na rialacha príobháideachta, ag baint úsáide as an cosán go dtí an cód. Mar shampla, an
 Gheofar cineál `Asparagus` sa mhodúl glasraí gairdín ag
  `crate::garden::vegetables::Asparagus`.
- **Príobháideach vs. poiblí**: Tá cód laistigh de mhodúl príobháideach óna thuismitheoir
 modúil de réir réamhshocraithe. Chun modúl a phoibliú, dearbhaigh é le `pub mod`
 in ionad `mod`. Chun míreanna laistigh de mhodúl poiblí a dhéanamh poiblí freisin, bain úsáid as
 `pub` roimh a ndearbhuithe.
- **An eochairfhocal `use`**: Laistigh de raon feidhme, cruthaíonn an eochairfhocal `use` aicearraí chuig
 míreanna chun athrá cosáin fhada a laghdú. In aon scóip is féidir tagairt a dhéanamh do
 `crate::garden::vegetables::Asparagus`, is féidir leat aicearra a chruthú le `use
 crate::garden::vegetables::Asparagus;`  agus as sin amach ní gá duit ach
 scríobh `Asparagus` chun úsáid a bhaint as an gcineál sin sa scóip.

Anseo, cruthaímid cliathbhosca dénártha darb ainm `backyard` a léiríonn na rialacha seo.
Tá na comhaid agus na heolairí seo i gcomhadlann an chliabháin, ar a dtugtar `backyard` freisin:

```text
backyard
├── Cargo.lock
├── Cargo.toml
└── src
    ├── garden
    │   └── vegetables.rs
    ├── garden.rs
    └── main.rs
```

Is é an comhad fréimhe cliathbhosca sa chás seo ná _src/main.rs_, agus tá:

<Listing file-name="src/main.rs">

```rust,noplayground,ignore
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/quick-reference-example/src/main.rs}}
```

</Listing>

Insíonn an líne `pub mod garden;` don tiomsaitheoir an cód a aimsíonn sé a chur san áireamh
_src/garden.rs_, mar atá:

<Listing file-name="src/garden.rs">

```rust,noplayground,ignore
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/quick-reference-example/src/garden.rs}}
```

</Listing>

Anseo, ciallaíonn `pub mod vegetables;` an cód i _src/garden/vegetables.rs_ is
san áireamh freisin. Is é an cód sin:

```rust,noplayground,ignore
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/quick-reference-example/src/garden/vegetables.rs}}
```

Anois déanaimis sonraí na rialacha seo a fháil agus iad a léiriú i ngníomh!

### Cód Gaolmhar a Ghrúpáil i Modúil

_Modules_ lig dúinn cód a eagrú laistigh de chliathbhosca ar mhaithe le hinléiteacht agus le hathúsáid éasca.
Ligeann modúil dúinn freisin _príobháideacht_ míreanna a rialú toisc go bhfuil cód laistigh de a
modúl príobháideach de réir réamhshocraithe. Is sonraí inmheánacha cur chun feidhme iad míreanna príobháideacha
nach bhfuil ar fáil le húsáid lasmuigh. Is féidir linn a roghnú modúil agus na míreanna a dhéanamh
laistigh díobh poiblí, a nochtar iad chun ligean do chód seachtrach a úsáid agus a bheith ag brath
orthu.

Mar shampla, scríobhaimis cliathbhosca leabharlainne a sholáthraíonn feidhmiúlacht a
bialann. Déanfaimid sínithe na bhfeidhmeanna a shainiú ach fágfaimid a gcorp
folamh chun díriú ar eagrú an chóid seachas ar an
bialann a chur i bhfeidhm.

I dtionscal na mbialann, déantar tagairt do roinnt codanna de bhialann
_aghaidh an tí_ agus cinn eile mar _chúl an tí_. Tá áit os comhair an tí
tá custaiméirí; cuimsíonn sé seo an áit ina suíonn an t-óstach do chustaiméirí, a thógann na freastalaithe
orduithe agus íocaíocht, agus déanann tábhairne deochanna. Ar chúl an tí tá an áit a bhfuil an
oibríonn príomhchócaire agus cócairí sa chistin, glantar miasniteoirí, agus déanann bainisteoirí
obair riaracháin.

Chun ár gcliathbhosca a struchtúrú ar an mbealach seo, is féidir linn a feidhmeanna a eagrú ina neadacha
modúil. Cruthaigh leabharlann nua darb ainm `restaurant` trí `cargo new
restaurant --lib`. Ansin cuir isteach an cód i Liostú 7-1 isteach _src/lib.rs_ go
roinnt modúil agus sínithe feidhm a shainiú; is é an cód seo tosaigh an tí
alt.

<Listing number="7-1" file-name="src/lib.rs" caption="A `front_of_house` module containing other modules that then contain functions">

```rust,noplayground
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-01/src/lib.rs}}
```

</Listing>

Sainmhínímid modúl leis an eochairfhocal `mod` agus ainm an mhodúil ina dhiaidh
(sa chás seo, `front_of_house`). Téann corp an mhodúil ansin taobh istigh de chatach
lúibíní. Taobh istigh modúil, is féidir linn a chur modúil eile, mar atá sa chás seo leis an
modúil `hosting` agus `serving`. Is féidir le modúil sainmhínithe a bheith acu ar mhodúil eile freisin
míreanna, mar struchtúir, éinim, tairisigh, tréithe, agus — mar atá i Liostú
7-1 - feidhmeanna.

Trí modúil a úsáid, is féidir linn sainmhínithe gaolmhara a ghrúpáil le chéile agus an fáth a ainmniú
tá gaol acu leis. Is féidir le ríomhchláraitheoirí a úsáideann an cód seo an cód a nascleanúint bunaithe ar an
grúpaí seachas a bheith ag léamh tríd na sainmhínithe go léir, é a dhéanamh níos éasca
chun na sainmhínithe a bhaineann leo a fháil. Ríomhchláraitheoirí ag cur feidhmiúlacht nua leis
Bheadh ​​a fhios ag an gcód seo cá háit a gcuirfí an cód chun an clár a choinneáil eagraithe.

Níos luaithe, luaigh muid go dtugtar cliathbhosca ar _src/main.rs_ agus _src/lib.rs_
fréamhacha. Is é an chúis atá lena n-ainm ná go bhfuil ábhar ceachtar den dá cheann seo
cruthaíonn comhaid modúl darb ainm `crate` ag bun struchtúr modúil an chliabháin,
ar a dtugtar an crann _module tree_.

Léiríonn Liostú 7-2 an crann modúl don struchtúr i Liostú 7-1.

<Listing number="7-2" caption="The module tree for the code in Listing 7-1">

```text
crate
 └── front_of_house
     ├── hosting
     │   ├── add_to_waitlist
     │   └── seat_at_table
     └── serving
         ├── take_order
         ├── serve_order
         └── take_payment
```

</Listing>

Léiríonn an crann seo conas a neadaíonn cuid de na modúil taobh istigh de mhodúil eile; mar shampla,
`hosting` a óstáil taobh istigh de `front_of_house`. Léiríonn an crann freisin go bhfuil roinnt modúil
is _siblíní_ iad, rud a chiallaíonn go bhfuil siad sainmhínithe sa mhodúl céanna; `hosting` agus
is siblíní iad `serving` laistigh de `front_of_house`. Más modúl A é
atá taobh istigh modúl B, deirimid go bhfuil modúl A an _child_ de mhodúl B agus
gurb é modúl B an _tuismitheoir_ de mhodúl A. Tabhair faoi deara go bhfuil an crann modúl ar fad
atá fréamhaithe faoin modúl intuigthe darb ainm `crate`.

Seans go gcuirfidh crann na modúl i gcuimhne duit crann eolaire an chórais comhad ar do
ríomhaire; is comparáid an-oiriúnach é seo! Cosúil le heolairí i gcóras comhaid,
úsáideann tú modúil chun do chód a eagrú. Agus díreach cosúil le comhaid i eolaire, táimid
gá bealach chun ár modúil a aimsiú.