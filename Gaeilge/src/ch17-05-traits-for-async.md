## Breathnú níos géire ar na tréithe le haghaidh Asyncrónach

<!-- Old headings. Do not remove or links may break. -->

<a id="digging-into-the-traits-for-async"></a>

Ar fud na caibidle, úsáidimid na tréithe `Future`, `Pin`, `Unpin`, `Stream`, agus
`StreamExt` ar bhealaí éagsúla. Go dtí seo, áfach, sheachain muid dul ró-dhomhain isteach sna sonraí maidir le conas a oibríonn siad nó conas a oireann siad le chéile, rud atá go breá
an chuid is mó den am do d'obair laethúil Rust. Uaireanta, áfach,
tiocfaidh tú trasna ar chásanna ina mbeidh ort cúpla ceann eile de na sonraí seo a thuiscint. Sa chuid seo, déanfaimid tochailt isteach go leor chun cabhrú sna cásanna sin,
ag fágáil an tumadh _an-domhain_ fós le haghaidh doiciméadú eile.

<!-- Old headings. Do not remove or links may break. -->

<a id="future"></a>

### Tréith an ‘Todhchaí’

Tosaímis trí bhreathnú níos géire ar an gcaoi a n-oibríonn tréith an ‘Todhchaí’. Seo mar a shainmhíníonn Rust í:

```rust
use std::pin::Pin;
use std::task::{Context, Poll};

pub trait Future {
    type Output;

    fn poll(self: Pin<&mut Self>, cx: &mut Context<'_>) -> Poll<Self::Output>;
}
```

Áirítear leis an sainmhíniú tréithe sin roinnt cineálacha nua agus roinnt comhréir nach bhfacamar cheana, mar sin déanaimis siúl tríd an sainmhíniú píosa ar phíosa.

Ar dtús, deir cineál gaolmhar `Future`, `Output`, cad a réitíonn an todhchaí.

Tá sé seo cosúil leis an gcineál gaolmhar `Item` don tréith `Iterator`.
Ar an dara dul síos, tá an modh `poll` ag `Future` freisin, a ghlacann tagairt speisialta `Pin` dá pharaiméadar `self` agus tagairt inathraithe do chineál `Context`,
agus a thugann `Poll<Self::Output>` ar ais. Labhróimid níos mó faoi `Pin` agus
`Context` i gceann nóiméid. Anois, díreoimid ar a dtugann an modh ar ais,
an cineál `Poll`:

```rust
enum Poll<T> {
    Ready(T),
    Pending,
}
```

Tá an cineál `Poll` seo cosúil le `Option`. Tá malairt amháin ann a bhfuil luach aige,
`Ready(T)`, agus ceann nach bhfuil, `Pending`. Ciallaíonn `Poll` rud éigin go hiomlán difriúil ó `Option`, áfach! Léiríonn an malairt `Pending` go bhfuil obair le déanamh ag an todhchaí
fós, mar sin beidh ar an nglaoiteoir seiceáil arís níos déanaí. Léiríonn an malairt `Ready` go bhfuil a chuid oibre críochnaithe ag an todhchaí agus go bhfuil an luach `T`
ar fáil.

> Nóta: Le formhór na dtodhchaí, níor cheart don ghlaoiteoir glaoch ar `poll` arís tar éis don todhchaí `Ready` a thabhairt ar ais. Beidh scaoll ar go leor todhchaí má dhéantar polláil orthu arís tar éis
> dóibh a bheith réidh. Déarfaidh todhchaí atá sábháilte le polláil arís é sin go sainráite ina
> ndoiciméadacht. Tá sé seo cosúil leis an gcaoi a n-iompraíonn `Iterator::next`.

Nuair a fheiceann tú cód a úsáideann `await`, tiomsaíonn Rust é faoi chochall chun cód a ghlaonn ar `poll`. Má fhéachann tú siar ar Liostáil 17-4, áit ar phriontáileamar amach teideal an leathanaigh le haghaidh URL aonair nuair a réitíodh é, tiomsaíonn Rust é i rud éigin cosúil le seo (cé nach bhfuil sé go díreach):

```rust,ignore
match page_title(url).poll() {
    Ready(page_title) => match page_title {
        Some(title) => println!("The title for {url} was {title}"),
        None => println!("{url} had no title"),
    }
    Pending => {
        // But what goes here?
    }
}
```

Cad ba cheart dúinn a dhéanamh nuair atá an todhchaí fós 'Ar Feitheamh'? Teastaíonn bealach éigin uainn chun iarracht a dhéanamh arís, agus arís, agus arís eile, go dtí go mbeidh an todhchaí réidh faoi dheireadh. I bhfocail eile, teastaíonn lúb uainn:

