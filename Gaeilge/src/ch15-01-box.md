## Ag baint úsáide as `Box<T>` chun Pointe ar Shonraí ar an Charn

Is é an pointeoir cliste is simplí ná _box_, a bhfuil a chineál scríofa
`Box<T>`. Ligeann boscaí duit sonraí a stóráil ar an gcarn seachas ar an gcruach. Cad
fós ar an chairn an pointeoir do na sonraí gcarn. Déan tagairt do Chaibidil 4 go
athbhreithniú a dhéanamh ar an difríocht idir an chairn agus an gcarn.

Níl forchostais feidhmíochta ag boscaí, seachas a gcuid sonraí a stóráil ar an
gcarn in ionad ar an chruach. Ach níl mórán cumais bhreise acu
ach an oiread. Úsáidfidh tú iad is minice sna cásanna seo:

- Nuair a bhíonn cineál agat nach féidir a mhéid a bheith ar eolas ag am tiomsaithe agus atá uait
 luach den chineál sin a úsáid i gcomhthéacs a éilíonn méid beacht
- Nuair a bheidh tú méid mór sonraí agus ba mhaith leat a aistriú úinéireachta ach
 cinntigh nach ndéanfar na sonraí a chóipeáil nuair a dhéanann tú amhlaidh
- Nuair is mian leat luach a bheith agat agus is cuma leat ach gur cineál é sin
 cuireann sé tréith ar leith i bhfeidhm seachas a bheith de chineál ar leith

