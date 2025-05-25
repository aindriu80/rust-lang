## Na hÁiteanna Uile ar Féidir Patrúin a Úsáid

Tagann patrúin aníos i roinnt áiteanna i Rust, agus tá tú ag baint úsáide astu go minic
gan a bheith ar an eolas faoi! Pléann an chuid seo na háiteanna uile ina bhfuil patrúin
bailí.

### Lámha `match`

Mar a pléadh i gCaibidil 6, úsáidimid patrúin in airm nathanna `match`.
Go foirmiúil, sainmhínítear nathanna `match` mar an eochairfhocal `match`, luach le
meaitseáil air, agus lámh mheaitseála amháin nó níos mó ina bhfuil patrún agus
léiriú le rith má chomhlíonann an luach patrún na láimhe sin, mar seo:

```text
match VALUE {
    PATTERN => EXPRESSION,
    PATTERN => EXPRESSION,
    PATTERN => EXPRESSION,
}
```

Mar shampla, seo an abairt `match` ó Liosta 6-5 a mheaitseálann ar luach `Option<i32>` san athróg `x`:

```rust,ignore
match x {
    None => None,
    Some(i) => Some(i + 1),
}
```

Is iad na patrúin sa léiriú `match` seo ná `None` agus `Some(i)` ar thaobh na
clé de gach saighead.

Riachtanas amháin do léirithe `match` ná go gcaithfidh siad a bheith _uileghabhálach_ sa
mhéid is go gcaithfear gach féidearthacht don luach sa léiriú `match` a chur san áireamh. Bealach amháin chun a chinntiú go bhfuil gach féidearthacht clúdaithe agat ná patrún
gabhálach a bheith agat don lámh dheireanach: mar shampla, ní féidir le hainm athróg a mheaitseálann aon
luach teip riamh agus dá bhrí sin clúdaíonn sé gach cás atá fágtha.

Mheaitseálfaidh an patrún áirithe `_` aon rud, ach ní cheanglaíonn sé le
athróg riamh, mar sin is minic a úsáidtear é sa lámh mheaitseála dheireanach. Is féidir leis an patrún `_` a bheith
úsáideach nuair is mian leat neamhaird a dhéanamh d'aon luach nach bhfuil sonraithe, mar shampla. Clúdóimid an patrún `_` níos mine sa chuid [“Neamhaird a thabhairt ar Luachanna i
Patrún”][neamhaird-luachanna-i-patrún]<!-- neamhaird --> níos déanaí sa
chaibidil seo.

### Léirithe Coinníollacha `if let`

I gCaibidil 6 phléamar conas léirithe `if let` a úsáid go príomha mar bhealach níos giorra
chun coibhéis `match` a scríobh nach n-oireann ach do chás amháin.
De rogha air sin, is féidir le `if let` `else` comhfhreagrach a bheith aige ina bhfuil cód le rith mura
n-oireann an patrún sa `if let`.

Léiríonn Liostáil 19-1 gur féidir léirithe `if let`, `else
if`, agus `else if let` a mheascadh agus a mheaitseáil freisin. Tugann sé sin níos mó solúbthachta dúinn ná
léiriú `match` ina bhféadfaimid luach amháin a chur in iúl le comparáid a dhéanamh leis na
patrúin. Chomh maith leis sin, ní éilíonn Rust go mbeadh baint ag na coinníollacha i sraith de ghéaga `if
let`, `else if`, `else if let` lena chéile.

Cinneann an cód i Liostáil 19-1 cén dath atá le cur ar do chúlra bunaithe ar
shraith seiceálacha le haghaidh roinnt coinníollacha. Don sampla seo, chruthaíomar athróga le luachanna crua-chódaithe a d'fhéadfadh clár fíor a fháil ó ionchur úsáideora.