```rust,ignore
let mut page_title_fut = page_title(url);
loop {
    match page_title_fut.poll() {
        Ready(value) => match page_title {
            Some(title) => println!("The title for {url} was {title}"),
            None => println!("{url} had no title"),
        }
        Pending => {
            // continue
        }
    }
}
```

Dá mba rud é gur thiomsaigh Rust é leis an gcód sin go díreach, áfach, bheadh ​​gach 'await' ina
bhac - díreach os coinne an rud a bhíomar ag iarraidh! Ina áit sin, cinntíonn Rust
go bhféadann an lúb smacht a thabhairt do rud éigin ar féidir leis obair ar an
todhchaí seo a chur ar sos chun oibriú ar thodhchaí eile agus ansin an ceann seo a sheiceáil arís níos déanaí. Mar a
fheicimid, is rith-am neamhshioncrónach é an rud sin, agus is é an obair sceidealaithe agus chomhordaithe seo
ceann dá phríomhphoist.

Níos luaithe sa chaibidil, rinneamar cur síos ar fanacht ar `rx.recv`. Tugann an glao `recv`
todhchaí ar ais, agus déanann fanacht ar an todhchaí pobalbhreith air. Thugamar faoi deara go gcuirfidh rith-am
an todhchaí ar sos go dtí go mbeidh sé réidh le `Some(message)` nó `None` nuair a dhúnann an
cainéal. Leis an tuiscint níos doimhne atá againn ar an tréith `Future`, agus
go sonrach `Future::poll`, is féidir linn a fheiceáil conas a oibríonn sé sin. Tá a fhios ag an rith-am nach bhfuil an
todhchaí réidh nuair a thugann sé `Poll::Pending` ar ais. Os a choinne sin, tá a fhios ag an am reatha go bhfuil an todhchaí _réidh_ agus cuireann sé chun cinn é nuair a thugann `poll` `Poll::Ready(Some(sessage))` nó `Poll::Ready(None)` ar ais.

Tá na sonraí beachta maidir le conas a dhéanann am reatha é sin lasmuigh de raon feidhme an leabhair seo,
ach is é an eochair ná meicnic bhunúsacha na dtodhchaí a fheiceáil: déanann am reatha _polls_ ar gach
todhchaí a bhfuil sé freagrach as, ag cur an todhchaí ar ais ina chodladh nuair nach bhfuil sé
réidh fós.

<!-- Old headings. Do not remove or links may break. -->

<a id="pinning-and-the-pin-and-unpin-traits"></a>

### Tréithe `Pin` agus `Unpin`

Nuair a thugamar isteach an coincheap maidir le bioráin i Liosta 17-16, tháinig teachtaireacht earráide an-deacair orainn. Seo an chuid ábhartha di arís:

<!-- manual-regeneration
cd listings/ch17-async-await/listing-17-16
cargo build
copy *only* the final `error` block from the errors
-->

```text
error[E0277]: `{async block@src/main.rs:10:23: 10:33}` cannot be unpinned
  --> src/main.rs:48:33
   |
48 |         trpl::join_all(futures).await;
   |                                 ^^^^^ the trait `Unpin` is not implemented for `{async block@src/main.rs:10:23: 10:33}`, which is required by `Box<{async block@src/main.rs:10:23: 10:33}>: Future`
   |
   = note: consider using the `pin!` macro
           consider using `Box::pin` if you need to access the pinned value outside of the current scope
   = note: required for `Box<{async block@src/main.rs:10:23: 10:33}>` to implement `Future`
note: required by a bound in `futures_util::future::join_all::JoinAll`
  --> file:///home/.cargo/registry/src/index.crates.io-6f17d22bba15001f/futures-util-0.3.30/src/future/join_all.rs:29:8
   |
27 | pub struct JoinAll<F>
   |            ------- required by a bound in this struct
28 | where
29 |     F: Future,
   |        ^^^^^^ required by this bound in `JoinAll`
```

Insíonn an teachtaireacht earráide seo dúinn ní hamháin go gcaithfimid na luachanna a phionáil ach freisin cén fáth go bhfuil
pionáil ag teastáil. Tugann an fheidhm `trpl::join_all` struchtúr ar ais ar a dtugtar
`JoinAll`. Tá an struchtúr sin cineálach thar chineál `F`, atá srianta chun
an tréith `Future` a chur i bhfeidhm. Trí thodhchaí a choinneáil go díreach le `await`, prionálann tú an
todhchaí go hintíreach. Sin an fáth nach gá dúinn `pin!` a úsáid i ngach áit ar mhaith linn
todhchaí a choinneáil.

