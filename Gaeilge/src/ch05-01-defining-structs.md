## Struchtúir a Shainmhíniú agus a Thionscnamh

Tá struchtúir cosúil le tuples, a phléitear in [“An Cineál Tuple”][tuples]<!--
neamhaird a dhéanamh ar --> alt, sa mhéid is go bhfuil luachanna gaolmhara iolracha ag an dá cheann. Cosúil le tuples, an
is féidir cineálacha éagsúla a bheith i bpíosaí struchtúir. Murab ionann agus tuples, i struct
ainmneoidh tú gach píosa sonraí ionas go mbeidh sé soiléir cad a chiallaíonn na luachanna. Ag cur leo seo
Ciallaíonn ainmneacha go bhfuil struchtúir níos solúbtha ná tuples: ní gá duit a bheith ag brath
ar ord na sonraí chun luachanna an tsampla a shonrú nó a rochtain.

Chun struchtúr a shainiú, cuirimid an eochairfhocal `struct` isteach agus ainmnímid an struchtúr iomlán. A
ba chóir go ndéanfadh ainm struct cur síos ar thábhacht na bpíosaí sonraí atá ann
grúpáilte le chéile. Ansin, taobh istigh de lúibíní curly, sainímid ainmneacha agus cineálacha
na píosaí sonraí, ar a dtugaimid _fields_. Mar shampla, taispeánann Liostú 5-1 a
struchtúr a stórálann faisnéis faoi chuntas úsáideora.

<Listing number="5-1" file-name="src/main.rs" caption="A `User` struct definition">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-01/src/main.rs:here}}
```

</Listing>

Chun struchtúr a úsáid tar éis dúinn é a shainiú, cruthaímid _gcás_ den struchtúr sin
trí luachanna nithiúla a shonrú do gach ceann de na réimsí. Cruthaímid sampla trí
ag lua ainm an struchtúir agus ansin cuir lúibíní curlaí ina bhfuil _key:
value_ péirí, áit a bhfuil na heochracha ainmneacha na réimsí agus na luachanna an
sonraí ba mhaith linn a stóráil sna réimsí sin. Ní gá dúinn na réimsí a shonrú i
an t-ord céanna inar dhearbhaigh muid iad sa struct. I bhfocail eile, tá an
Tá sainmhíniú struchtúr cosúil le teimpléad ginearálta don chineál, agus cásanna a líonadh
sa teimpléad sin le sonraí ar leith chun luachanna den chineál a chruthú. Le haghaidh
Mar shampla, is féidir linn úsáideoir áirithe a dhearbhú mar a thaispeántar i Liostú 5-2.

<Listing number="5-2" file-name="src/main.rs" caption="Creating an instance of the `User` struct">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-02/src/main.rs:here}}
```

</Listing>

Chun luach sonrach a fháil ó struchtúr, úsáidimid nodaireacht poncanna. Mar shampla, go
rochtain a fháil ar sheoladh ríomhphoist an úsáideora seo, úsáidimid `user1.email`. Más é an cás
mutable, is féidir linn luach a athrú tríd an nodaireacht ponc a úsáid agus a shannadh isteach i
réimse ar leith. Léiríonn liostú 5-3 conas an luach sa `email` a athrú
réimse shampla `User` mutable.

<Listing number="5-3" file-name="src/main.rs" caption="Changing the value in the `email` field of a `User` instance">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-03/src/main.rs:here}}
```

</Listing>

Tabhair faoi deara go gcaithfidh an ásc iomlán a bheith mutable; Ní ligeann meirge dúinn marcáil
ach réimsí áirithe mar shoghluaiste. Mar is amhlaidh le haon slonn, is féidir linn ceann nua a thógáil
shampla an struct mar an slonn deiridh i gcorp feidhme a
go hintuigthe cuir ar ais an cás nua sin.

Taispeánann liostú 5-4 feidhm `build_user` a sheolann sampla `User` ar ais le
an seoladh ríomhphoist agus an t-ainm úsáideora a tugadh. Faigheann an réimse `active` luach `true`, agus
faigheann an `sign_in_count` luach `1`.

<Listing number="5-4" file-name="src/main.rs" caption="A `build_user` function that takes an email and username and returns a `User` instance">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-04/src/main.rs:here}}
```

</Listing>