<Listing number="19-1" file-name="src/main.rs" caption="Mixing `if let`, `else if`, `else if let`, and `else`">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-01/src/main.rs}}
```

</Listing>

Má shonraíonn an t-úsáideoir dath is fearr leis, úsáidtear an dath sin mar chúlra.
Mura sonraítear aon dath is fearr leis agus gur Dé Máirt atá ann inniu, is glas an dath cúlra. Seachas sin, má shonraíonn an t-úsáideoir a n-aois mar shreang agus gur féidir linn é a pharsáil mar uimhir go rathúil, is corcra nó oráiste an dath ag brath ar luach na huimhreach. Mura bhfuil feidhm ag aon cheann de na coinníollacha seo, is gorm an dath cúlra.

Ligeann an struchtúr coinníollach seo dúinn tacú le riachtanais chasta. Leis na luachanna crua-chódaithe atá againn anseo, priontálfaidh an sampla seo `Using purple as the 
background color`.

Is féidir leat a fheiceáil gur féidir le `if let` athróga nua a thabhairt isteach freisin a scáthaíonn athróga atá ann cheana féin ar an mbealach céanna a fhéadann `match` arms: tugann an líne `if let Ok(age) = age` athróg nua `age` isteach ina bhfuil an luach taobh istigh den athraitheach `Ok`,
ag scáthú an athróg `age` atá ann cheana féin. Ciallaíonn sé seo go gcaithfimid an coinníoll `if age >
30` a chur laistigh den bhloc sin: ní féidir linn an dá choinníoll seo a chomhcheangal i `if
let Ok(age) = age && age > 30`. Níl an `age` nua ar mhaith linn a chur i gcomparáid le 30 bailí go dtí go dtosaíonn an raon feidhme nua leis an lúibín chatach.

Is é an míbhuntáiste a bhaineann le húsáid nathanna `if let` ná nach ndéanann an tiomsaitheoir seiceáil
le haghaidh uileghabhálachta, ach le nathanna `match` déanann sé. Dá mba rud é go bhfágfaimis an
bloc `else` deireanach ar lár agus dá bhrí sin go gcaillfimis láimhseáil roinnt cásanna, ní chuirfeadh an tiomsaitheoir foláireamh orainn faoin bhfadhb loighce féideartha.

### Lúba Coinníollach `while let`
Cosúil le `if let` i dtógáil, ceadaíonn an lúb coinníollach `while let` do lúb
`while` rith chomh fada agus a leanann patrún ag meaitseáil. Chonaiceamar lúb
`while let` den chéad uair i gCaibidil 17, áit ar úsáideadh é chun leanúint ar aghaidh ag lúbadh chomh fada agus a tháirg sruth luachanna nua. Ar an gcaoi chéanna, i Liostáil 19-2 taispeánaimid lúb `while let` a fhanann ar theachtaireachtaí a sheoltar idir snáitheanna, ach sa chás seo seiceálann sé `Result` in ionad `Option`.

<Listing number="19-2" caption="Using a `while let` loop to print values for as long as `rx.recv()` returns `Ok`">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-02/src/main.rs:here}}
```

</Listing>

Priontálann an sampla seo 1, 2, agus 3. Nuair a chonaiceamar `recv` siar i gCaibidil 16, dhíphacáileamar an earráid go díreach, nó idirghníomhaíomar léi mar athrá ag baint úsáide as lúb `for`. Mar a léiríonn Liostáil 19-2, áfach, is féidir linn `while let` a úsáid freisin, mar go dtugann an
modh `recv` `Ok` ar ais chomh fada agus a bhíonn an seoltóir ag táirgeadh teachtaireachtaí, agus ansin
gineann sé `Err` nuair a dhícheanglaíonn taobh an tseoltóra.

### Lúba `for`

I lúb `for`, is patrún é an luach a leanann an eochairfhocal `for` go díreach. Mar shampla, i `for x in y` is é an `x` an patrún. Léiríonn Liostáil 19-3
conas patrún a úsáid i lúb `for` chun tuple a dhístruchtúrú, nó a bhriseadh óna chéile, mar chuid den lúb `for`.	