Mar sin féin, nílimid ag fanacht go díreach le todhchaí anseo. Ina áit sin, tógfaimid
todhchaí nua, `JoinAll`, trí bhailiúchán todhchaí a rith chuig an bhfeidhm `join_all`. Éilíonn an síniú do `join_all` go gcuireann na cineálacha míreanna sa
bhailiúchán an tréith `Future` i bhfeidhm go léir, agus nach gcuireann `Box<T>` `Future` i bhfeidhm ach amháin má tá an `T` a fhilleann sé ina thodhchaí a chuireann an tréith `Unpin` i bhfeidhm.

Is mór an méid sin le glacadh! Chun tuiscint cheart a fháil air, déanaimis iniúchadh níos doimhne ar an gcaoi a n-oibríonn an tréith ‘Todhchaí’ i ndáiríre, go háirithe maidir le _pinning_.

Féach arís ar shainmhíniú na tréithe ‘Todhchaí’:

```rust
use std::pin::Pin;
use std::task::{Context, Poll};

pub trait Future {
    type Output;

    // Required method
    fn poll(self: Pin<&mut Self>, cx: &mut Context<'_>) -> Poll<Self::Output>;
}
```

Is iad an paraiméadar `cx` agus a chineál `Context` an eochair do conas a bhíonn a fhios ag rith-am cathain is ceart aon todhchaí ar leith a sheiceáil agus fós leisciúil. Arís, tá sonraí
an chaoi a n-oibríonn sé sin lasmuigh de raon feidhme na caibidle seo, agus de ghnáth ní gá duit ach
smaoineamh air seo agus tú ag scríobh cur i bhfeidhm saincheaptha `Future`. Díreoimid
ina ionad sin ar an gcineál do `self`, mar is é seo an chéad uair a chonaiceamar
modh ina bhfuil anótáil cineáil ag `self`. Oibríonn anótáil cineáil do `self`
cosúil le hanótálacha cineáil do pharaiméadair feidhme eile, ach le dhá phríomhdhifríocht:

- Insíonn sé do Rust cén cineál a chaithfidh `self` a bheith ann chun go nglaofar ar an modh.

- Ní féidir leis a bheith ina chineál ar bith. Tá sé srianta don chineál ar a bhfuil an modh curtha i bhfeidhm, tagairt nó pointeoir cliste don chineál sin, nó `pin` ag timfhilleadh
tagairt don chineál sin.

Feicfimid tuilleadh ar an gcomhréir seo i [Caibidil 18][ch-18]<!-- neamhaird -->. Faoi láthair,
is leor a fhios go más mian linn todhchaí a vótáil chun a sheiceáil an bhfuil sé
`Pending` nó `Ready(Output)`, teastaíonn tagairt inathraithe fillte le `Pin` uainn don
chineál.

Is fillteán é `Pin` do chineálacha cosúil le pointeoir ar nós `&`, `&mut`, `Box`, agus `Rc`.

(Go teicniúil, oibríonn `Pin` le cineálacha a chuireann tréithe `Deref` nó `DerefMut` i bhfeidhm,
ach is ionann é seo go héifeachtach agus oibriú le pointeoirí amháin.) Ní pointeoir é féin é `Pin` agus níl aon iompar aige féin mar atá ag `Rc` agus
`Arc` le comhaireamh tagartha; is uirlis amháin é is féidir leis an tiomsaitheoir a úsáid chun
srianta a fhorfheidhmiú ar úsáid pointeora.

Ag cuimhneamh go gcuirtear `await` i bhfeidhm i dtéarmaí glaonna chuig `poll`, tosaíonn sé ag
míniú an teachtaireacht earráide a chonaiceamar níos luaithe, ach bhí sé sin i dtéarmaí `Unpin`, ní
`Pin`. Mar sin, cén bhaint atá ag `Pin` le `Unpin` go díreach, agus cén fáth a gcaithfidh `Future` `self` a bheith i gcineál `Pin` chun `poll` a ghlaoch?

