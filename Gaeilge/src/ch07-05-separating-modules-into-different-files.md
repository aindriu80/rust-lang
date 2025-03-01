## Modúil a Scaradh ina gComhaid Éagsúla

Go dtí seo, shainmhínigh na samplaí go léir sa chaibidil seo modúil iolracha in aon chomhad amháin.
Nuair a thagann méadú mór ar mhodúil, b'fhéidir gur mhaith leat a sainmhínithe a aistriú go dtí ceann eile
comhad chun an cód a dhéanamh níos éasca le nascleanúint a dhéanamh.

Mar shampla, cuirimis tús leis an gcód i Liostú 7-17 a raibh iolraí ann
modúil bialann. Bainfimid modúil isteach i gcomhaid in ionad na modúil go léir a bheith againn
modúil atá sainithe i bhfréamhchomhad an chliabháin. Sa chás seo, tá an comhad fréimhe gcliathbhosca
_src/lib.rs_, ach oibríonn an nós imeachta seo freisin le cliathbhoscaí dénártha a bhfuil a fhréamh gcliathbhosca
Tá an comhad _src/main.rs_.

Ar dtús bainfimid an modúl `front_of_house` as a chomhad féin. Bain an
cód taobh istigh de na lúibíní chatach don mhodúl `front_of_house`, ag fágáil amháin
an `mod front_of_house;` dearbhú, ionas go mbeidh an cód ag _src/lib.rs_
léirithe i Liosta 7-21. Tabhair faoi deara nach dtiomsóidh sé seo go dtí go gcruthóimid an
_src/front_of_house.rs_ comhad i Liostú 7-22.

<Listing number="7-21" file-name="src/lib.rs" caption="Declaring the `front_of_house` module whose body will be in *src/front_of_house.rs*">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-21-and-22/src/lib.rs}}
```

</Listing>

Ansin, cuir an cód a bhí sna lúibíní cuartha isteach i gcomhad nua darb ainm
_src/front_of_house.rs_, mar a thaispeántar i Liostú 7-22. Tá a fhios ag an tiomsaitheoir breathnú
sa chomhad seo toisc gur tháinig sé trasna ar dhearbhú an mhodúil sa fhréamh gcliathbhosca
leis an ainm `front_of_house`.

<Listing number="7-22" file-name="src/front_of_house.rs" caption="Definitions inside the `front_of_house` module in *src/front_of_house.rs*">

```rust,ignore
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-21-and-22/src/front_of_house.rs}}
```

</Listing>

Tabhair faoi deara nach gá duit ach comhad a luchtú ag baint úsáide as dearbhú `mod` _aon uair_ i do
crann modúl. Nuair a bhíonn a fhios ag an tiomsaitheoir tá an comhad mar chuid den tionscadal (agus tá a fhios aige
áit sa chrann modúl ina bhfuil cónaí ar an gcód mar gheall ar an áit ar chuir tú an `mod`
ráiteas), ba cheart go dtagraíonn comhaid eile i do thionscadal do chód an chomhaid luchtaithe
ag baint úsáide as cosán go dtí an áit a dearbhaíodh é, mar atá clúdaithe sa [“Cosáin le haghaidh Tagartha
chuig Mír i gCrann an Mhodúil”][paths]<!-- déan neamhaird de -->. I bhfocail eile,
Is _not_ é `mod` ná oibríocht "cuir san áireamh" a d'fhéadfadh a bheith feicthe agat i gceann eile
teangacha ríomhchlárúcháin.

Ansin, bainfimid an modúl `hosting` as a chomhad féin. Tá an próiseas beagán
difriúil toisc go bhfuil `hosting` ina mhodúl linbh de `front_of_house`, ní de na
modúl fréimhe. Cuirfimid an comhad le haghaidh `hosting` in eolaire nua a bheidh
ainmnithe as a sinsir sa chrann modúl, sa chás seo _src/front_of_house_.

Chun tús a chur le `hosting` a bhogadh, athraíonn muid _src/front_of_house.rs_ go bhfuil iontu amháin
dearbhú an mhodúil `hosting`:

<Listing file-name="src/front_of_house.rs">

```rust,ignore
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/no-listing-02-extracting-hosting/src/front_of_house.rs}}
```

</Listing>

Ansin cruthaímid eolaire _src/front_of_house_ agus comhad _hosting.rs_ chun
go bhfuil na sainmhínithe a rinneadh sa mhodúl `hosting`:

<Listing file-name="src/front_of_house/hosting.rs">

```rust,ignore
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/no-listing-02-extracting-hosting/src/front_of_house/hosting.rs}}
```

</Listing>

Dá gcuirfimid _hosting.rs_ san eolaire _src_ ina ionad sin, dhéanfadh an tiomsaitheoir
bí ag súil go mbeidh an cód _hosting.rs_ i modúl `hosting` dearbhaithe sa chliathbhosca
fréamh, agus nach ndearbhaítear é mar leanbh den mhodúl `tosaigh_an tí. Tá an
rialacha tiomsaitheora maidir leis na comhaid le seiceáil cé na modúil a chiallaíonn cód an
meaitseálann eolairí agus comhaid níos dlúithe le crann an mhodúil.