Léireoimid an chéad staid sna [“Cumasú Cineálacha Athchúrsacha le
Boscaí”](#enabling-recursive-types-with-boxes)<!-- neamhaird -->. Sa roinn
sa dara cás, is féidir go dtógfaidh sé tamall fada aistriú úinéireachta ar líon mór sonraí
am toisc go ndéantar na sonraí a chóipeáil timpeall ar an gcruach. Chun feidhmíocht a fheabhsú i
an staid seo, is féidir linn an méid mór sonraí a stóráil ar an gcarn i mbosca.
Ansin, ní dhéantar ach an méid beag sonraí pointeora a chóipeáil timpeall ar an gcruach,
agus fanann na sonraí dá dtagraíonn sé in aon áit amháin ar an gcarn. Is é an tríú cás
ar a dtugtar _trait object_, agus tugann Caibidil 18 roinn iomlán, [“Ag baint úsáide as
Réada Tréith a Ligeann Luachanna de Chineálacha Éagsúla,”][trait-objects]<!--
neamhaird a dhéanamh --> díreach leis an ábhar sin. Mar sin, an méid a fhoghlaimíonn tú anseo, cuirfidh tú isteach arís é
Caibidil 18!

### Ag baint úsáide as `Box<T>` chun Sonraí a Stóráil ar an Charn

Sula ndéanaimid plé ar an gcás úsáide stórála carn do `Box<T>`, clúdóimid an
comhréir agus conas idirghníomhú le luachanna atá stóráilte laistigh de `Box<T>`.

Léiríonn liostú 15-1 conas bosca a úsáid chun luach `i32` a stóráil ar an gcarn:

<Listing number="15-1" file-name="src/main.rs" caption="Storing an `i32` value on the heap using a box">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-01/src/main.rs}}
```

</Listing>

Sainmhínímid an athróg `b` chun luach `Box` a bheith aige a dhíríonn ar an
luach `5`, a leithdháiltear ar an gcarn. Priontálfaidh an clár seo `b = 5`; isteach
sa chás seo, is féidir linn rochtain a fháil ar na sonraí sa bhosca cosúil le conas a bheadh ​​muid dá mba é seo
bhí na sonraí ar an gcruach. Díreach mar aon luach faoi úinéireacht, nuair a théann bosca as
scóip, mar a dhéanann `b` ag deireadh `main`, déanfar é a dháileadh. Tá an
Tarlaíonn deallocation don bhosca (atá stóráilte ar an chruach) agus na sonraí é
pointí go (stóráilte ar an gcarn).

Níl sé an-úsáideach luach aonair a chur ar an gcarn, mar sin ní úsáidfidh tú boscaí faoi
iad féin ar an mbealach seo go minic. Ag luachanna cosúil le `i32` amháin ar an
Tá stack, áit a stóráiltear iad de réir réamhshocraithe, níos oiriúnaí don chuid is mó de
cásanna. Breathnaímid ar chás ina ligeann boscaí dúinn na cineálacha a shainímid
ní bheadh ​​cead againn mura mbeadh boscaí againn.

### Cineálacha Athchúrsacha a Chumasú le Boscaí

Is féidir luach eile den chineál céanna a bheith ag luach de chineál _recursive_ mar chuid de
féin. Cruthaíonn cineálacha athchúrsacha ceist mar go gcaithfidh meirge ag am tiomsaithe
fios cé mhéad spáis a thógann cineál. Mar sin féin, tá neadú luachanna na
d'fhéadfadh cineálacha athchúrsacha leanúint ar aghaidh go teoiriciúil gan teorainn, mar sin ní féidir le Rust a fhios conas
go leor spáis de dhíth ar an luach. Toisc go bhfuil méid aitheanta ag boscaí, is féidir linn a chumasú
cineálacha athchúrsacha trí bhosca a chur isteach sa sainmhíniú ar chineál athchúrsach.

Mar shampla de chineál athchúrsach, déanaimis iniúchadh ar an liosta _cons_. Is sonraí é seo
cineál a fhaightear go coitianta i dteangacha ríomhchlárúcháin feidhme. An cineál liosta míbhuntáistí
beidh muid a shainiú simplí ach amháin i gcás an atarlú; dá bhrí sin, an
beidh na coincheapa sa sampla a mbeimid ag obair leo úsáideach am ar bith a rachaidh tú isteach
cásanna níos casta a bhaineann le cineálacha athfhillteacha.

#### Tuilleadh Eolais Faoin Liosta Míbhuntáistí

Is struchtúr sonraí é _cons list_ a thagann ón teanga ríomhchlárúcháin Lisp
agus a chanúintí agus tá sé comhdhéanta de phéirí neadaithe, agus is é an leagan Lisp d'a
liosta nasctha. Tagann a ainm ón bhfeidhm `cons` (gearr le haghaidh "construct
function”) in Lisp a dhéanann péire nua óna dhá argóint
ag glaoch `cons` ar phéire comhdhéanta de luach agus péire eile, is féidir linn
déan liostaí míbhuntáistí a bheidh comhdhéanta de phéirí athchúrsacha.

Mar shampla, seo léiriú pseudocode de liosta míbhuntáistí a bhfuil an
liosta 1, 2, 3 le gach péire i lúibíní:

```téacs
(1, (2, (3, nialas)))
```

Tá dhá eilimint i ngach mír i liosta míbhuntáistí: luach na míre reatha
agus an chéad mhír eile. Níl sa mhír dheiridh ar an liosta ach luach darb ainm `Nil`
sin an chéad mhír eile. Táirgtear liosta míbhuntáistí trí na 'míbhuntáistí' a ghlaoch go hathchúrsach
feidhm. Is é an t-ainm canónach chun bunchás an atarlaithe a chur in iúl ná `Nil`.
Tabhair faoi deara nach ionann é seo agus an coincheap “neamhní” i gCaibidil 6,
atá ina luach neamhbhailí nó as láthair.

Ní struchtúr sonraí a úsáidtear go coitianta i Rust é an liosta míbhuntáistí. An chuid is mó den am
nuair a bhíonn liosta míreanna agat i Rust, is rogha níos fearr é `Vec<T>` le húsáid.
Cineálacha sonraí athfhillteacha eile atá níos casta _are_ úsáideach i gcásanna éagsúla,
ach ag tosú leis an liosta míbhuntáistí sa chaibidil seo, is féidir linn a iniúchadh conas boscaí
lig dúinn cineál sonraí athchúrsach a shainiú gan mórán seachráin.

I liostú 15-2 tá sainmhíniú enum le haghaidh liosta míbhuntáistí. Tabhair faoi deara go bhfuil an cód
ní thiomsóidh sé fós toisc nach bhfuil méid aitheanta ag an gcineál `List`, rud a
léireoimid.

<Listing number="15-2" file-name="src/main.rs" caption="The first attempt at defining an enum to represent a cons list data structure of `i32` values">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-02/src/main.rs:here}}
```

</Listing>

> Tabhair faoi deara: Tá liosta míbhuntáistí á gcur i bhfeidhm againn nach bhfuil ach luachanna `i32` le haghaidh an
> críocha an tsampla seo. D'fhéadfaimis é a chur i bhfeidhm ag baint úsáide as generics, mar a dhéanaimid
> a phléitear i gCaibidil 10, chun cineál liosta míbhuntáistí a shainiú a d'fhéadfadh luachanna de
> de shaghas ar bith.