Cuimhnigh ó níos luaithe sa chaibidil seo go ndéantar sraith pointí feithimh i bhfuture a thiomsú i meaisín stáit, agus cinntíonn an tiomsaitheoir go leanann an meaisín stáit sin gach gnáthriail de chuid Rust maidir le sábháilteacht, lena n-áirítear iasacht agus
úinéireacht. Chun sin a chur ag obair, féachann Rust ar na sonraí atá ag teastáil idir pointe
faitimh amháin agus an chéad phointe feithimh eile nó deireadh an bhloic neamhshioncrónaigh. Ansin cruthaíonn sé malairt chomhfhreagrach sa mheaisín stáit tiomsaithe. Faigheann gach malairt
an rochtain atá ag teastáil uaidh ar na sonraí a úsáidfear sa chuid sin den
chód foinse, bíodh sé trí úinéireacht a ghlacadh ar na sonraí sin nó trí thagairt inathraithe nó
neamhathraithe a fháil dó.

Go dtí seo, tá gach rud go breá: má fhaighimid aon rud mícheart faoin úinéireacht nó faoi na tagairtí i
bhloc neamhshioncrónach ar leith, inseoidh an seiceálaí iasachta dúinn é. Nuair is mian linn bogadh timpeall
an todhchaí a fhreagraíonn don bhloc sin—mar shampla é a bhogadh isteach i `Vec` le cur ar aghaidh chuig
`join_all`—éiríonn rudaí níos casta.

Nuair a bhogaimid todhchaí—cibé acu trína bhrú isteach i struchtúr sonraí le húsáid mar
athraitheoir le `join_all` nó trína thabhairt ar ais ó fheidhm—ciallaíonn sé sin i ndáiríre
an meaisín stáit a chruthaíonn Rust dúinn a bhogadh. Agus murab ionann agus an chuid is mó de na cineálacha eile i
Rust, is féidir leis na todhchaí a chruthaíonn Rust do bhloic neamhshioncrónacha tagairtí a bheith acu
dóibh féin i réimsí aon athraithe ar leith, mar a thaispeántar sa léaráid shimplithe i bhFíor 17-4.

<figure>

<img alt="Tábla aoncholún, trí shraith a léiríonn todhchaí, fut1, a bhfuil luachanna sonraí 0 agus 1 sna chéad dá shraith agus saighead ag pointeáil ón tríú sraith ar ais go dtí an dara sraith, ag léiriú tagairt inmheánach laistigh den todhchaí." src="img/trpl17-04.svg" class="center" />

<figcaption>Fíor 17-4: Cineál sonraí féin-thagartha.</figcaption>

</figure>

De réir réamhshocraithe, áfach, níl aon réad a bhfuil tagairt dó féin sábháilte a bhogadh,
toisc go mbíonn tagairtí i gcónaí ag tagairt don seoladh cuimhne iarbhír de cibé rud a
dtagraíonn siad dó (féach Fíor 17-5). Má bhogann tú an struchtúr sonraí féin, fágfar na
tagairtí inmheánacha sin ag pointeáil chuig an sean-suíomh. Mar sin féin, tá an
suíomh cuimhne sin neamhbhailí anois. Ar an gcéad dul síos, ní dhéanfar a luach a nuashonrú
nuair a dhéanann tú athruithe ar an struchtúr sonraí. Ar an gcéad dul síos - rud níos tábhachtaí - tá an ríomhaire saor anois an chuimhne sin a athúsáid chun críocha eile! D’fhéadfá
sonraí nach mbaineann leis ar chor ar bith a léamh níos déanaí.

<figure>

<img alt="Dhá thábla, a léiríonn dhá thodhchaí, fut1 agus fut2, agus colún amháin agus trí shraith i ngach ceann acu, rud a léiríonn toradh todhchaí a bhogadh amach as fut1 isteach i fut2. Tá an chéad cheann, fut1, liath, le comhartha ceiste i ngach innéacs, rud a léiríonn cuimhne anaithnid. Tá 0 agus 1 sa chéad agus sa dara sraith ag an dara ceann, fut2, agus saighead ag pointeáil óna thríú sraith ar ais go dtí an dara sraith de fut1, rud a léiríonn pointeoir atá ag tagairt don sean-suíomh i gcuimhne an todhchaí sular aistríodh é." src="img/trpl17-05.svg" class="center" />

<figcaption>Fíor 17-5: An toradh neamhshábháilte a bhaineann le cineál sonraí féin-thagartha a bhogadh</figcaption>

</figure>

Go teoiriciúil, d'fhéadfadh an tiomsaitheoir Rust iarracht a dhéanamh gach tagairt do
réad a nuashonrú aon uair a bhogtar é, ach d'fhéadfadh sé sin go leor forchostais feidhmíochta a chur leis,
go háirithe má tá gá le gréasán iomlán tagairtí a nuashonrú. Dá bhféadfaimis a chinntiú ina ionad sin nach mbogann an struchtúr sonraí atá i gceist _sa chuimhne_, ní bheadh ​​orainn
aon tagairtí a nuashonrú. Seo go díreach a éilíonn seiceálaí iasachta Rust:
i gcód sábháilte, cuireann sé cosc ​​​​ort aon mhír a bhogadh a bhfuil tagairt ghníomhach aici
dó.

