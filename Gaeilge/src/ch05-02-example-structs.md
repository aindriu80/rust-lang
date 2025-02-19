## Clár Samplach ag Úsáid Structs

Chun a thuiscint cathain a d’fhéadfadh muid a bheith ag iarraidh struchtúir a úsáid, scríobhaimis clár a
ríomhann sé achar dronuilleog. Tosóimid trí athróga aonair a úsáid, agus
ansin athmhacnaigh an clár go dtí go mbeimid ag úsáid structs ina ionad.

Déanaimis tionscadal dénártha nua le lasta ar a dtugtar _rectangles_ a ghlacfaidh
leithead agus airde dronuilleog sonraithe i bpicteilín agus ríomh an t-achar
den dronuilleog. Léiríonn liostú 5-8 clár gearr le bealach amháin le déanamh
go díreach é sin i _src/main.rs_ ár dtionscadal.

<Listing number="5-8" file-name="src/main.rs" caption="Calculating the area of a rectangle specified by separate width and height variables">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-08/src/main.rs:all}}
```

</Listing>

Now, run this program using `cargo run`:

```console
{{#include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-08/output.txt}}
```

Éiríonn leis an gcód seo achar na dronuilleoige a dhéanamh amach trí ghlaoch a chur ar an
feidhm `area` le gach gné, ach is féidir linn níos mó a dhéanamh chun an cód seo a dhéanamh soiléir
agus inléite.

Tá an tsaincheist leis an gcód seo le feiceáil i síniú `area`:

```rust,ignore
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-08/src/main.rs:here}}
```

Tá an fheidhm `area` ceaptha chun achar dronuilleog amháin a ríomh, ach an
tá dhá pharaiméadar ag an bhfeidhm a scríobhamar, agus níl sé soiléir áit ar bith inár
clár go bhfuil baint ag na paraiméadair. Bheadh ​​​​sé níos inléite agus níos mó
inbhainistithe leithead agus airde a ghrúpáil le chéile. Tá bealach amháin pléite againn cheana féin
d'fhéadfaimis é sin a dhéanamh sa ["An Cineál Tuple"][the-tuple-type]<!-- neamhaird a dhéanamh ar --> alt
de Chaibidil 3: trí úsáid a bhaint as tuples.

### Athmhachnamh le Tuples

Léiríonn liostú 5-9 leagan eile dár gclár a úsáideann tuples.

<Listing number="5-9" file-name="src/main.rs" caption="Specifying the width and height of the rectangle with a tuple">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-09/src/main.rs}}
```

</Listing>

Ar bhealach amháin, tá an clár seo níos fearr. Tuples in iúl dúinn a chur le beagán de struchtúr, agus
níl ach argóint amháin á rith againn anois. Ach ar bhealach eile, tá an leagan seo níos lú
soiléir: ní ainmníonn tuples a n-eilimintí, mar sin ní mór dúinn a innéacsú isteach i gcodanna
an tuple, rud a fhágann nach bhfuil ár ríomh chomh soiléir.

Ní bhainfeadh an leithead agus an airde a mheascadh le ríomh an limistéir, ach dá mbeadh
ba mhaith linn an dronuilleog a tharraingt ar an scáileán, is cuma! Bheadh ​​orainn
coinnigh i gcuimhne gurb é `width` an t-innéacs tuple `0` agus is é `height` an tuple
innéacs `1`. Bheadh ​​sé seo níos deacra fós do dhuine eile a dhéanamh amach agus a choinneáil i
aigne dá mba rud é go n-úsáidfeadh siad ár gcód. Toisc nach bhfuil muid tar éis an bhrí a chur in iúl
ár sonraí inár gcód, tá sé níos éasca anois earráidí a thabhairt isteach.

### Athmhacrú le Struchtúir: Níos Mó Brí a Chur Leis

Bainimid úsáid as struchtúir chun brí a chur leis trí na sonraí a lipéadú. Is féidir linn an tuple a athrú
táimid ag baint úsáide as struchtúr le ainm don iomlán chomh maith le hainmneacha don
páirteanna, mar a thaispeántar i Liosta 5-10.

