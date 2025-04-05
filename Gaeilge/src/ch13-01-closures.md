<!-- Sean-cheannteideal. Ná bain amach nó seans go mbrisfidh naisc. -->

<a id="closures-anonymous-feidhmeanna-a-féidir-a ghabháil-a-timpeallacht"></a>

## Dúnadh: Feidhmeanna Gan Ainm a Gabhann A dTimpeallacht

Is feidhmeanna gan ainm iad dúnadh Rust is féidir leat a shábháil in athróg nó pas a fháil mar
argóintí le feidhmeanna eile. Is féidir leat an dúnadh a chruthú in aon áit amháin agus ansin
glaoch ar an dúnadh áit eile chun é a mheas i gcomhthéacs difriúil. Murab ionann
feidhmeanna, is féidir le dúnadh luachanna a ghabháil ón raon feidhme ina bhfuil siad sainithe.
Léireoimid conas a cheadaíonn na gnéithe dúnta seo athúsáid cód agus iompar
saincheaptha.

<!-- Sean-cheannteidil. Ná bain amach nó seans go mbrisfidh naisc. -->

<a id="creating-an-abstraction-of-behavior-with-closures"></a>
<a id="refactoring-using-functions"></a>
<a id="refactoring-with-closures-to-store-code"></a>

### Ag Gabháil na Timpeallachta le Dúnadh

Scrúdóimid ar dtús conas is féidir linn dúnadh a úsáid chun luachanna a fháil ó na
timpeallacht ina bhfuil siad sainithe le húsáid níos déanaí. Seo é an scéal: Gach cás
go minic, tugann ár gcomhlacht t-léine léine eisiach, eagrán teoranta do
duine ar ár liosta postála mar chur chun cinn. Is féidir le daoine ar an liosta postála
go roghnach a dath is fearr leat a chur ar a bpróifíl. Má tá an duine a roghnaíodh le haghaidh
tá a sraith dathanna is fearr leat ag léine saor in aisce, faigheann siad an léine dath sin. Má tá an
níl dath is fearr leat sonraithe ag an duine, faigheann siad cibé dath atá ar an gcuideachta
faoi ​​láthair tá an chuid is mó de.

Tá go leor bealaí ann chun é seo a chur i bhfeidhm. Mar shampla, bainfimid úsáid as
enum ar a dtugtar `ShirtColor` a bhfuil na leaganacha `Red` agus `Blue` (le teorainn
líon na dathanna atá ar fáil ar mhaithe le simplíocht). Déanaimid ionadaíocht ar son na cuideachta
fardal le struchtúr `Inventory` ar a bhfuil réimse darb ainm `shirts` sin
ina bhfuil `Vec<ShirtColor>` a sheasann do dhathanna na léine atá sa stoc faoi láthair.
Faigheann an modh `giveaway` a shainmhínítear ar `Inventory` an léine roghnach
rogha dath an bhuaiteoir léine in aisce, agus filleann dath an léine an
gheobhaidh duine. Taispeántar an socrú seo i Liostú 13-1:

<Listing number="13-1" file-name="src/main.rs" caption="Shirt company giveaway situation">

```rust,noplayground
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-01/src/main.rs}}
```

</Listing>

Tá dhá léine ghorma agus léine dhearg amháin fágtha sa `store` a shainmhínítear sa `main`
a dháileadh don chur chun cinn eagrán teoranta seo. Tugaimid an modh `giveaway`
d'úsáideoir a bhfuil rogha le haghaidh léine dearg agus úsáideoir gan aon rogha.