Tógann `Pin` air sin chun an ráthaíocht chruinn atá de dhíth orainn a thabhairt dúinn. Nuair a _phionánaimid_ luach
trí phointeoir chuig an luach sin a fhilleadh i `Pin`, ní féidir leis bogadh a thuilleadh. Dá bhrí sin,
má tá `Pin<Box<SomeType>>` agat, bioránn tú an luach `SomeType` i ndáiríre, _ní_ an pointeoir `Box`. Léiríonn Fíor 17-6 an próiseas seo.

<figure>

<img alt="Trí bhosca leagtha amach taobh le taobh. Tá lipéad “Pin” ar an gcéad cheann, “b1” ar an dara ceann, agus “pinned” ar an tríú ceann. Laistigh de “pinned” tá tábla lipéadaithe “fut”, le colún amháin; seasann sé do thodhchaí le cealla do gach cuid den struchtúr sonraí. Tá an luach “0” ar a chéad chill, tá saighead ag teacht amach as an dara cill agus ag pointeáil chuig an gceathrú cill agus an chill dheireanach, a bhfuil an luach “1” inti, agus tá línte stróicthe agus eilipsis ar an tríú cill chun a léiriú go bhféadfadh codanna eile a bheith sa struchtúr sonraí. Le chéile, seasann an tábla “fut” do thodhchaí atá féin-thagartha. Fágann saighead an bosca lipéadaithe “Pin”, téann sí tríd an mbosca lipéadaithe “b1” agus críochnaíonn sí taobh istigh den bhosca “pinned” ag an tábla “fut”." src="img/trpl17-06.svg" class="center" />

<figcaption>Fíor 17-6: Ag bioránáil `Box` a dhíríonn ar chineál todhchaí féin-thagartha.</figcaption>

</figure>

Déanta na fírinne, is féidir leis an pointeoir `Box` bogadh timpeall go saor fós. Cuimhnigh: is cúram dúinn a chinntiú go bhfanann na sonraí atá á dtagairt sa deireadh ina n-áit. Má bhogann pointeoir
timpeall, _ach go bhfuil na sonraí a bhfuil sé ag pointeáil orthu san áit chéanna_, mar atá i bhFíor
17-7, níl aon fhadhb ann. Mar chleachtadh neamhspleách, féach ar na doiciméid
do na cineálacha chomh maith leis an modúl `std::pin` agus déan iarracht a fháil amach conas a dhéanfá
é seo le `Pin` ag timfhilleadh `Box`.) Is é an rud is tábhachtaí ná nach féidir leis an gcineál féin-thagartha
féin bogadh, toisc go bhfuil sé fós bioráilte.

<figure>

<img alt="Ceithre bhosca leagtha amach i dtrí cholún garbha, mar an gcéanna leis an léaráid roimhe seo le hathrú ar an dara colún. Anois tá dhá bhosca sa dara colún, lipéadaithe “b1” agus “b2”, tá “b1” liath, agus téann an tsaighead ó “Pin” trí “b2” in ionad “b1”, rud a léiríonn gur bhog an pointeoir ó “b1” go “b2”, ach níor bhog na sonraí i “pinned”." src="img/trpl17-07.svg" class="center" />

<figcaption>Fíor 17-7: Bogadh ‘Bosca’ a dhíríonn ar chineál todhchaí féin-thagartha.</figcaption>

</figure>

Mar sin féin, tá sé sábháilte bogadh timpeall an chuid is mó de na cineálacha, fiú má tharlaíonn siad a bheith
taobh thiar de phointeoir ‘Pin’. Ní gá dúinn smaoineamh ar phionáil ach nuair a bhíonn
tagairtí inmheánacha ag míreanna. Tá luachanna príomhúla ar nós uimhreacha agus Booleans sábháilte
ós rud é nach bhfuil aon tagairtí inmheánacha acu ar ndóigh, mar sin tá siad
sábháilte ar ndóigh. Ní bhíonn formhór na gcineálacha a n-oibríonn tú leo de ghnáth i Rust sábháilte ach an oiread. Is féidir leat bogadh timpeall
`Vec`, mar shampla, gan a bheith buartha. Ag smaoineamh ar an méid atá feicthe againn go dtí seo amháin, má
tá `Pin<Vec<String>>` agat, bheadh ​​​​ort gach rud a dhéanamh trí na APIanna sábháilte ach
srianta a sholáthraíonn `Pin`, cé go bhfuil `Vec<String>` sábháilte i gcónaí
le bogadh mura bhfuil aon tagairtí eile ann dó. Teastaíonn bealach uainn chun a rá leis an
tiomsaitheoir go bhfuil sé ceart go leor míreanna a bhogadh timpeall i gcásanna mar seo - agus sin
an áit a dtagann `Unpin` i bhfeidhm.