> ### Conairí Comhad Malartacha
>
> Go dtí seo tá na conairí comhaid is gnásúla a úsáideann an tiomsaitheoir Rust clúdaithe againn,
> ach tacaíonn Rust le cosán comhaid stíl níos sine freisin. Le haghaidh modúl ainmnithe
> `front_of_house` dearbhaithe i bhfréamh an gcliathbhosca, lorgóidh an tiomsaitheoir an
> cód an mhodúil i:
>
> - _src/front_of_house.rs_ (cad a chlúdaigh muid)
> - _src/front_of_house/mod.rs_ (stíl níos sine, cosán tacaithe fós)
>
> I gcás modúl darb ainm `hosting` is fomhodúl de `front_of_house` é, an
> lorgóidh tiomsaitheoir cód an mhodúil i:
>
> - _src/front_of_house/hosting.rs_ (cad a chlúdaigh muid)
> - _src/front_of_house/hosting/mod.rs_ (stíl níos sine, cosán tacaithe fós)
>
> Má úsáideann tú an dá stíl don mhodúl céanna, gheobhaidh tú earráid tiomsaithe.
> Is éard atá i gceist le meascán den dá stíl a úsáid le haghaidh modúil éagsúla sa tionscadal céanna
> ceadaithe, ach d'fhéadfadh sé a bheith mearbhall do dhaoine atá ag seoladh do thionscadal.
>
> Is é an príomhbhuntáiste a bhaineann leis an stíl a úsáideann comhaid darb ainm _mod.rs_ ná go bhfuil do
> Is féidir go leor comhad darb ainm _mod.rs_ a bheith ag an tionscadal, rud a chuireann mearbhall ort
> nuair a bhíonn siad oscailte agat i d'eagarthóir ag an am céanna.

Táimid tar éis cód gach modúl a aistriú go comhad ar leith, agus tá crann an mhodúil fós ann
mar an gcéanna. Oibreoidh an fheidhm glaonna i `eat_at_restaurant` gan aon cheann
modhnú, cé go bhfuil na sainmhínithe ina gcónaí i gcomhaid éagsúla. seo
ligeann teicníocht duit modúil a aistriú go comhaid nua de réir mar a fhásann siad i méid.

Tabhair faoi deara go bhfuil an `pub use crate::front_of_house :: hosting` ráiteas i
Níor athraigh _src/lib.rs_ freisin, agus ní bhíonn tionchar ar bith ag `use` ar na comhaid
a thiomsaítear mar chuid den chliabhán. Dearbhaíonn an eochairfhocal `mod` modúil, agus Rust
Breathnaíonn i gcomhad leis an ainm céanna leis an modúl don chód a théann isteach
an modúl sin.

## Achoimre

Ligeann Rust duit pacáiste a roinnt ina cliathbhoscaí iolracha agus cliathbhoscaí ina modúil
is féidir leat tagairt a dhéanamh d'earraí atá sainithe i modúl amháin ó mhodúl eile. Is féidir leat a dhéanamh
seo trí chosáin iomlána nó choibhneasta a shonrú. Is féidir na cosáin seo a thabhairt isteach
raon feidhme le ráiteas `use` ionas gur féidir leat cosán níos giorra a úsáid le haghaidh úsáidí iolracha
an mhír sa raon feidhme sin. Tá cód an mhodúil príobháideach de réir réamhshocraithe, ach is féidir leat a dhéanamh
sainmhínithe go poiblí tríd an eochairfhocal `pub` a chur leis.

Sa chéad chaibidil eile, féachfaimid ar roinnt struchtúr sonraí bailiúcháin sa
leabharlann caighdeánach ar féidir leat a úsáid i do chód eagraithe go néata.

[paths]: ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html