<Listing number="5-10" file-name="src/main.rs" caption="Defining a `Rectangle` struct">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-10/src/main.rs}}
```

</Listing>

Anseo tá struchtúr sainmhínithe againn agus thugamar `Rectangle` air. Laistigh den chuach
lúibíní, shainmhíníomar na réimsí mar `width` agus `height`, a bhfuil an dá cheann acu
clóscríobh `u32`. Ansin, i `main`, chruthaíomar sampla ar leith de `Rectangle`
go bhfuil leithead `30` agus airde `50`.

Tá ár bhfeidhm `area` sainmhínithe anois le paraiméadar amháin, atá ainmnithe againn
`Rectangle`, a bhfuil a chineál ar iasacht do-inaistrithe de struchtúr `Rectangle`
shampla. Mar a luadh i gCaibidil 4, ba mhaith linn an struct a fháil ar iasacht seachas
úinéireacht a ghlacadh air. Ar an mbealach seo, coimeádann `main` a úinéireacht agus is féidir leanúint ar aghaidh
ag baint úsáide as `rect1`, agus sin é an fáth a n-úsáidimid an `&` sa síniú feidhme agus
an áit a dtugaimid an fheidhm.

Faigheann an fheidhm `area` rochtain ar na réimsí `width` agus `height` sa `Rectangle`
shampla (tabhair faoi deara nach ionann rochtain a fháil ar réimsí den struchtúr a fuarthas ar iasacht
na luachanna réimse a bhogadh, agus sin an fáth a fheiceann tú go minic ar iasacht de struchtúir). Ár
deir síniú feidhme do `area` anois go díreach cad atá i gceist againn: ríomh an t-achar
de `Rectangle`, ag baint úsáide as a réimsí `width` agus `height`. Tugann sé seo le fios go bhfuil an
tá leithead agus airde gaolmhar lena chéile, agus tugann sé ainmneacha tuairisciúla ar
na luachanna seachas na luachanna comhinnéacs tuple de `0` agus `1` a úsáid. Seo a
buaigh ar mhaithe le soiléireacht.

### Feidhmiúlacht Úsáideach a Chur le Tréithe Díorthaithe

Bheadh ​​sé úsáideach a bheith in ann sampla de `Rectangle` a phriontáil agus muid
dífhabhtaigh ár gclár agus féach ar na luachanna dá réimsí go léir. Liostáil 5-11 iarracht
ag baint úsáide as an [`println!` macro][println]<!-- neamhaird --> mar a d'úsáideamar i
caibidlí roimhe seo. Ní oibreoidh sé seo, áfach.

<Listing number="5-11" file-name="src/main.rs" caption="Attempting to print a `Rectangle` instance">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-11/src/main.rs}}
```

</Listing>

Nuair a thiomsaimid an cód seo, faighimid earráid leis an bpríomhtheachtaireacht seo:

```text
{{#include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-11/output.txt:3}}
```

Is féidir leis an macra `println!` go leor cineálacha formáidithe a dhéanamh, agus de réir réamhshocraithe, an chatach
insíonn lúibíní do `println!` formáidiú ar a dtugtar `Display` a úsáid: an t-aschur atá beartaithe
le haghaidh tomhaltas díreach úsáideora deiridh. Na cineálacha primitive atá feicthe againn go dtí seo
cuir `Display` i bhfeidhm de réir réamhshocraithe mar níl ach bealach amháin ann ar mhaith leat a thaispeáint
a `1` nó aon chineál primitive eile d'úsáideoir. Ach le structs, ar an mbealach
Ba cheart go bhformáid `println!` nach bhfuil an t-aschur chomh soiléir mar go bhfuil níos mó ann
féidearthachtaí taispeána: Ar mhaith leat camóga nó nach bhfuil? Ar mhaith leat an
lúibíní curly? Ar chóir na réimsí go léir a thaispeáint? Mar gheall ar an débhríocht seo, Rust
ní dhéanann sé iarracht buille faoi thuairim a dhéanamh ar cad atá uainn, agus níl aon soláthar ag struchtúir
`Display` a chur i bhfeidhm le húsáid le `println!` agus an sealbhóir áite `{}`.

Má leanaimid ar aghaidh ag léamh na n-earráidí, gheobhaidh muid an nóta cabhrach seo:

```text
{{#include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-11/output.txt:9:10}}
```

Déanaimis iarracht é! Beidh cuma anois ar an nglao macra `println!` mar `println! ("rect1 is
{rect1:?}");`. Ag cur an sonraitheora `:?` taobh istigh de na lúibíní cuartha insíonn
`println!` ba mhaith linn formáid aschuir ar a dtugtar `Debug` a úsáid. An trait `Debug`
cuireann sé ar ár gcumas ár struchtúr a phriontáil ar bhealach atá úsáideach d'fhorbróirí ionas gur féidir linn
féach ar a luach agus muid ag dífhabhtú ár gcód.

Tiomsaigh an cód leis an athrú seo. Drat! Faighimid earráid fós:

```text
{{#include ../../listings/ch05-using-structs-to-structure-related-data/output-only-01-debug/output.txt:3}}
```

Ach arís, tugann an tiomsaitheoir nóta cabhrach dúinn:

```text
{{#include ../../listings/ch05-using-structs-to-structure-related-data/output-only-01-debug/output.txt:9:10}}
```

Rust _does_ san áireamh feidhmiúlacht chun faisnéis debugging a phriontáil amach, ach táimid
ní mór dúinn tarraingt isteach go sainráite chun an fheidhmiúlacht sin a chur ar fáil dár struchtúr.
Chun é sin a dhéanamh, cuirimid an tréith sheachtrach `#[derive(Debug)]` díreach roimh an
struct sainmhíniú, mar a thaispeántar i Liostú 5-12.