Is tréith marcóra é `Unpin`, cosúil leis na tréithe `Send` agus `Sync` a chonaiceamar i
gCaibidil 16, agus mar sin níl aon fheidhmiúlacht aige féin. Níl tréithe marcóra ann ach chun a chur in iúl don tiomsaitheoir go bhfuil sé sábháilte an cineál a úsáid a chuireann tréith áirithe i bhfeidhm i gcomhthéacs ar leith. Cuireann `Unpin` in iúl don tiomsaitheoir nach gá do chineál áirithe aon ráthaíochtaí a choinneáil faoi cibé an féidir an luach atá i gceist a bhogadh go sábháilte.

<!--
Is é an aidhm atá leis an `<code>` inlíne sa chéad bhloc eile ná an `<em>` inlíne a cheadú istigh ann,
ag teacht leis an méid a dhéanann NoStarch ó thaobh stíl de, agus ag béimniú laistigh den téacs anseo
gur rud éigin difriúil é ó ghnáthchineál.
-->

Díreach mar atá le `Send` agus `Sync`, cuireann an tiomsaitheoir `Unpin` i bhfeidhm go huathoibríoch
do gach cineál ina bhféadann sé a chruthú go bhfuil sé sábháilte. Cás speisialta, arís cosúil le
`Send` agus `Sync`, ná nuair nach gcuirtear `Unpin` i bhfeidhm le haghaidh cineál. Is é an
nótaíocht don seo ná <code>impl !Unpin do <em>SomeType</em></code>, áit a bhfuil
<code><em>SomeType</em></code> ina ainm ar chineál a _ní mór_ dó na ráthaíochtaí sin a choinneáil slán
a bheith sábháilte aon uair a úsáidtear pointeoir chuig an gcineál sin i `Pin`.

I bhfocail eile, tá dhá rud le coinneáil i gcuimhne faoin ngaol
idir `Pin` agus `Unpin`. Ar dtús, is é `Unpin` an cás “gnáth”, agus is é `!Unpin` an cás speisialta. Ar an dara dul síos, níl aon tábhacht ach nuair a bhíonn pointeoir bioráilte á úsáid agat don chineál sin cosúil le <code>Pin<&mut
<em>SomeType</em>></code>.

Chun sin a dhéanamh soiléir, smaoinigh ar `String`: tá fad aige agus na carachtair Unicode
a dhéanann suas é. Is féidir linn `String` a fhilleadh i `Pin`, mar a fheictear i bhFíor
17-8. Mar sin féin, cuireann `String` `Unpin` i bhfeidhm go huathoibríoch, mar a dhéanann formhór na gcineálacha eile
i Rust.

<figure>

<img alt="Sreabhadh oibre comhthráthach" src="img/trpl17-08.svg" class="center" />

<figcaption>Fíor 17-8: `String` a phionáil; Léiríonn an líne phoncaithe go gcuireann an `String` an tréith `Unpin` i bhfeidhm, agus dá bhrí sin nach bhfuil sé bioráilte.</figcaption>

</figure>

Mar thoradh air sin, is féidir linn rudaí a dhéanamh a bheadh ​​​​mídhleathach dá gcuirfeadh `String` `!Unpin` i bhfeidhm ina ionad, amhail teaghrán amháin a athsholáthar le ceann eile ag an suíomh céanna sa chuimhne mar atá i bhFíor 17-9. Ní sháraíonn sé seo an conradh `Pin`,
toisc nach bhfuil aon tagairtí inmheánacha ag `String` a fhágann go bhfuil sé neamhshábháilte bogadh timpeall!
Sin é an fáth go díreach a gcuireann sé `Unpin` i bhfeidhm seachas `!Unpin`.

<figure>

<img alt="Sreabhadh oibre comhuaineach" src="img/trpl17-09.svg" class="center" />

<figcaption>Fíor 17-9: An `String` á athsholáthar le `String` atá go hiomlán difriúil sa chuimhne.</figcaption>

</figure>