Déanann sé ciall paraiméadair na feidhme a ainmniú leis an ainm céanna leis an struchtúr
réimsí, ach caithfidh tú na hainmneacha réimse `email` agus `username` a athdhéanamh agus
athróga beagán tedious. Dá mbeadh níos mó réimsí sa struchtúr, agus gach ainm á athrá
bheadh ​​níos mó fós annoying. Ar ámharaí an tsaoil, tá gearrscannán áisiúil ann!

<!-- Old heading. Do not remove or links may break. -->

<a id="using-the-field-init-shorthand-when-variables-and-fields-have-the-same-name"></a>

### Ag baint úsáide as an Réimse Init Gearrlámh

Toisc go bhfuil ainmneacha na bparaiméadar agus na hainmneacha páirce struct díreach mar a chéile i
Ag liostú 5-4, is féidir linn an chomhréir _field init shorthand_ a úsáid chun athscríobh
`build_user` mar sin iompraíonn sé díreach mar an gcéanna ach ní bhíonn an athrá air
`username` agus `email`, mar a thaispeántar i Liostú 5-5.

<Listing number="5-5" file-name="src/main.rs" caption="A `build_user` function that uses field init shorthand because the `username` and `email` parameters have the same name as struct fields">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-05/src/main.rs:here}}
```

</Listing>

Anseo, táimid ag cruthú sampla nua den struchtúr `User`, a bhfuil réimse aige
darb ainm `email`. Ba mhaith linn luach an réimse `email` a shocrú go dtí an luach sa
paraiméadar `email` den fheidhm `build_user`. Toisc go bhfuil an réimse `email` agus
Tá an t-ainm céanna ar an bparaiméadar `email`, ní gá dúinn ach `email` a scríobh in áit
ná `email: email`.

### Cásanna a Chruthú ó Chásanna Eile le Comhréir Nuashonraithe Struchtúr

Is minic a bhíonn sé úsáideach sampla nua de struchtúr a chruthú a chuimsíonn an chuid is mó de
na luachanna ó shampla eile, ach athraíonn roinnt. Is féidir leat é seo a dhéanamh ag baint úsáide as
_struct nuashonraigh comhréir_.

Ar dtús, i Liostú 5-6 léirímid conas mar shampla `User` nua a chruthú in `user2`
go rialta, gan an chomhréir nuashonraithe. Shocraigh muid luach nua do `email` ach
nó bain úsáid as na luachanna céanna ó `user1` a chruthaigh muid i Liostú 5-2.

<Listing number="5-6" file-name="src/main.rs" caption="Creating a new `User` instance using all but one of the values from `user1`">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-06/src/main.rs:here}}
```

</Listing>

Ag baint úsáide as comhréir nuashonraithe struct, is féidir linn an éifeacht chéanna a bhaint amach le níos lú cód, mar
léirithe i Liosta 5-7. Sonraíonn an chomhréir `..` nach bhfuil na réimsí atá fágtha
ba cheart go mbeadh an luach céanna ag na réimsí a leagtar síos go sainráite agus atá ag na réimsí sa chás ar leith.