<Listing number="19-3" caption="Using a pattern in a `for` loop to destructure a tuple">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-03/src/main.rs:here}}
```

</Listing>

Priontálfaidh an cód i Liosta 19-3 an méid seo a leanas:

```console
{{#include ../../listings/ch19-patterns-and-matching/listing-19-03/output.txt}}
```

Déanaimid oiriúnú ar athráiteoir ag baint úsáide as an modh `enumerate` ionas go dtáirgeann sé luach agus
an t-innéacs don luach sin, curtha i dtuple. Is é an chéad luach a tháirgtear ná an
tuple `(0, 'a')`. Nuair a mheaitseáiltear an luach seo leis an bpatrún `(index, value)`,
beidh `index` ina `0` agus beidh `value` ina `'a'`, ag priontáil an chéad líne den
aschur.

### Ráitis `let`

Roimh an gcaibidil seo, ní raibh pléite againn ach go sainráite ar úsáid patrún le
`match` agus `if let`, ach i ndáiríre, úsáideadh patrúin in áiteanna eile chomh maith,
lena n-áirítear i ráitis `let`. Mar shampla, smaoinigh ar an sannadh athróg simplí seo le `let`:

```rust
let x = 5;
```

Gach uair a d'úsáid tú ráiteas `let` mar seo, bhí tú ag úsáid patrúin, cé nach mbeadh a fhios agat é b'fhéidir! Ar bhealach níos foirmiúla, breathnaíonn ráiteas `let` mar seo:

```text
let PATTERN = EXPRESSION;
```

I ráitis cosúil le `let x = 5;` le hainm athróg sa sliotán `PATTERN`, níl san
ainm athróg ach foirm thar a bheith simplí de phatrún. Déanann Rust comparáid idir an abairt agus an patrún agus sannadh aon ainmneacha a aimsíonn sé. Mar sin, sa
shampla `let x = 5;`, is patrún é `x` a chiallaíonn "ceangail an rud a mheaitseálann anseo leis an
athróg `x`." Toisc gurb é an t-ainm `x` an patrún iomlán, ciallaíonn an patrún seo
go héifeachtach "ceangail gach rud leis an athróg `x`, cibé luach é."

Chun gné meaitseála patrún `let` a fheiceáil níos soiléire, smaoinigh ar Liostáil
19-4, a úsáideann patrún le `let` chun tuple a dhístruchtúrú.

<Listing number="19-4" caption="Using a pattern to destructure a tuple and create three variables at once">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-04/src/main.rs:here}}
```

</Listing>

Anseo, déanaimid tupla a mheaitseáil le patrún. Déanann Rust comparáid idir an luach `(1, 2, 3)` agus an patrún `(x, y, z)` agus feiceann sé go bhfuil an luach ag teacht leis an patrún, mar sin ceanglaíonn Rust `1` le `x`, `2` le `y`, agus `3` le `z`. Is féidir leat smaoineamh ar an patrún tupla seo
mar phatrún ina bhfuil trí phatrún athróg aonair neadaithe ann.

Mura bhfuil líon na n-eilimintí sa phatrún ag teacht le líon na n-eilimintí
sa tupla, ní bheidh an cineál foriomlán ag teacht leis agus gheobhaidh muid earráid tiomsaitheora. Mar
shampla, taispeánann Liostáil 19-5 iarracht tupla le trí
eilimint a dhístruchtúrú ina dhá athróg, rud nach n-oibreoidh.

<Listing number="19-5" caption="Incorrectly constructing a pattern whose variables don’t match the number of elements in the tuple">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-05/src/main.rs:here}}
```

</Listing>

Má dhéantar iarracht an cód seo a thiomsú, tagann an cineál earráide seo chun cinn:

```console
{{#include ../../listings/ch19-patterns-and-matching/listing-19-05/output.txt}}
```

Chun an earráid a shocrú, d'fhéadfaimis neamhaird a dhéanamh de cheann amháin nó níos mó de na luachanna sa tuple ag baint úsáide as
`_` nó `..`, mar a fheicfidh tú sa chuid [“Neamhaird a dhéanamh de Luachanna i
Patrún”][neamhaird-luachanna-i-patrún]<!-- neamhaird a dhéanamh -->. Más é an fhadhb
go bhfuil an iomarca athróg againn sa phatrún, is é an réiteach ná na
cineálacha a mheaitseáil trí athróga a bhaint ionas go mbeidh líon na n-athróg cothrom le líon
na n-eilimintí sa tuple.

### Paraiméadair Fheidhme

Is féidir le paraiméadair feidhme a bheith ina bpatrúin freisin. Ba chóir go mbeadh an cód i Liosta 19-6, a
dhearbhaíonn feidhm darb ainm `foo` a ghlacann paraiméadar amháin darb ainm `x` den chineál
`i32`, eolach anois.

<Listing number="19-6" caption="A function signature uses patterns in the parameters">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-06/src/main.rs:here}}
```

</Listing>

Is patrún é an chuid `x`! Mar a rinneamar le `let`, d’fhéadfaimis tuple in argóintí feidhme a mheaitseáil leis an patrún. Roinntear na luachanna i tuple agus muid á chur ar aghaidh chuig feidhm trí 19-7 a liostáil.

<Listing number="19-7" file-name="src/main.rs" caption="A function with parameters that destructure a tuple">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-07/src/main.rs}}
```

</Listing>

Priontálann an cód seo `Current location: (3, 5)`. Meaitseálann na luachanna `&(3, 5)` an patrún `&(x, y)`, mar sin is é `x` an luach `3` agus is é `y` an luach `5`.

Is féidir linn patrúin a úsáid i liostaí paraiméadair dúnta ar an mbealach céanna agus atá i
liostaí paraiméadair feidhme, toisc go bhfuil dúnta cosúil le feidhmeanna, mar a
phléitear i gCaibidil 13.

Ag an bpointe seo, tá roinnt bealaí feicthe agat chun patrúin a úsáid, ach ní
oibríonn patrúin mar an gcéanna i ngach áit is féidir linn iad a úsáid. I roinnt áiteanna, ní mór na patrúin a bheith
dochloíte; i gcúinsí eile, is féidir iad a bhréagnú. Pléifimid
an dá choincheap seo ina dhiaidh seo.

[ignoring-values-in-a-pattern]: ch19-03-pattern-syntax.html#ignoring-values-in-a-pattern