Arís, d’fhéadfaí an cód seo a chur i bhfeidhm ar go leor bealaí, agus anseo, chun díriú air
dúnadh, táimid tar éis cloí le coincheapa atá foghlamtha agat cheana féin seachas an corpán
an modh `giveaway` a úsáideann clabhsúr. Sa mhodh `giveaway`, faigheann muid an
rogha an úsáideora mar pharaiméadar den chineál `Option<ShirtColor>` agus glaoigh ar an
modh `unwrap_or_else` ar `user_preference`. Tá an modh [`unwrap_or_else` ar siúl
`Option<T>`][unwrap-or-else]<!-- neamhaird --> ag an ngnáthleabharlann.
Bíonn argóint amháin ann: dúnadh gan argóintí ar bith a thugann luach `T` ar ais
(an cineál céanna atá stóráilte sa leagan `Some` den `Option<T>`, sa chás seo
`ShirtColor`). Más é an `Option<T>` an ​​leagan `Some`, `unwrap_or_else`
aischuireann an luach ó laistigh den `Some`. Más é an `Option<T>` an ​​`None`
leagan eile, glaonn `unwrap_or_else` an dúnadh agus seolann sé an luach ar ais le
an dúnadh.

Sonraimid an slonn dúnta `|| self.most_stocked()` mar an argóint chun
`unwrap_or_else`. Seo dúnadh nach nglacann aon pharaiméadair féin (má tá an
Bhí paraiméadair ag dúnadh, bheadh ​​siad le feiceáil idir an dá bharra ingearach). Tá an
glaonn comhlacht an dúnta `self.most_stocked()`. Táimid ag sainmhíniú an dúnadh
anseo, agus déanfaidh feidhmiú `unwrap_or_else` an dúnadh a mheas
níos déanaí má tá an toradh ag teastáil.

Ag rith an chóid seo priontaí:

```console
{{#include ../../listings/ch13-functional-features/listing-13-01/output.txt}}
```

Gné shuimiúil amháin anseo ná gur éirigh linn dúnadh a ghlaonn
`self.most_stocked()` ar an gcás reatha `Inventory`. An leabharlann caighdeánach
níor ghá go mbeadh eolas ar bith againn ar na cineálacha `Inventory` nó `ShirtColor` atá againn
sainithe, nó an loighic ba mhaith linn a úsáid sa chás seo. Gabhann an dúnadh an
tagairt domhalartaithe don ásc `self` `Inventory` agus é a chur ar aghaidh leis an
cód a shonraimid leis an modh `unwrap_or_else`. Feidhmeanna, ar an láimh eile,
nach bhfuil in ann a dtimpeallacht a ghabháil ar an mbealach seo.

### Tátail agus Anótáil Cineál Dúnadh

Tá níos mó difríochtaí idir feidhmeanna agus dúnta. Ní dhéanann dúnta
de ghnáth éilíonn tú cineálacha na bparaiméadar nó an luach tuairisceáin a anótáil
mar a dhéanann feidhmeanna `fn`. Teastaíonn nótaí cineáil ar fheidhmeanna toisc go bhfuil an
tá cineálacha mar chuid de chomhéadan follasach a nochtar do d'úsáideoirí. Ag sainmhíniú seo
comhéadan docht tábhachtach chun a chinntiú go n-aontaíonn gach duine ar cad iad na cineálacha
de luachanna úsáideann feidhm agus tuairisceáin. Ar an láimh eile, ní úsáidtear dúnta
i gcomhéadan nochta mar seo: déantar iad a stóráil in athróga agus úsáidtear iad gan
iad a ainmniú agus iad a nochtadh d'úsáideoirí ár leabharlann.

Is iondúil go mbíonn dúnta gearr agus ní bhaineann siad ach le comhthéacs cúng
ná in aon chás treallach. Laistigh de na comhthéacsanna teoranta seo, is féidir leis an tiomsaitheoir
tátail na bparaiméadar agus an cineál tuairisceáin, cosúil leis an gcaoi a bhfuil sé in ann
chun tátal a bhaint as na cineálacha athróg is mó (tá cásanna annamh nuair a bhíonn an tiomsaitheoir
tá nótaí dúnta de dhíth freisin).

Mar is amhlaidh le hathróga, is féidir linn nótaí cineáil a chur leis más mian linn méadú a dhéanamh
soiléireacht agus soiléireacht ar chostas a bheith níos briathartha ná mar atá go docht
riachtanach. Is cosúil leis an sainmhíniú an sainmhíniú a thabhairt ar na cineálacha le haghaidh dúnadh
léirithe i Liostú 13-2. Sa sampla seo, táimid ag sainmhíniú dúnadh agus á stóráil
in athróg seachas an dúnadh a shainiú sa spota tugaimid thairis é mar
argóint mar a rinneamar i Liosta 13-1.