Anois tá a fhios againn go leor chun na hearráidí a tuairiscíodh don ghlao `join_all` sin a thuiscint
ó chúl i Liosta 17-17. Ar dtús rinneamar iarracht na todhchaí a tháirgtear ag
bloic async a bhogadh isteach i `Vec<Box<dyn Future<Output = ()>>>`, ach mar a chonaiceamar,
d’fhéadfadh tagairtí inmheánacha a bheith ag na todhchaí sin, mar sin ní chuireann siad `Unpin` i bhfeidhm.
Ní mór iad a phionáil, agus ansin is féidir linn an cineál `Pin` a chur isteach sa `Vec`,
muiníneach nach mbogfar na sonraí bunúsacha sna todhchaí.

Tá `Pin` agus `Unpin` tábhachtach den chuid is mó chun leabharlanna íochtaracha a thógáil, nó
nuair atá tú ag tógáil rith-ama féin, seachas le haghaidh cód Rust laethúil.
Nuair a fheiceann tú na tréithe seo i dteachtaireachtaí earráide, áfach, beidh tuiscint níos fearr agat anois ar conas do chód a shocrú!

> Nóta: Leis an teaglaim seo de `Pin` agus `Unpin` is féidir rang iomlán cineálacha casta a chur i bhfeidhm go sábháilte i Rust a bheadh ​​dúshlánach murach sin
> toisc go bhfuil siad féin-thagartha. Is minic a fheictear cineálacha a éilíonn `Pin` i Rust neamhshioncrónach inniu, ach ó am go ham, d'fhéadfá iad a fheiceáil
> i gcomhthéacsanna eile freisin.

> Tá na sonraí maidir le conas a oibríonn `Pin` agus `Unpin`, agus na rialacha a bhfuil orthu
> a choinneáil, clúdaithe go fairsing sa doiciméadacht API do `std::pin`, mar sin
> más spéis leat tuilleadh a fhoghlaim, is áit iontach é sin le tosú. >
> Más mian leat tuiscint níos mine a fháil ar an gcaoi a n-oibríonn rudaí faoin gcochall,
> féach ar Chaibidlí [2][faoi chochall] agus [4][bioráin] de [_Asynchronous
> Programming in Rust_][async-book].

### Tréith an `Stream`

Anois go bhfuil tuiscint níos doimhne agat ar na tréithe `Future`, `Pin`, agus `Unpin`, is féidir linn ár n-aird a dhíriú ar an tréith `Stream`. Mar a d'fhoghlaim tú níos luaithe sa
chaibidil, tá sruthanna cosúil le hathraitheoirí neamhshioncrónacha. Murab ionann agus `Iterator` agus
`Future`, áfach, níl aon sainmhíniú ar `Stream` sa leabharlann chaighdeánach tráth scríofa na tréimhse seo,
ach tá _sainmhíniú_ an-choitianta ann ón gcliathbhosca `futures` a úsáidtear
ar fud an éiceachórais.

Déanaimis athbhreithniú ar shainmhínithe na dtréithe `Iterator` agus `Future` sula
mbreathnaímid ar an gcaoi a bhféadfadh tréith `Stream` iad a chumasc le chéile. Ó `Iterator`, tá
an smaoineamh againn ar sheicheamh: soláthraíonn a mhodh `next` `Option<Self::Item>`.
Ó `Future`, tá an smaoineamh againn ar ullmhacht le himeacht ama: soláthraíonn a mhodh `poll` `Poll<Self::Output>`. Chun sraith míreanna a léiriú a bhíonn réidh le himeacht ama, sainmhínímid tréith `Stream` a chuireann na gnéithe sin le chéile:

```rust
use std::pin::Pin;
use std::task::{Context, Poll};

trait Stream {
    type Item;

    fn poll_next(
        self: Pin<&mut Self>,
        cx: &mut Context<'_>
    ) -> Poll<Option<Self::Item>>;
}
```

Sainmhíníonn an tréith `Stream` cineál gaolmhar ar a dtugtar `Mír` don chineál
míreanna a tháirgeann an sruth. Tá sé seo cosúil le `Iterator`, áit a bhféadfadh
nialas míreanna a bheith ann go leor, agus murab ionann agus `Future`, áit a mbíonn `Output` aonair i gcónaí, fiú más é an cineál aonaid `()` é.