<Listing number="5-7" file-name="src/main.rs" caption="Using struct update syntax to set a new `email` value for a `User` instance but to use the rest of the values from `user1`">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-07/src/main.rs:here}}
```

</Listing>

Cruthaíonn an cód i Liostú 5-7 sampla freisin in `user2` a bhfuil a
luach difriúil don `email` ach tá na luachanna céanna aige don `username`,
réimsí `active`, agus `sign_in_count` ó `user1`. Caithfidh an `..user1` teacht ar deireadh
a shonrú gur cheart go bhfaigheadh ​​aon réimsí atá fágtha a luachanna ó na
réimsí comhfhreagracha in `user1`, ach is féidir linn a roghnú luachanna a shonrú mar
go leor réimsí mar ba mhaith linn in aon ord, beag beann ar ord na réimsí i
sainmhíniú an struchtúir.

Tabhair faoi deara go n-úsáideann an chomhréir nuashonraithe struct `=` cosúil le tasc; tá sé seo mar gheall ar
bogann sé na sonraí, díreach mar a chonaic muid sa [“Athróga agus Sonraí Idirghníomhú le
Bog”][bogadh]<!-- neamhaird --> alt. Sa sampla seo, ní féidir linn a úsáid a thuilleadh
`user1` ina iomláine tar éis `user2` a chruthú mar go bhfuil an `String` sa
Bogadh an réimse `username` de `user1` go `user2`. Dá mbeadh `user2` nua tugtha againn
Luachanna `String` le haghaidh `email` agus `username` araon, agus mar sin níor úsáideadh ach an
luachanna `active` agus `sign_in_count` ó `user1`, ansin bheadh ​​`user1` fós
bailí tar éis `user2` a chruthú. Is cineálacha iad `active` agus `sign_in_count` araon
an tréith `Copy` a chur i bhfeidhm, mar sin an iompar a phléamar sa [“Stack-Only
Sonraí: Cóipeáil”][cóip]<!-- neamhaird --> bheadh ​​feidhm ag an alt. Is féidir linn a úsáid fós
`user1.email` sa sampla seo, toisc gur _ní_ bogadh amach a luach.

### Ag Úsáid Struchtúir Tuple Gan Réimsí Ainmnithe chun Cineálacha Éagsúla a Chruthú

Tacaíonn meirge freisin le struchtúir atá cosúil le tuples, ar a dtugtar _tuple structs_.
Tá an bhrí bhreise ag struchtúir tuple a sholáthraíonn an t-ainm struchtúir ach níl an bhrí eile aige
ainmneacha a bhaineann lena réimsí; in áit, níl acu ach cineálacha an
réimsí. Tá struchtúir tuple úsáideach nuair is mian leat ainm a thabhairt don tuple iomlán
agus déan cineál difriúil den tuple ó thuple eile, agus nuair a ainmnítear gach ceann acu
réimse mar atá i struchtúr rialta bheadh ​​briathra nó iomarcach.

Chun tuple struct a shainiú, cuir tús leis an eochairfhocal `struct` agus an t-ainm struct
ina dhiaidh sin na cineálacha sa tuple. Mar shampla, anseo sainímid agus úsáidimid dhá cheann
tuple structs darb ainm `Color` agus `Point`:

<Listing file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/no-listing-01-tuple-structs/src/main.rs}}
```

</Listing>

Tabhair faoi deara gur cineálacha difriúla iad na luachanna `black` agus `origin` toisc go bhfuil siad
cásanna de struchtúir tuple éagsúla. Is é a chineál féin gach struchtúr a shainíonn tú,
cé go bhféadfadh na cineálacha céanna a bheith sna réimsí laistigh den struchtúr. Le haghaidh
Mar shampla, ní féidir le feidhm a ghlacann paraiméadar den chineál `Color` a
`Point` mar argóint, cé go bhfuil an dá chineál comhdhéanta de thrí `i32`
luachanna. Seachas sin, tá cásanna tuple struct cosúil le tuples sa mhéid is gur féidir leat
iad a scrios ina bpíosaí aonair, agus is féidir leat úsáid a bhaint as `.` dhiaidh sin
ag an innéacs chun rochtain a fháil ar luach aonair. Murab ionann agus tuples, tuple structs
iarraidh ort an cineál struchtúir a ainmniú nuair a dhéanann tú iad a mhilleadh. Le haghaidh
Mar shampla, scríobhfaimis `Let Point(x, y, z) = point`.

### Struchtúir atá cosúil le hAonad gan Réimsí ar bith

Is féidir leat struchtúir a shainiú freisin nach bhfuil réimsí ar bith acu! Tugtar iad seo
_unit-like structs_ toisc go n-iompraíonn siad mar an gcéanna le `()`, cineál an aonaid sin
luaigh muid i ["An Cineál Tuple"][tuples]<!-- neamhaird --> alt. Aonad-mhaith
is féidir le struchtúir a bheith úsáideach nuair is gá duit tréith de chineál éigin a chur i bhfeidhm ach nach ndéanann
aon sonraí is mian leat a stóráil sa chineál féin. Pléifimid tréithe
i gCaibidil 10. Seo sampla de struchtúr aonaid a dhearbhú agus a thabhairt ar an toirt
darb ainm `AlwaysEqual`:

<Listing file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/no-listing-04-unit-like-structs/src/main.rs}}
```

</Listing>

Chun `AlwaysEqual` a shainiú, úsáidimid an eochairfhocal `struct`, an t-ainm a theastaíonn uainn, agus
ansin leathstad. Níl gá le lúibíní nó lúibíní chatach! Ansin is féidir linn a fháil ar
mar shampla de `AlwaysEqual` san athróg `subject` ar bhealach comhchosúil: ag baint úsáide as an
an t-ainm atá sainmhínithe againn, gan aon lúibíní nó lúibíní chatach. Samhlaigh sin níos déanaí
cuirfimid iompar den chineál seo i bhfeidhm ionas go mbeidh gach cás de
Bíonn `AlwaysEqual` i gcónaí cothrom le gach cás d'aon chineál eile, b'fhéidir
go mbeadh toradh aitheanta acu chun críocha tástála. Ní bheadh ​​aon sonraí ag teastáil uainn
cuir an t-iompar sin i bhfeidhm! Feicfidh tú i gCaibidil 10 conas tréithe a shainiú agus
iad a chur i bhfeidhm ar aon chineál, lena n-áirítear struchtúir aonad-mhaith.

> ### Úinéireacht Sonraí Struchtúr
>
> Sa sainmhíniú ar struchtúr `User` i Liostú 5-1, d'úsáideamar an `String` faoi úinéireacht
> cineál seachas an cineál sliseog teaghrán `&str`. Is rogha d'aon ghnó é seo
> mar ba mhaith linn go mbeadh úinéireacht ag gach cás den struchtúr seo ar a chuid sonraí go léir agus ar a son
> go mbeidh na sonraí sin bailí chomh fada agus a bheidh an struchtúr iomlán bailí.
>
> Is féidir freisin do struchtúir tagairtí a stóráil do shonraí ar le rud éigin iad
> eile, ach chun é sin a dhéanamh teastaíonn úsáid _lifetimes_, gné Rust a dhéanfaimid
> pléigh i gCaibidil 10. Cinntíonn Saolré go bhfuil na sonraí dá dtagraítear ag struct
> bailí chomh fada agus atá an struchtúr. Ligean le rá go ndéanann tú iarracht tagairt a stóráil
> i struchtúr gan saolréanna a shonrú, mar a leanas; ní oibreoidh sé seo:
>
> <Listing file-name="src/main.rs">
>
> <!-- CAN'T EXTRACT SEE https://github.com/rust-lang/mdBook/issues/1127 -->
>
> ```rust,ignore,does_not_compile
> struct User {
>     active: bool,
>     username: &str,
>     email: &str,
>     sign_in_count: u64,
> }
>
> fn main() {
>     let user1 = User {
>         active: true,
>         username: "someusername123",
>         email: "someone@example.com",
>         sign_in_count: 1,
>     };
> }
> ```
>
> </Listing>
>
> Déanfaidh an tiomsaitheoir gearán go bhfuil sonraíocht saoil de dhíth air:
>
> ```console
> $ cargo run
>    Compiling structs v0.1.0 (file:///projects/structs)
> error[E0106]: missing lifetime specifier
>  --> src/main.rs:3:15
>   |
> 3 |     username: &str,
>   |               ^ expected named lifetime parameter
>   |
> help: consider introducing a named lifetime parameter
>   |
> 1 ~ struct User<'a> {
> 2 |     active: bool,
> 3 ~     username: &'a str,
>   |
>
> error[E0106]: missing lifetime specifier
>  --> src/main.rs:4:12
>   |
> 4 |     email: &str,
>   |            ^ expected named lifetime parameter
>   |
> help: consider introducing a named lifetime parameter
>   |
> 1 ~ struct User<'a> {
> 2 |     active: bool,
> 3 |     username: &str,
> 4 ~     email: &'a str,
>   |
>
> Chun tuilleadh eolais a fháil faoin earráid seo, bain triail as `rustc --explain E0106`.
> error: níorbh fhéidir `structs` (bin "structs") a thiomsú mar gheall ar 2 earráid roimhe seo
> ```
>
> I gCaibidil 10, pléifimid conas na hearráidí seo a cheartú ionas gur féidir leat iad a stóráil
> tagairtí i struchtúir, ach faoi láthair, socróimid earráidí mar seo ag baint úsáide as úinéireacht
> cineálacha cosúil le `String` in ionad tagairtí cosúil le `&str`.

<!-- manual-regeneration
for the error above
after running update-rustc.sh:
pbcopy < listings/ch05-using-structs-to-structure-related-data/no-listing-02-reference-in-struct/output.txt
paste above
add `> ` before every line -->

[tuples]: ch03-02-data-types.html#the-tuple-type
[move]: ch04-01-what-is-ownership.html#variables-and-data-interacting-with-move
[copy]: ch04-01-what-is-ownership.html#stack-only-data-copy