<Listing number="5-12" file-name="src/main.rs" caption="Adding the attribute to derive the `Debug` trait and printing the `Rectangle` instance using debug formatting">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-12/src/main.rs}}
```

</Listing>

Anois agus an clár á rith againn, ní bhfaighidh muid aon earráidí, agus feicfidh muid an
aschur seo a leanas:

```console
{{#include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-12/output.txt}}
```

Go deas! Ní hé an t-aschur is deise é, ach taispeánann sé luachanna na réimsí go léir
sa chás seo, rud a chuideodh go cinnte le linn dífhabhtaithe. Nuair atá againn
struchtúir níos mó, tá sé úsáideach aschur a bheith agat atá beagán níos éasca le léamh; isteach
sna cásanna sin, is féidir linn `{:#?}` a úsáid in ionad `{:?}` sa teaghrán `println!`. I
an sampla seo, ag baint úsáide as an stíl `{:#?}` aschuirfear an méid seo a leanas:

```consól
{{#include ../../listings/ch05-using-structs-to-structure-related-data/output-only-02-pretty-debug/output.txt}}
```

Bealach eile chun luach a phriontáil ag baint úsáide as an bhformáid `Debug` is ea an [`dbg!`
macro][dbg] <!-- neamhaird -->a úsáid, a ghlacann úinéireacht slonn (seachas
go `println!`, a thógann tagairt), priontaí an comhad agus uimhir líne na
áit a dtarlaíonn an macraghlao `dbg!` sin i do chód mar aon leis an luach iarmhartach
den slonn sin, agus tugann sé úinéireacht ar an luach ar ais.

> Nóta: Ag glaoch ar an `dbg!` priontaí macra chuig an sruth caighdeánach consól earráide
> (`stderr`), seachas `println!`, a phriontálann go dtí an t-aschur caighdeánach
> sruth consól (`stdout`). Labhróimid níos mó faoi `stderr` agus `stdout` sa
> [“Teachtaireachtaí Earráide á Scríobh go Earráid Chaighdeánach In ionad Aschur Caighdeánach”
> alt i gCaibidil 12][err]<!-- neamhaird -->.

Seo sampla ina bhfuil suim againn sa luach a shanntar don
réimse `width`, chomh maith le luach an struchtúir iomláin in `rect1`:

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/no-listing-05-dbg-macro/src/main.rs}}
```

Is féidir linn `dbg!` a chur timpeall ar an slonn `scale 30 *` agus, toisc go bhfuil `dbg!`
ar ais úinéireacht ar luach na slonn, gheobhaidh an réimse `width` an
an luach céanna mura mbeadh an glao `dbg!` againn ann. Nílimid ag iarraidh `dbg!` a
seilbh a ghlacadh ar `rect1`, mar sin úsáidimid tagairt do `rect1` sa chéad ghlao eile.
Seo an chuma atá ar aschur an tsampla seo:

```console
{{#include ../../listings/ch05-using-structs-to-structure-related-data/no-listing-05-dbg-macro/output.txt}}
```

Is féidir linn a fheiceáil gur tháinig an chéad phíosa aschuir ó _src/main.rs_ líne 10 áit a bhfuilimid
ag dífhabhtú na slonn `30 * scale`, agus is é an luach iarmhartach ná `60` (an
Is éard atá i gceist le formáidiú `Debug` a chuirtear i bhfeidhm le haghaidh slánuimhreacha a luach a phriontáil amháin. Tá an
Aschuir `dbg!` glao ar líne 14 de _src/main.rs_ luach `&rect1`, is é sin
an struchtúr `Rectangle`. Úsáideann an t-aschur seo formáidiú deas `Debug` an
Cineál `Rectangle`. Is féidir leis an macra `dbg!` a bheith an-chabhrach agus tú ag iarraidh é a dhéanamh
déan amach cad atá á dhéanamh ag do chód!

Chomh maith leis an trait `Debug`, tá Rust tar éis roinnt tréithe a sholáthar dúinn
a úsáid leis an tréith `derive` ar féidir a iompar úsáideach a chur lenár saincheaptha
cineálacha. Tá na tréithe sin agus a n-iompraíocht liostaithe in [Aguisín C][app-c]<!--
neamhaird a dhéanamh -->. Clúdóimid conas na tréithe seo a chur i bhfeidhm le hiompar saincheaptha mar
chomh maith le conas do chuid tréithe féin a chruthú i gCaibidil 10. Tá go leor ann freisin
tréithe seachas `derive`; le haghaidh tuilleadh eolais, féach [na “Tréithe”
chuid den Tagairt Rust][attributes].

Tá ár bhfeidhm `area` an-sonrach: ní ríomhann sé ach achar na dronuilleogach.
Bheadh ​​sé ina chuidiú an t-iompar seo a cheangal níos dlúithe lenár struchtúr `Rectangle`
mar ní oibreoidh sé le haon chineál eile. Breathnaímid ar conas is féidir linn leanúint ar aghaidh
athmhonaraigh an cód seo tríd an bhfeidhm `area` a iompú ina `area` _method_
sainithe ar ár gcineál `Rectangle`.

[the-tuple-type]: ch03-02-data-types.html#the-tuple-type
[app-c]: appendix-03-derivable-traits.md
[println]: ../std/macro.println.html
[dbg]: ../std/macro.dbg.html
[err]: ch12-06-writing-to-stderr-instead-of-stdout.html
[attributes]: ../reference/attributes.html