<Listing number="13-2" file-name="src/main.rs" caption="Adding optional type annotations of the parameter and return value types in the closure">

```rust
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-02/src/main.rs:here}}
```

</Listing>

Agus nótaí cineáil curtha leis, tá cuma níos cosúla ar chomhréir na ndúntaí leis an
comhréir feidhmeanna. Anseo sainímid feidhm a chuireann 1 lena pharaiméadar agus
clabhsúr a bhfuil an t-iompar céanna air, chun comparáid a dhéanamh. Chuireamar roinnt spásanna leis
chun na codanna ábhartha a líneáil. Léiríonn sé seo an chomhréir dúnta comhchosúil
chun comhréir a fheidhmiú ach amháin maidir le húsáid píopaí agus an méid comhréire atá
roghnach:

```rust,ignore
fn  add_one_v1   (x: u32) -> u32 { x + 1 }
let add_one_v2 = |x: u32| -> u32 { x + 1 };
let add_one_v3 = |x|             { x + 1 };
let add_one_v4 = |x|               x + 1  ;
```

Taispeánann an chéad líne sainmhíniú ar fheidhm, agus taispeánann an dara líne sainmhíniú iomlán
sainmhíniú dúnta anótáilte. Sa tríú líne, bainimid na nótaí cineáil
ón sainmhíniú dúnta. Sa cheathrú líne, bainimid na lúibíní, a bhfuil
atá roghnach toisc nach bhfuil ach léiriú amháin ag an gcomhlacht dúnta. Is iad seo go léir
sainmhínithe bailí a thabharfaidh an t-iompar céanna nuair a ghlaotar orthu. Tá an
Éilíonn línte `add_one_v3` agus `cuir_one_v4` go ndéanfaí na dúnta a mheas
in ann a thiomsú mar go mbeidh na cineálacha a thuiscint óna n-úsáid. Tá sé seo
cosúil le `let v = Vec::new();` a dteastaíonn ceachtar den chineál nótaí nó luachanna de
cineál éigin le cur isteach sa `Vec` le go mbeidh Rust in ann an cineál a thuiscint.

Maidir le sainmhínithe dúnta, bainfidh an tiomsaitheoir le tátal a bhaint as cineál coincréite amháin do gach ceann díobh
a bparaiméadar agus a luach aischuir. Mar shampla, taispeánann Liostú 13-3
an sainmhíniú ar dhúnadh gairid nach dtugann ach an luach a fhaigheann sé ar ais mar a
paraiméadar. Níl an dúnadh seo an-úsáideach ach amháin chun críocha seo
shampla. Tabhair faoi deara nach bhfuil aon chineál nótaí curtha againn leis an sainmhíniú.
Toisc nach bhfuil aon nótaí cineáil ann, is féidir linn an dúnadh a ghlaoch le haon chineál,
rud atá déanta againn anseo le `String` an chéad uair. Má dhéanaimid iarracht ansin glaoch
`example_closure` le slánuimhir, gheobhaidh muid earráid.