Sainmhíníonn `Stream` modh freisin chun na míreanna sin a fháil. Tugtar `poll_next` air, chun
a shoiléiriú go ndéanann sé pobalbhreith ar an mbealach céanna a dhéanann `Future::poll` agus go dtáirgeann sé
seicheamh míreanna ar an mbealach céanna a dhéanann `Iterator::next`. Comhcheanglaíonn a chineál fillte `Poll` le `Rogha`. Is é `Poll` an cineál seachtrach, mar go gcaithfear a sheiceáil le haghaidh ullmhachta, díreach mar a dhéanann todhchaí. Is é `Rogha` an cineál inmheánach,
mar go gcaithfidh sé comhartha a thabhairt an bhfuil níos mó teachtaireachtaí ann, díreach mar a dhéanann athráiteoir.

Is dócha go mbeidh rud éigin an-chosúil leis an sainmhíniú seo mar chuid de
leabharlann chaighdeánach Rust. Idir an dá linn, is cuid de threalamh fhormhór na rith-amanna é, mar sin
is féidir leat brath air, agus ba cheart go mbeadh feidhm ag gach rud a chlúdóimid ina dhiaidh seo go ginearálta!

Sa sampla a chonaiceamar sa chuid ar shruthú, áfach, níor úsáideadh
`poll_next` _nó_ `Stream`, ach ina ionad sin úsáideadh `next` agus `StreamExt`. _D'fhéadfaimis_
oibriú go díreach i dtéarmaí API `poll_next` trí ár meaisíní stáit `Stream` féin a scríobh de láimh, ar ndóigh, díreach mar a _d'fhéadfaimis_ oibriú le todhchaí go díreach trína modh `poll`. Tá úsáid `await` i bhfad níos deise, áfach, agus soláthraíonn an tréith `StreamExt` an modh `next` ionas gur féidir linn é sin a dhéanamh:

```rust
{{#rustdoc_include ../../listings/ch17-async-await/no-listing-stream-ext/src/lib.rs:here}}
```

<!--
LE DO DHÉANAMH: nuashonraigh é seo má/nuair a nuashonraíonn tokio/etc. a MSRV agus aistrigh go feidhmeanna neamhshioncrónacha a úsáid
i dtréithe, ós rud é gurb é an easpa sin an chúis nach bhfuil sé seo acu fós.
-->

> Nóta: Tá cuma beagán difriúil ar an sainmhíniú iarbhír a d'úsáideamar níos luaithe sa chaibidil ná seo, toisc go dtacaíonn sé le leaganacha de Rust nár thacaigh
> le feidhmeanna neamhshioncrónacha a úsáid i dtréithe fós. Mar thoradh air sin, tá cuma mar seo air:
>
> ```rust,ignore
> fn next(&mut self) -> Next<'_, Self> where Self: Unpin;
> ```
>
> Is `struct` an cineál `Next` sin a chuireann `Future` i bhfeidhm agus a ligeann dúinn saolré an tagartha do `self` a ainmniú
> le `Next<'_, Self>`, ionas gur féidir le `await`
> oibriú leis an modh seo.

Is é an tréith `StreamExt` baile na modhanna suimiúla go léir atá ar fáil
le húsáid le sruthanna freisin. Cuirtear `StreamExt` i bhfeidhm go huathoibríoch do gach cineál
a chuireann `Stream` i bhfeidhm, ach sainmhínítear na tréithe seo ar leithligh chun go mbeidh an pobal in ann athrá a dhéanamh ar APIanna áise gan cur isteach ar an
tréith bhunúsach.

Sa leagan de `StreamExt` a úsáidtear sa chliathán `trpl`, ní hamháin go sainmhíníonn an tréith an modh `next` ach soláthraíonn sí cur i bhfeidhm réamhshocraithe de `next`
a láimhseálann sonraí glao `Stream::poll_next` i gceart. Ciallaíonn sé seo
fiú nuair is gá duit do chineál sonraí sruthú féin a scríobh, nach gá duit ach `Stream` a chur i bhfeidhm, agus ansin is féidir le duine ar bith a úsáideann do chineál sonraí `StreamExt` agus a mhodhanna a úsáid leis go huathoibríoch.

Sin a bhfuilimid chun a chlúdach le haghaidh na sonraí níos ísle ar na tréithe seo. Chun
mar fhocal scoir, déanaimis machnamh ar an gcaoi a n-oireann todhchaí (lena n-áirítear sruthanna), tascanna, agus snáitheanna
le chéile!

[ch-18]: ch18-00-oop.html
[async-book]: https://rust-lang.github.io/async-book/
[under-the-hood]: https://rust-lang.github.io/async-book/02_execution/01_chapter.html
[pinning]: https://rust-lang.github.io/async-book/04_pinning/01_chapter.html
[first-async]: ch17-01-futures-and-syntax.html#our-first-async-program
[any-number-futures]: ch17-03-more-futures.html#working-with-any-number-of-futures	