Ag baint úsáide as an gcineál `List` chun an liosta `1, 2, 3` a stóráil bheadh ​​cuma an chóid ann
Liostáil 15-3:

<Listing number="15-3" file-name="src/main.rs" caption="Using the `List` enum to store the list `1, 2, 3`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-03/src/main.rs:here}}
```

</Listing>

Tá `1` ag an gcéad luach `Cons` agus luach `List` eile. Is é an luach `List` seo
luach `Cons` eile a bhfuil `2` aige agus luach `List` eile. An luach `List` seo
is luach `Cons` amháin eile a shealbhaíonn `3` agus luach `List`, atá ar deireadh
`Nil`, an t-athraitheach neamh-athfhillteach a chomharthaíonn deireadh an liosta.

Má dhéanaimid iarracht an cód a thiomsú i Liostú 15-3, faighimid an earráid a thaispeántar i
Liostáil 15-4:

<Listing number="15-4" file-name="output.txt" caption="The error we get when attempting to define a recursive enum">

```console
{{#include ../../listings/ch15-smart-pointers/listing-15-03/output.txt}}
```

</Listing>

Léiríonn an earráid seo "go bhfuil méid gan teorainn." Is é an chúis atá sainmhínithe againn
`List` le malairt athfhillteach: tá luach eile ann féin
go díreach. Mar thoradh air sin, ní féidir le Rust a dhéanamh amach cé mhéad spáis a theastaíonn uaidh a stóráil
luach `List`. Déanaimis briseadh síos cén fáth a bhfaighimid an earráid seo. Ar dtús, féachfaimid conas
Cinneann Rust cé mhéad spáis a theastaíonn uaidh chun luach de chineál neamh-athfhillteach a stóráil.

#### Méid Cineál Neamh-Athchúrsach a Ríomh

Athghairm an `Message` enum a mhínigh muid i Liostú 6-2 nuair a phléamar enum
sainmhínithe i gCaibidil 6:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-02/src/main.rs:here}}
```

Chun a chinneadh cé mhéad spáis atá le leithdháileadh ar luach `Message`, téann Rust
trí gach leagan chun a fháil amach cé acu malairt de dhíth ar an spás is mó. Meirge
feictear nach bhfuil spás ar bith de dhíth ar `Message::Quit`, tá go leor de dhíth ar `Message::Move`
spás chun dhá luach `i32` a stóráil, agus mar sin de. Toisc nach mbeidh ach leagan amháin ann
úsáidte, is é an spás is mó a bheidh ag teastáil ó luach `Message` ná an spás a thógfadh sé
stóráil an ceann is mó dá leagan.

Cuir é seo i gcodarsnacht leis an méid a tharlaíonn nuair a dhéanann Rust iarracht a fháil amach cé mhéad spáis a
cineál athchúrsach cosúil leis an enum `List` i Liostú 15-2 riachtanas. Tosaíonn an tiomsaitheoir
trí bhreathnú ar an leagan `Cons`, a bhfuil luach de chineál `i32` agus luach aige
den chineál `List`. Mar sin, tá gá le `Cons` méid spáis atá comhionann le méid
an `i32` móide méid `List`. Chun a dhéanamh amach cé mhéad cuimhne an `List`
riachtanais cineáil, breathnaíonn an tiomsaitheoir ar na leaganacha, ag tosú leis an `Cons`
athraitheach. Tá luach cineál `i32` agus luach cineáil ag an leagan `Cons`
`List`, agus leanann an próiseas seo gan teorainn, mar a thaispeántar i bhFíor 15-1.

<img alt="Liosta CONS gan teorainn" src="img/trpl15-01.svg" class="center" style="leithead: 50%;" />

<span class="caption">Fíor 15-1: ‘Liosta’ gan teorainn ina bhfuil éigríoch
Leaganacha `cons`</span>

#### Ag baint úsáide as `Box<T>` chun Cineál Athchúrsach a Fháil le Méid Aitheanta

Toisc nach féidir le Rust a dhéanamh amach cé mhéad spáis atá le leithdháileadh le haghaidh athchúrsach
cineálacha sainithe, tugann an tiomsaitheoir earráid leis an moladh cabhrach seo:

<!-- manual-regeneration
after doing automatic regeneration, look at listings/ch15-smart-pointers/listing-15-03/output.txt and copy the relevant line
-->

```text
help: insert some indirection (e.g., a `Box`, `Rc`, or `&`) to break the cycle
  |
2 |     Cons(i32, Box<List>),
  |               ++++    +
```

Sa mholadh seo, ciallaíonn “indíreach” sin in ionad luach a stóráil
go díreach, ba cheart dúinn an struchtúr sonraí a athrú chun an luach a stóráil go hindíreach trí
ag stóráil pointeoir don luach ina ionad sin.

Toisc gur pointeoir é `Box<T>`, bíonn a fhios ag Rust i gcónaí cé mhéad spáis atá i `Box<T>`
riachtanais: ní athraíonn méid an phointeora bunaithe ar an méid sonraí atá ann
ag tagairt do. Ciallaíonn sé seo gur féidir linn `Box<T>` a chur taobh istigh den leagan `Cons` ina ionad sin
de luach `List` eile go díreach. Díreoidh an `Box<T>` go dtí an chéad `List` eile
luach a bheidh ar an gcarn seachas taobh istigh den leagan `Cons`.
Go coincheapúil, tá liosta fós againn, a cruthaíodh le liostaí a bhfuil liostaí eile acu, ach
tá an cur i bhfeidhm seo níos cosúla anois leis na míreanna a chur in aice lena chéile
seachas taobh istigh dá chéile.

Is féidir linn an sainmhíniú ar an `List` enum i Liostú 15-2 agus an úsáid a athrú
den `List` i Liostú 15-3 leis an gcód i Liostú 15-5, a thiomsóidh:

<Listing number="15-5" file-name="src/main.rs" caption="Definition of `List` that uses `Box<T>` in order to have a known size">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-05/src/main.rs}}
```

</Listing>

Tá méid `i32` de dhíth ar an leagan `Cons` mar aon leis an spás chun an
sonraí pointeoir an bhosca. Ní stórálann an leagan `Nil` aon luachanna, mar sin teastaíonn níos lú spáis uaidh
ná an leagan `Cons`. Tá a fhios againn anois go nglacfaidh aon luach `List` leis an
méid `i32` móide méid sonraí pointeoir an bhosca. Trí úsáid a bhaint as bosca, tá
briste an slabhra gan teorainn, athchúrsach, ionas gur féidir leis an tiomsaitheoir an méid a dhéanamh amach
ní mór dó luach `List` a stóráil. Léiríonn Figiúr 15-2 cad é an leagan `Cons`
cuma anois.

<img alt="A finite Cons list" src="img/trpl15-02.svg" class="center" />

<span class="caption">Figure 15-2: A `List` that is not infinitely sized
because `Cons` holds a `Box`</span>

Ní sholáthraíonn boscaí ach an t-indíreach agus an leithdháileadh carn; níl aon acu
cumais speisialta eile, cosúil leis na cinn a fheicfimid leis an bpointeoir cliste eile
cineálacha. Níl an forchostas feidhmíochta acu chomh maith ná na cinn speisialta seo
cumais a thabhú, ionas gur féidir leo a bheith úsáideach i gcásanna cosúil leis an liosta míbhuntáistí a bhfuil an
is é indirection an t-aon ghné a theastaíonn uainn. Breathnóimid ar níos mó cásanna úsáide do bhoscaí
i gCaibidil 18, freisin.

Is pointeoir cliste é an cineál `Box<T>` toisc go gcuireann sé an trait `Deref` i bhfeidhm,
rud a ligeann do luachanna `Box<T>` a láimhseáil mar thagairtí. Nuair a bhíonn `Box<T>`
Téann luach as an raon feidhme, déantar na sonraí carn a bhfuil an bosca ag díriú orthu a ghlanadh
suas chomh maith mar gheall ar chur i bhfeidhm na tréithe `Drop`. Beidh an dá thréith seo
níos tábhachtaí fós maidir leis an bhfeidhmiúlacht a sholáthraíonn an pointeoir cliste eile
cineálacha a phléfaimid sa chuid eile den chaibidil seo. Déanaimis iniúchadh ar an dá thréith seo
níos mine.

[trait-objects]: ch18-02-trait-objects.html#using-trait-objects-that-allow-for-values-of-different-types