<Listing number="13-3" file-name="src/main.rs" caption="Attempting to call a closure whose types are inferred with two different types">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-03/src/main.rs:here}}
```

</Listing>

Tugann an tiomsaitheoir an earráid seo dúinn:

```console
{{#include ../../listings/ch13-functional-features/listing-13-03/output.txt}}
```

An chéad uair a thugaimid `example_closure` air leis an luach `String`, an tiomsaitheoir
tugtar le tuiscint gur `String` an cineál `x` agus an cineál fillte den dúnadh. Iad siúd
cuirtear cineálacha faoi ghlas ansin sa dúnadh i `example_closure`, agus faigheann muid cineál
earráid nuair a dhéanaimid iarracht cineál eile a úsáid leis an dúnadh céanna.

### Tagairtí a Ghabháil nó Úinéireacht a Bhogadh

Is féidir le dúnta luachanna a ghabháil óna dtimpeallacht ar thrí bhealach, rud a
léarscáil go díreach chuig na trí bhealach is féidir le feidhm a ghlacadh paraiméadar: iasacht a fháil
go do-athraithe, iasachtaí a fháil go comhuaineach, agus úinéireacht a ghlacadh. Cinnfidh an dúnadh
cé acu seo atá le húsáid bunaithe ar cad a dhéanann corp na feidhme leis an
luachanna gafa.

I Liostú 13-4, sainmhínímid dúnadh a ghabhann tagairt do-athlasach do
an veicteoir darb ainm `list` toisc nach bhfuil de dhíth air ach tagairt do-athlasta le priontáil
an luach:

<Listing number="13-4" file-name="src/main.rs" caption="Defining and calling a closure that captures an immutable reference">

```rust
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-04/src/main.rs}}
```

</Listing>

Léiríonn an sampla seo freisin gur féidir le hathróg ceangal le sainmhíniú dúnta,.
agus is féidir linn an dúnadh a ghlaoch níos déanaí tríd an ainm athróg agus lúibíní a úsáid mar
dá mba ainm feidhme é an t-ainm athróg.

Toisc gur féidir linn go leor tagairtí do-athlasta a bheith againn do `list` ag an am céanna,
tá `list` fós inrochtana ón gcód roimh an sainmhíniú dúnta, tar éis
an sainmhíniú ar dhúnadh ach sula dtugtar an dúnadh, agus tar éis an dúnadh
ar a dtugtar. Tiomsaíonn, ritheann agus priontaí an cód seo:

```console
{{#include ../../listings/ch13-functional-features/listing-13-04/output.txt}}
```

Ansin, i Liostú 13-5, athraíonn muid an corp dúnta ionas go gcuireann sé eilimint leis
an veicteoir `list`. Gabhann an dúnadh tagairt mutable anois:

<Listing number="13-5" file-name="src/main.rs" caption="Defining and calling a closure that captures a mutable reference">

```rust
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-05/src/main.rs}}
```

</Listing>

Tiomsaíonn, ritheann agus priontaí an cód seo:

```console
{{#include ../../listings/ch13-functional-features/listing-13-05/output.txt}}
```

Tabhair faoi deara nach bhfuil `println!` a thuilleadh idir an sainmhíniú agus an glao ar
an dúnadh `borrows_mutably`: nuair a shainmhínítear `borrows_mutably`, gabhann sé
tagairt mutable do `list`. Ní úsáidimid an dúnadh arís tar éis an dúnta
ar a dtugtar, mar sin a thagann deireadh leis an iasacht mutable. Idir an sainmhíniú dúnta agus an
glao dúnta, ní cheadaítear iasacht neamh-inaistrithe le priontáil toisc nach bhfuil ceann eile
ceadaítear iasachtaí nuair a bhíonn iasacht shochorraithe ann. Bain triail as `println!` a chur leis
ann a fheiceáil cén teachtaireacht earráide a fhaigheann tú!

Más mian leat iallach a chur ar an dúnadh úinéireacht a ghlacadh ar na luachanna a úsáideann sé sa
timpeallacht cé nach gá go docht le corp an dúnta
úinéireacht, is féidir leat an eochairfhocal `move` a úsáid roimh liosta na bparaiméadar.

Tá an teicníocht seo úsáideach den chuid is mó agus dúnadh á rith ag snáithe nua le bogadh
na sonraí ionas go mbeidh sé faoi úinéireacht an snáithe nua. Pléifimid snáitheanna agus cén fáth
ba mhaith leat iad a úsáid go mion i gCaibidil 16 agus muid ag caint faoi
concurrency, ach faoi láthair, déanaimis iniúchadh gairid ar sceite snáithe nua ag baint úsáide as a
dúnadh a dteastaíonn an eochairfhocal `move`. Léiríonn Liostú 13-6 Liosta 13-4 modhnaithe
chun an veicteoir a phriontáil i snáithe nua seachas sa phríomhshnáithe:

<Listing number="13-6" file-name="src/main.rs" caption="Using `move` to force the closure for the thread to take ownership of `list`">

```rust
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-06/src/main.rs}}
```

</Listing>

Scaipimid snáithe nua, rud a fhágann gur dúnadh an snáithe a rith mar argóint. Tá an
comhlacht dúnadh priontaí amach an liosta. I Liosta 13-4, níor gabhadh ach an dúnadh
`list` ag baint úsáide as tagairt neamh-inmhalartaithe toisc gurb é sin an méid rochtana is lú
chun `list` a theastaíonn chun é a phriontáil. Sa sampla seo, cé go bhfuil an comhlacht dúnta
fós ag teastáil ach tagairt do- immutable, ní mór dúinn a shonrú gur chóir `list`
a bhogadh isteach sa dúnadh tríd an eochairfhocal `move` a chur ag tús an
sainmhíniú dúnta. Seans go gcríochnódh an snáithe nua roimh an gcuid eile den phríomhshnáithe
bailchríocha an tsnáithe, nó b'fhéidir go gcríochnódh an príomhshnáithe ar dtús. Má tá an snáithe is mó
choinnigh úinéireacht ar `list` ach tháinig deireadh leis sular tháinig agus thit an snáithe nua
`list`, bheadh ​​an tagairt do-athlasta sa snáithe neamhbhailí. Dá bhrí sin, an
Éilíonn tiomsaitheoir go n-aistreofar `list` isteach sa dúnadh a thugtar don snáithe nua
mar sin beidh an tagairt bailí. Bain triail as an eochairfhocal `move` a bhaint nó úsáid a bhaint as `list`
sa snáithe is mó tar éis an dúnadh a shainmhíniú a fheiceáil cad earráidí tiomsaitheoir tú
faigh!

<!-- Old headings. Do not remove or links may break. -->

<a id="storing-closures-using-generic-parameters-and-the-fn-traits"></a>
<a id="limitations-of-the-cacher-implementation"></a>
<a id="moving-captured-values-out-of-the-closure-and-the-fn-traits"></a>

### Luachanna Gafa á Bogadh As Dúnadh agus na Tréithe `Fn`

Nuair a bheidh tagairt faighte ag dúnadh nó úinéireacht luach a ghabháil ó
an timpeallacht ina sainmhínítear an dúnadh (ar an gcaoi sin bíonn tionchar aige ar cad, más rud ar bith,
ar athraíodh a ionad _into_ an dúnadh), sainmhíníonn an cód i gcorp an dúnta cad
a tharlaíonn do na tagairtí nó na luachanna nuair a dhéantar an dúnadh a mheas níos déanaí (mar sin
ag cur isteach ar an rud, más rud ar bith, a bhogtar _amach as_ an dúnadh). Is féidir le comhlacht dúnadh
déan aon cheann díobh seo a leanas: bog luach gafa amach as an dúnadh, mutate an
luach a gabhadh, ná bogadh ná mutate an luach, nó a ghabháil aon rud ó na
timpeallacht ar dtús.

Bíonn tionchar ag an mbealach a shealbhaíonn agus a láimhseálann dúnadh luachanna ón gcomhshaol
a bhfuil tréithe na n-uirlisí dúnta, agus na tréithe a bhaineann le feidhmeanna agus struchtúir
is féidir a shonrú cad iad na cineálacha dúnta is féidir leo a úsáid. Dúnfar go huathoibríoch
cuir ceann amháin, dhá cheann, nó trí cinn de na tréithe `Fn` seo i bhfeidhm ar bhealach suimitheach,
ag brath ar an gcaoi a láimhseálann corp an dúnaidh na luachanna:

1. Baineann `FnOnce` le dúnadh ar féidir glaoch orthu uair amháin. Cuireann gach dúnadh i bhfeidhm
 an trait seo ar a laghad, mar is féidir glaoch ar gach dúnadh. Dúnadh sin
 ní chuirfidh bogann luachanna a gabhadh amach as a chorp ach `FnOnce` agus ní chuirfidh sé aon cheann i bhfeidhm
 de na tréithe `Fn` eile, mar ní féidir é a ghlaoch ach uair amháin.
2. Baineann `FnMut` le dúnadh nach n-aistríonn luachanna a gabhadh amach as a gcuid
 comhlacht, ach d'fhéadfadh sé sin na luachanna a gabhadh a athrú. Is féidir leis na dúnta seo a bheith
 ar a dtugtar níos mó ná uair amháin.
3. Baineann `Fn` le dúnadh nach n-aistríonn luachanna gafa amach as a gcorp
 agus nach mutálann luachanna a gabhadh, chomh maith le dúnadh a ghabháil
 rud ar bith óna dtimpeallacht. Is féidir glaoch ar na dúnta seo níos mó ná uair amháin
 gan mutating a dtimpeallacht, rud atá tábhachtach i gcásanna mar
 dúnadh a ghlaoch go minic i gcomhthráth.

Breathnaímid ar an sainmhíniú ar an modh `unwrap_or_else` ar `Option<T>` go
d’úsáideamar i Liostú 13-1:

```rust,ignore
impl<T> Option<T> {
    pub fn unwrap_or_else<F>(self, f: F) -> T
    where
        F: FnOnce() -> T
    {
        match self {
            Some(x) => x,
            None => f(),
        }
    }
}
```

Thabhairt chun cuimhne gurb é `T` an cineál cineálach a léiríonn an cineál luacha sa
Leagan `Some` de `Option`. Is é an cineál sin `T` freisin an cineál tuairisceáin den
feidhm `unwrap_or_else`: cód a ghlaonn `unwrap_or_else` ar an
Gheobhaidh `Option<String>`, mar shampla, `String`.

Ansin, tabhair faoi deara go bhfuil an cineál cineálach breise ag an bhfeidhm `unwrap_or_else`
paraiméadar `F`. Is é an cineál `F` ná cineál an pharaiméadar darb ainm `f`, mar atá
an dúnadh a chuirimid ar fáil nuair a ghlaonn tú ar `unwrap_or_else`.

Is í an tréith a shonraítear ar an gcineál cineálach `F` ná `FnOnce() -> T`, a
ciallaíonn sé go gcaithfidh `F` a bheith in ann glaoch a chur air uair amháin, gan argóintí a ghlacadh, agus `T` a thabhairt ar ais.
Trí úsáid a bhaint as `FnOnce` sa tréith faoi cheangal cuirtear an srian sin in iúl
Ní dhéanfaidh `unwrap_or_else` ach `f` a ghlaoch ar uair amháin ar a mhéad. I gcorp na
`unwrap_or_else`, feicimid más `Some` an `Option`, ní bheidh `f`
ar a dtugtar. Murab é an `Option` ná `None`, tabharfar `f` uair amháin. Mar gheall ar go léir
feidhmíonn dúnta `FnOnce`, glacann `unwrap_or_else` leis na trí chineál
dúnta agus tá sé chomh solúbtha agus is féidir.

> Nóta: Más rud é nach gá luach a ghabháil ón méid is mian linn a dhéanamh
> timpeallacht, is féidir linn ainm feidhm a úsáid seachas dúnadh. Le haghaidh
> mar shampla, d'fhéadfaimis `unwrap_or_else(Vec::nua)` a ghlaoch ar luach `Option<Vec<T>>`
> chun veicteoir nua, folamh a fháil más é an luach `None`. An tiomsaitheoir go huathoibríoch
> cuireann sé i bhfeidhm cibé ceann de na tréithe `Fn` a bhaineann le feidhm
> sainmhíniú.

Anois breathnaímid ar an modh caighdeánach leabharlainne `sort_by_key` atá sainmhínithe ar slisní,
a fheiceáil conas atá sé difriúil ó `unwrap_or_else` agus cén fáth a n-úsáideann `sort_by_key`
`FnMut` in ionad `FnOnce` don trait faoi cheangal. Faigheann an dúnadh argóint amháin
i bhfoirm tagartha don mhír reatha sa tslis atá á bhreithniú,.
agus cuireann sé ar ais luach cineál `K` is féidir a ordú. Tá an fheidhm seo úsáideach
nuair is mian leat slice a shórtáil de réir tréith ar leith de gach mír. I
Ag liostú 13-7, tá liosta cásanna `Rectangle` againn agus úsáidimid `sort_by_key`
chun iad a ordú de réir a tréith `width` ó íseal go hard:

<Listing number="13-7" file-name="src/main.rs" caption="Using `sort_by_key` to order rectangles by width">

```rust
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-07/src/main.rs}}
```

</Listing>

Priontálann an cód seo:

```console
{{#include ../../listings/ch13-functional-features/listing-13-07/output.txt}}
```

Is é an chúis a shainmhínítear `sort_by_key` chun dúnadh `FnMut` a ghlacadh ná go nglaonn sé
an dúnadh iolraí: uair amháin do gach mír sa slice. Ní dhéanann an dúnadh `|r| r.width` aon rud a ghabháil, a mutadh ná a bhogadh amach óna thimpeallacht, mar sin
comhlíonann sé na ceanglais a bhaineann le tréithe.

I gcodarsnacht leis sin, léiríonn Liosta 13-8 sampla de dhúnadh a fheidhmíonn díreach
an trait `FnOnce`, toisc go mbogann sé luach amach as an timpeallacht. Tá an
ní ligfidh an tiomsaitheoir dúinn an dúnadh seo a úsáid le `sort_by_key`:

<Listing number="13-8" file-name="src/main.rs" caption="Attempting to use an `FnOnce` closure with `sort_by_key`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-08/src/main.rs}}
```

</Listing>

Is bealach suarach, convoluted é seo (nach n-oibríonn) chun iarracht a dhéanamh na
líon uaireanta a ghlaonn `sort_by_key` ar an dúnadh agus `list` á shórtáil. An cód seo
déanann sé iarracht an comhaireamh seo a dhéanamh trí `value`—a `String` a bhrú ó na dúnta
timpeallacht - isteach sa veicteoir `sort_operations`. Gabhann an dúnadh `value`
ansin bogtar `value` amach as an dúnadh trí úinéireacht `value` a aistriú go dtí
an veicteoir `sort_operations`. Is féidir an dúnadh seo a ghairm uair amháin; ag iarraidh glaoch
ní n-oibreodh sé an dara huair mar ní bheadh ​​`value` sa
timpeallacht a bhrú isteach i `sort_operations` arís! Dá bhrí sin, an dúnadh seo
ní chuireann ach `FnOnce` i bhfeidhm. Nuair a dhéanaimid iarracht an cód seo a thiomsú, faigheann muid an earráid seo
nach féidir an `value` sin a bhogadh amach as an dúnadh mar ní mór an dúnadh
cuir `FnMut` i bhfeidhm:

```console
{{#include ../../listings/ch13-functional-features/listing-13-08/output.txt}}
```

Díríonn an earráid ar an líne sa chorp dúnta a bhogann `value` amach as an
timpeallacht. Chun é seo a shocrú, ní mór dúinn an comhlacht dúnta a athrú ionas nach ndéanann sé
luachanna a bhogadh amach as an timpeallacht. Chun an líon uaireanta an dúnadh a chomhaireamh
ar a dtugtar, cuntar a choinneáil sa timpeallacht agus a luach a mhéadú i
Is bealach níos simplí é an comhlacht dúnta chun é sin a ríomh. An dúnadh
i Liostú 13-9 oibríonn sé le `sort_by_key` toisc nach bhfuil ann ach mutable a ghabháil
tagairt don chuntar `num_sort_operations` agus mar sin is féidir níos mó a ghlaoch air
ná uair amháin:

<Listing number="13-9" file-name="src/main.rs" caption="Using an `FnMut` closure with `sort_by_key` is allowed">

```rust
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-09/src/main.rs}}
```

</Listing>

Tá na tréithe `Fn` tábhachtach nuair a bhíonn feidhmeanna nó cineálacha sin á sainiú nó á n-úsáid
úsáid a bhaint as dúnta. Sa chéad chuid eile, déanfaimid plé ar atriallta. go leor
Glacann modhanna iterator argóintí dúnta, mar sin coinnigh na sonraí dúnta seo san áireamh
agus muid ag leanúint ar aghaidh!

[unwrap-or-else]: ../std/option/enum.Option.html#method.unwrap_or_else